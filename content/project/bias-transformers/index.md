---
title: Biases and Stereotypes in StableDiffusion
summary: Automatically create pictures with StableDiffusion from a given prompt and analyze them with DeepFace. What stereotypes and biases are embedded in StableDiffusion? How far do they reach and what could be done to elimate existing biases? What gender will the people in the scene have with the following description "a nurse talks to a doctor" ?

tags:
  - Natural Language Processing
date: '2023-02-28T00:00:00Z'

# Optional external URL for project (replaces project detail page).
external_link: ''

image:
  focal_point: Smart

---
Resources:
- L. Struppek, D. Hintersdorf, F. Friedrich, M. Brack, P.Schramowski, K.Kersting, The Biased Artist, arxiv, 2022. 
- J. Salminen, S. Jung, B. Jansen, S. Chowdhury, Analyzing Demographic Bias in Artificially Generated Facial Pictures, CHI2020, 2020. 

As multimodal transformers like DALL-E and StableDiffusion become increasingly popular and accessible to the public, concerns about their neutrality are growing. To investigate these concerns, I have developed a small program that enables the analysis of output images from StableDiffusion to identify any potential biases or stereotypes present. This tool aims to provide greater transparency and accountability in the use of advanced AI technologies, helping to ensure that they are deployed ethically and responsibly.
```python
import torch
from diffusers import StableDiffusionPipeline
from PIL import Image
from deepface import DeepFace
import os
import pandas as pd

def create_image(imgs, prompt, counter, width, height):
    curr_img = Image.new('RGB', size=(width, height))
    curr_img.paste(imgs[0])
    curr_img.save('Images/'+ prompt.replace(' ', '_') + '_' + str(counter) + '.png')

def use_pipeline(prompt, input_seed):
    generator = torch.Generator(device=device)
    latents = None
    seeds = []
    if not input_seed:
        seed = generator.seed()
    else:
        seed = input_seed

    seeds.append(seed)
    generator = generator.manual_seed(seed)
    image_latents = torch.randn(
        (1, pipe.unet.in_channels, height // 8, width // 8),
        generator=generator,
        device=device
    )
    latents = image_latents if latents is None else torch.cat((latents, image_latents))
    with torch.autocast("cuda"):
        images = pipe(
            [prompt] * 1,
            guidance_scale=7.5,
            latents = latents,
            )
    nsfw = images['nsfw_content_detected']
    images = images['images']
    return images, nsfw


def seed_req(num_images):
    random_seed = input('Random seed? (y/n)')
    if random_seed != 'y':
        seeds = []
        seed_asc = input('Seed ascending? (y / n)')
        if seed_asc != 'y':
            while num_images > 0:
                print('you need' + num_images + 'more seeds')
                seeds.append = input('Which seeds do you want to use? Enter one seed')
                num_images -= 1
        else:
            seeds = range(0, num_images)
        return seeds

def main(img_filepath1, img_filepath2, dataset_path):
    backends = [
    'opencv',
    'ssd',
    'dlib',
    'mtcnn',
    'retinaface',
    'mediapipe'
    ]

    #facial analysis
    demography = DeepFace.analyze(img_path = img_filepath1, enforce_detection=False,
            detector_backend = backends[4], actions = ['gender']
    )

    output_list = []
    for i in range(len(demography)):
        output_list.append(demography[i]['gender']['Woman'])
        output_list.append(demography[i]['gender']['Man'])
    return output_list

def analyze(prompt):
    df = pd.DataFrame()
    all_outputs = []
    lengths = []
    for count, file in enumerate(os.listdir('Images')):
        if file.split('_')[:-1] == prompt.split(' '):
            output = main('Images/'+ file, "", "")
            lengths.append(int(len(output)/2))
            all_outputs.append(output)
    max_length = max(lengths)
    columns = []
    for i in range(0, max_length):
        columns.append(str(i) + ' Woman')
        columns.append(str(i) + ' Man')
    columns = ['num_faces'] + columns
    for idx, elem in enumerate(all_outputs):
        if lengths[idx] < max_length:
            for j in range(int(max_length - lengths[idx])*2):
                elem.append(0.0)
        all_outputs[idx] = [lengths[idx]] + elem

    df = pd.DataFrame(all_outputs, columns = columns)
    df.to_csv(prompt.replace(' ', '_') + '.csv', index=False)



if input('a to only analyze ') == 'a':
    analyze(input('Filename '))
else:
    print(torch.cuda.is_available())
    device = "cuda"
    model_id = "CompVis/stable-diffusion-v1-4"
    pipe = StableDiffusionPipeline.from_pretrained(
        model_id,
        revision="fp16",
        torch_dtype=torch.float16,
        use_auth_token='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',
    ).to(device)
    num_images = int(input('Anzahl an Bildern. '))
    width = int(input('Geben Sie die Breite der Bilder ein. '))
    height = int(input('Geben Sie die Höhe der Bilder ein. '))
    prompt = input('Geben Sie Ihren Prompt ein ')
    # seeds = seed_req(num_images)
    # max_images = num_images
    # no_nsfw = 1
    cn = 0
    while num_images > 0:
        curr_imgs, nsfw = use_pipeline(prompt, [])
        if nsfw[0]:
            # seeds[num_images] = max_images + no_nsfw
            pass
        elif not nsfw[0]:
            create_image(curr_imgs, prompt, cn, width, height)
            cn += 1
            num_images -=1
    analyze(prompt)

# df2 = pd.read_csv('man.csv') # read csv file
# print(df2)
```
The different state are Suspectible, Exposed, Infected and Recovered. Transimission between the states is possible with a calculated probability.

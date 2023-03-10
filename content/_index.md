---
# Leave the homepage title empty to use the site title
title:
date: 2022-10-24
type: landing

sections:
  - block: about.avatar
    id: about
    content:
      # Choose a user profile to display (a folder name within `content/authors/`)
      username: admin
      # Override your bio text from `authors/admin/_index.md`?
      text:
  - block: experience
    content:
      title: Experience
      # Date format for experience
      #   Refer to https://wowchemy.com/docs/customization/#date-format
      date_format: Jan 2006
      # Experiences.
      #   Add/remove as many `experience` items below as you like.
      #   Required fields are `title`, `company`, and `date_start`.
      #   Leave `date_end` empty if it's your current employer.
      #   Begin multi-line descriptions with YAML's `|2-` multi-line prefix.
      items:
        - title: Student Assistant - IT Support
          company: Goethe University
          company_url: ''
          company_logo: gu_logo
          location: Frankfurt am Main
          date_start: '2018-04-01'
          date_end: '2023-03-30'
          description: Managed IT infrastrucuture for the Department of Economics and its associated buildings. Assisted national and internation staff with technical issues
        - title:  Web development
          company: ITF Juniors Tournament Bruchköbel
          company_url: ''
          company_logo: itf_logo
          location: Bruchköbel
          date_start: '2020-08-01'
          date_end: '2021-08-01'
          description: Managed the upload/editing of articles on the tournament website. Entered tournament and match results.
                       Promoted the tournament experience on social media
        - title: IT Support
          company: AWO Bundesverband e.V.
          company_url: ''
          company_logo: ''
          location: Bruchköbel
          date_start: '2017-01-01'
          date_end: '2018-05-01'
          description: Voluntary helpdesk in cooperation with AWO. Assisted with technical problems and created guides for home-use. Prepared short presentations on Office programs
    design:
      columns: '3'
  - block: collection
    id: posts
    content:
      title: Recent Posts
      subtitle: ''
      text: ''
      # Choose how many pages you would like to display (0 = all pages)
      count: 5
      # Filter on criteria
      filters:
        folders:
          - post
        author: ""
        category: ""
        tag: ""
        exclude_featured: false
        exclude_future: false
        exclude_past: false
        publication_type: ""
      # Choose how many pages you would like to offset by
      offset: 0
      # Page order: descending (desc) or ascending (asc) date.
      order: desc
    design:
      # Choose a layout view
      view: compact
      columns: '2'
  - block: portfolio
    id: projects
    content:
      title: Projects
      filters:
        folders:
          - project
      # Default filter index (e.g. 0 corresponds to the first `filter_button` instance below).
      default_button_index: 0
      # Filter toolbar (optional).
      # Add or remove as many filters (`filter_button` instances) as you like.
      # To show all items, set `tag` to "*".
      # To filter by a specific tag, set `tag` to an existing tag name.
      # To remove the toolbar, delete the entire `filter_button` block.
      buttons:
        - name: All
          tag: '*'
        - name: Simulation
          tag: Simulation
        - name: Natural Language Processing
          tag: Natural Language Processing
        - name: Other
          tag: Other
    design:
      # Choose how many columns the section has. Valid values: '1' or '2'.
      columns: '1'
      view: showcase
      # For Showcase view, flip alternate rows?
      flip_alt_rows: false
  - block: contact
    id: contact
    content:
      title: Contact
      subtitle:
      # email: nils.dambowy@googlemail.com
      # Automatically link email and phone or display as text?
      autolink: true
      # Email form provider
      form:
        provider: netlify
        formspree:
          id:
        netlify:
          # Enable CAPTCHA challenge to reduce spam?
          captcha: true
    design:
      columns: '2'
---

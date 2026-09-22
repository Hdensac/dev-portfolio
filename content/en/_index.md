---
title: 'Isac-portfolio'
summary: ''
date: 2026-01-05
type: landing

sections:
  - block: dev-hero
    id: hero
    content:
      username: me
      greeting: "Hi, I'm"
      show_status: true
      show_scroll_indicator: true
      typewriter:
        enable: true
        prefix: "I build"
        strings:
          - "secure web applications"
          - "cybersecurity solutions"
          - "Python & PHP backends"
          - "network security tools"
        type_speed: 70
        delete_speed: 40
        pause_time: 2500
      cta_buttons:
        - text: View my projects
          url: "#projects"
          icon: arrow-down
        - text: Contact me
          url: "#contact"
          icon: envelope
    design:
      style: centered
      avatar_shape: circle
      animations: true
      background:
        color:
          light: "#fafafa"
          dark: "#0a0a0f"
      spacing:
        padding: ["6rem", "0", "4rem", "0"]

  - block: portfolio
    id: projects
    content:
      title: "Selected Projects"
      subtitle: "A selection of recent work"
      count: 0
      filters:
        folders:
          - projects
      buttons:
        - name: All
          tag: '*'
        - name: Full-Stack
          tag: Full-Stack
        - name: Cybersecurity
          tag: Cybersecurity
        - name: Research
          tag: Research
      default_button_index: 0
    design:
      columns: 3
      background:
        color:
          light: "#ffffff"
          dark: "#0d0d12"
      spacing:
        padding: ["4rem", "0", "4rem", "0"]

  - block: tech-stack
    id: skills
    content:
      title: "Technical Skills"
      subtitle: "Technologies and tools I use to build and secure applications"
      categories:
        - name: Languages
          items:
            - name: Python
              icon: devicon/python
            - name: PHP
              icon: devicon/php
            - name: JavaScript
              icon: devicon/javascript
            - name: SQL
              icon: devicon/postgresql
        - name: Web Frameworks
          items:
            - name: Django
              icon: brands/django
            - name: Laravel
              icon: devicon/laravel
            - name: Vue.js
              icon: devicon/vuejs
            - name: Tailwind CSS
              icon: devicon/tailwindcss
        - name: Security & Networks
          items:
            - name: GNS3 & Cooja
              icon: devicon/linux
            - name: MikroTik
              icon: devicon/linux
            - name: OWASP ZAP
              icon: devicon/linux
            - name: CrowdStrike
              icon: devicon/linux
        - name: Systems & Tools
          items:
            - name: Linux
              icon: devicon/linux
            - name: Git & GitHub
              icon: brands/github
            - name: Render
              icon: brands/render
            - name: Vercel
              icon: devicon/vercel
    design:
      style: grid
      show_levels: false
      background:
        color:
          light: "#f5f5f5"
          dark: "#08080c"
      spacing:
        padding: ["4rem", "0", "4rem", "0"]

  - block: resume-experience
    id: experience
    content:
      title: Experience
      date_format: Jan 2006
      items:
        - title: IT Department Intern - Dematerialization & Information Systems
          company: Ministry of Economy and Finance (MEF)
          company_url: ''
          company_logo: ''
          location: Benin
          date_start: '2025-03-01'
          date_end: '2025-06-30'
          description: |2-
            * Dematerialized the internship management process through a web application
            * Analyzed needs and improved access security
            * Duration: 3 months
        - title: IT Department Intern - Network & Systems Support
          company: Ministry of Economy and Finance (MEF)
          company_url: ''
          company_logo: ''
          location: Benin
          date_start: '2024-08-01'
          date_end: '2024-09-30'
          description: |2-
            * Maintained the wired network through crimping, cabling, and tests
            * Configured and secured Windows workstations
            * Duration: 2 months
        - title: IT Department Intern
          company: Ministry of Economy and Finance (MEF)
          company_url: ''
          company_logo: ''
          location: Benin
          date_start: '2023-09-01'
          date_end: '2023-09-30'
          description: |2-
            * Learned algorithmic fundamentals
            * Discovered MEF structures and the datacenter
            * Duration: 1 month
    design:
      columns: '1'
      background:
        color:
          light: "#ffffff"
          dark: "#0d0d12"
      spacing:
        padding: ["4rem", "0", "4rem", "0"]

  - block: collection
    id: blog
    content:
      title: Recent Articles
      subtitle: "Notes on web development, cybersecurity, and modern tools"
      text: ''
      filters:
        folders:
          - blog
        exclude_featured: false
      count: 3
      order: desc
    design:
      view: card
      columns: 3
      background:
        color:
          light: "#f5f5f5"
          dark: "#08080c"
      spacing:
        padding: ["4rem", "0", "4rem", "0"]

  - block: contact-info
    id: contact
    content:
      title: Contact Me
      subtitle: "Let's build something solid together"
      text: |-
        I am open to projects, academic internships, and collaborations around web development and cybersecurity.
        Feel free to reach out to discuss an opportunity.
      email: hdensac@gmail.com
      autolink: true
    design:
      columns: '1'
      background:
        color:
          light: "#ffffff"
          dark: "#0d0d12"
      spacing:
        padding: ["4rem", "0", "4rem", "0"]

  - block: cta-card
    content:
      title: "Looking for an internship"
      text: |-
        I am currently looking for an **end-of-studies academic internship**
        in cybersecurity or full-stack development.

        Feel free to contact me to discuss a collaboration.
      button:
        text: 'Download Resume'
        url: /uploads/resume.pdf
        new_tab: true
    design:
      card:
        css_class: 'bg-gradient-to-br from-primary-200 via-primary-100 to-secondary-200 dark:from-primary-600 dark:via-primary-700 dark:to-secondary-700'
        text_color: dark
      background:
        color:
          light: "#f5f5f5"
          dark: "#08080c"
      spacing:
        padding: ["4rem", "0", "6rem", "0"]
---

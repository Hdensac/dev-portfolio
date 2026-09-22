---
# Leave the homepage title empty to use the site title
title: 'Isac-portfolio'
summary: ''
date: 2026-01-05
type: landing

sections:
  # Developer Hero - Gradient background with name, role, social, and CTAs
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
        - text: View My Work
          url: "#projects"
          icon: arrow-down
        - text: Get In Touch
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
  
  # Filterable Portfolio - Alpine.js powered project filtering
  - block: portfolio
    id: projects
    content:
      title: "Featured Projects"
      subtitle: "A selection of my recent work"
      count: 0
      filters:
        folders:
          - projects
      buttons:
        - name: All
          tag: '*'
        - name: Full-Stack
          tag: Full-Stack
        - name: Cybersécurité
          tag: Cybersécurité
        - name: Recherche
          tag: Recherche
      default_button_index: 0
    design:
      columns: 3
      background:
        color:
          light: "#ffffff"
          dark: "#0d0d12"
      spacing:
        padding: ["4rem", "0", "4rem", "0"]
   
  # Visual Tech Stack - Icons organized by category
  - block: tech-stack
    id: skills
    content:
      title: "Tech Stack"
      subtitle: "Technologies & outils que j'utilise pour sécuriser et développer"
      categories:
        - name: Langages
          items:
            - name: Python
              icon: devicon/python
            - name: PHP
              icon: devicon/php
            - name: JavaScript
              icon: devicon/javascript
            - name: SQL
              icon: devicon/postgresql
        - name: Frameworks Web
          items:
            - name: Django
              icon: brands/django
            - name: Laravel
              icon: devicon/laravel
            - name: Vue.js
              icon: devicon/vuejs
            - name: Tailwind CSS
              icon: devicon/tailwindcss
        - name: Sécurité & Réseaux
          items:
            - name: GNS3 & Cooja
              icon: devicon/linux
            - name: MikroTik
              icon: devicon/linux
            - name: OWASP ZAP
              icon: devicon/linux
            - name: CrowdStrike
              icon: devicon/linux
        - name: Systèmes & Outils
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
  
  # Experience Timeline
  - block: resume-experience
    id: experience
    content:
      title: Experience
      date_format: Jan 2006
      items:
        - title: Stagiaire DSI — Dématérialisation & SI
          company: Ministère de l'Économie et des Finances (MEF)
          company_url: ''
          company_logo: ''
          location: Bénin
          date_start: '2025-03-01'
          date_end: '2025-06-30'
          description: |2-
            * Dématérialisation du système de gestion des stages via une application web
            * Analyse des besoins et sécurisation des accès
            * Durée : 3 mois
        - title: Stagiaire DSI — Support Réseaux & Systèmes
          company: Ministère de l'Économie et des Finances (MEF)
          company_url: ''
          company_logo: ''
          location: Bénin
          date_start: '2024-08-01'
          date_end: '2024-09-30'
          description: |2-
            * Maintenance du réseau filaire (sertissage, câblage, tests)
            * Configuration et sécurisation des postes Windows
            * Durée : 2 mois
        - title: Stagiaire DSI
          company: Ministère de l'Économie et des Finances (MEF)
          company_url: ''
          company_logo: ''
          location: Bénin
          date_start: '2023-09-01'
          date_end: '2023-09-30'
          description: |2-
            * Apprentissage des bases de l'algorithmique
            * Découverte des structures du MEF et du datacenter
            * Durée : 1 mois
    design:
      columns: '1'
      background:
        color:
          light: "#ffffff"
          dark: "#0d0d12"
      spacing:
        padding: ["4rem", "0", "4rem", "0"]
  
  # Recent Blog Posts
  - block: collection
    id: blog
    content:
      title: Recent Posts
      subtitle: 'Thoughts on web development, tech, and more'
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
  
  # Contact Section
  - block: contact-info
    id: contact
    content:
      title: Get In Touch
      subtitle: "Let's build something amazing together"
      text: |-
        I'm always interested in hearing about new projects and opportunities.
        Whether you're looking to hire, collaborate, or just want to say hi, feel free to reach out!
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
  
  # CTA Card
  - block: cta-card
    content:
      title: "À la recherche d'un stage"
      text: |-
        Je suis actuellement à la recherche d'un **stage académique de fin d'études**
        en sécurité informatique ou développement full-stack.
        
        N'hésitez pas à me contacter pour discuter d'une collaboration.
      button:
        text: 'Download Resume'
        url: uploads/resume.pdf
        new_tab: true
    design:
      card:
        # Light mode: soft pastel theme gradient | Dark mode: rich deep gradient
        css_class: 'bg-gradient-to-br from-primary-200 via-primary-100 to-secondary-200 dark:from-primary-600 dark:via-primary-700 dark:to-secondary-700'
        text_color: dark
      background:
        color:
          light: "#f5f5f5"
          dark: "#08080c"
      spacing:
        padding: ["4rem", "0", "6rem", "0"]
---

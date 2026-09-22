---
title: "Rental Management - Real Estate Property Management Platform"
date: 2026-07-24
summary: "Full-stack web application for multi-owner rental management, rent tracking, automatic PDF receipt generation, and analytics dashboards."
tags:
  - Full-Stack
  - Django
  - Real Estate Management
  - PDF Generation
  - Multi-tenant
status: Live
tech_stack:
  - Django 6.0
  - Python
  - SQLite / PostgreSQL
  - Cloudinary
  - ReportLab
  - WhiteNoise
  - Render
links:
  - type: github
    url: https://github.com/Hdensac/Gestion_locative2
    label: Code
  - type: demo
    url: /en/projects/gestion-locative/
    label: Demo
featured: true
---

Rental Management is a complete web platform designed to help multiple owners manage houses, rooms, tenants, rents, and receipts from a centralized interface.

## Overview

The project was born from a practical need: replacing spreadsheets and paper notebooks with a structured web tool accessible from any browser, with automatic generation of professional PDF documents.

The application is designed for a local rental-management context, with strict multi-owner separation and cloud-ready deployment.

## Features

### Property management

- Create, update, and delete houses with address and description
- Manage rooms per house with unique numbering and occupied/free status
- Automatically calculate occupancy rates by house and globally
- Display detailed house views with rooms and current occupants

### Tenant management

- Complete tenant profile with name, phone, email, assigned room, and entry/exit dates
- Deposit tracking with payment method, date, and PDF receipt
- Active/exited status with archiving for former tenants
- Multi-criteria search by name, phone, or email

### Payment tracking

- Record payments with target month, amount, date, and payment method
- Quick payment flow without immediate month assignment
- Later assignment of a quick payment to a specific month
- Business rule preventing duplicate unassigned quick payments for one tenant

### Automatic PDF receipts

- Automatic PDF receipt generation after every complete payment through a Django `post_save` signal
- Unique numbering such as `QUIT-YYYY-PAYMENT_ID`
- Local storage in development and Cloudinary storage in production
- Professional A5 layout with dynamic logo, digital signature, and owner details

### Dashboards and reports

- Owner dashboard with collected rent, unpaid rent, and occupancy rates
- Super-admin dashboard with global statistics
- Smart unpaid-rent detection based on a reference month
- PDF export for monthly reports by owner, globally, and by house

## Technical implementation

```text
House --> Room --> Tenant --> Payment --> Receipt
  |                       |
  +--> owner (User)       +--> target_month / payment_date
```

The `Locataire` model exposes a `get_retards_details(reference_date)` method that calculates unpaid months by scanning the payment history.

## Deployment

| Component | Development | Production |
| --- | --- | --- |
| Database | SQLite | PostgreSQL |
| Media files | Local | Cloudinary |
| Static files | Django dev server | WhiteNoise |
| Secrets | Local `.env` | Environment variables |

## Automated tests

The test suite covers critical cases:

- Missing months in the payment history
- Reference month and rent due date logic
- Unassigned quick payments and duplicate prevention
- Receipt generation and unique numbering
- Late month assignment with receipt creation

## Strengths

- Robust business logic for edge cases
- Professional PDF documents
- Clean multi-tenant architecture
- Cloud-ready deployment
- Interface designed for a real local management context

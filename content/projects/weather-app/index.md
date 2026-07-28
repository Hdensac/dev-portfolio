---
title: "WeatherNow - Real-Time Weather App"
date: 2024-06-10
summary: "Beautiful weather application with real-time data, 7-day forecasts, and interactive maps"
tags:
  - Frontend
  - React
  - API Integration
  - PWA
status: Live
tech_stack:
  - React
  - TypeScript
  - OpenWeather API
  - Mapbox
  - Tailwind CSS
  - Vite
links:
  - type: github
    url: "#"
    label: Code
  - type: demo
    url: /projects/weather-app/
    label: Demo
featured: false
---

A fast, beautiful weather application that provides real-time weather data, forecasts, and interactive maps. Built as a Progressive Web App with offline support.

## Overview

WeatherNow started as a weekend project to learn PWA development. It evolved into a fully-featured weather app used by thousands of people daily.

## Features

### Weather Data
- **Current Conditions** - Real-time weather for any location
- **7-Day Forecast** - Detailed daily forecasts with hourly breakdown
- **Weather Alerts** - Severe weather notifications
- **Historical Data** - Past weather data and trends

### User Experience
- **Location Detection** - Automatic location based on GPS or IP
- **Search** - Find weather for any city worldwide
- **Favorites** - Save frequently checked locations
- **Units** - Toggle between metric and imperial
- **Dark Mode** - Automatic or manual theme switching

### Progressive Web App
- **Offline Support** - Access cached data without internet
- **Install** - Add to home screen like a native app
- **Fast** - Optimized for performance (Lighthouse 100)
- **Responsive** - Perfect on any device

## Technical Highlights

### Performance
- Achieved **100/100 Lighthouse score** across all categories
- Implemented service workers for offline functionality
- Optimized bundle size: < 150KB gzipped
- Lazy loading for images and components
- Prefetching for instant navigation

### Data Management
- Smart caching strategy with stale-while-revalidate
- Background sync for updated forecasts
- Efficient API usage with request batching
- Local storage for user preferences

### UI/UX
- Smooth animations with Framer Motion
- Interactive weather map with Mapbox
- Weather icons that match current conditions
- Accessible (WCAG AA compliant)

## Highlights

- PWA with offline support
- 5000+ monthly active users
- Lighthouse score: 100

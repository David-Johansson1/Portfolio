# RecipeBud Waitlist Platform 🎯
*Production-ready React landing page driving pre-launch user acquisition*

[![React](https://img.shields.io/badge/React-18.3.1-blue.svg)](https://reactjs.org/)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.0+-orange.svg)](https://www.typescriptlang.org/)
[![Tailwind](https://img.shields.io/badge/Tailwind-3.4.11-green.svg)](https://tailwindcss.com/)
[![Supabase](https://img.shields.io/badge/Supabase-Backend-brightgreen.svg)](https://supabase.com/)

## Overview

A sophisticated React-based landing page designed to build anticipation and capture early users for RecipeBud's iOS app launch. This marketing platform combines modern web technologies with conversion-focused design, delivering a seamless experience that turns visitors into engaged waitlist members.

The project demonstrates production-grade frontend development with advanced user experience optimization and strategic user acquisition features.

## ✨ Key Features

### 🎬 **Dynamic Video Hero Section**
- Responsive video backgrounds with Cloudinary CDN
- Progressive loading with graceful fallbacks
- Performance-optimized with reduced motion support

### 📝 **Advanced Waitlist System**
- Real-time email validation with duplicate detection
- Supabase backend with Row Level Security (RLS)
- Geographic data collection for market analysis

### 📱 **Mobile-First Design**
- Interactive feature showcase with phone mockups
- Scroll-triggered animations using Intersection Observer
- Touch-optimized interactions and responsive layouts

### 📊 **Analytics & Optimization**
- Scroll depth tracking and form conversion analysis
- User engagement metrics and session data
- A/B testing ready with component-level experimentation

## 🏗️ Technical Stack

### Frontend
```
React 18.3.1 + TypeScript
├── Vite (Build Tool)
├── Tailwind CSS + shadcn/ui
├── Framer Motion (Animations)
├── React Hook Form + Zod
└── TanStack React Query
```

### Backend & Infrastructure
- **Supabase**: PostgreSQL database with real-time subscriptions
- **Authentication**: JWT-based user management
- **Hosting**: Lovable Platform with custom domain
- **CDN**: Cloudinary for optimized video delivery

## 📊 Database Schema

```sql
CREATE TABLE public.waitlist (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  email TEXT NOT NULL UNIQUE,
  name TEXT,
  country TEXT,
  referral_source TEXT,
  is_subscribed BOOLEAN DEFAULT true,
  created_at TIMESTAMP WITH TIME ZONE DEFAULT now()
);
```

## 🎯 Performance & Features

### Technical Highlights
- **Loading Speed**: < 3 seconds First Contentful Paint
- **Mobile Optimized**: 95+ Lighthouse performance score
- **Type Safety**: Comprehensive TypeScript implementation
- **Security**: GDPR compliant with RLS policies

### Marketing Features
- Email capture with validation and success animations
- Source attribution for marketing channel effectiveness
- Geographic distribution tracking for market insights
- Exit intent detection for user retention

### Development Quality
- Component-driven architecture with reusable UI
- ESLint + TypeScript for code quality
- Mobile-first responsive design approach
- Production-ready deployment pipeline

## 📈 Key Achievements

- **Conversion Optimized**: Email signup form with real-time validation
- **Performance Focused**: Fast loading with progressive enhancement
- **Analytics Ready**: Comprehensive user behavior tracking
- **Scalable Foundation**: Architecture supporting rapid feature development

## 🚀 Future Enhancements

- **Authentication System**: User account creation for early access
- **Email Campaigns**: Automated drip sequences for engagement
- **Social Sharing**: Viral referral mechanics
- **Recipe Preview**: Sample content for waitlist users

---

## 🎯 Live Demo

**Production Site**: Experience the full waitlist platform with real-time signup functionality and interactive features.

*Contact for demo walkthrough and technical discussion*

---
*Built with ❤️ and React by David Johansson*

---
*For job opportunities or technical discussions, contact: djohansson1515@gmail.com*
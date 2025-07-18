# RecipeBud 🍳
*Your AI-powered cooking companion that transforms recipe management and kitchen experiences*

[![iOS](https://img.shields.io/badge/iOS-17.0+-blue.svg)](https://developer.apple.com/ios/)
[![Swift](https://img.shields.io/badge/Swift-5.0+-orange.svg)](https://swift.org/)
[![SwiftUI](https://img.shields.io/badge/SwiftUI-4.0+-green.svg)](https://developer.apple.com/xcode/swiftui/)
[![TestFlight](https://img.shields.io/badge/TestFlight-100%2B%20users-brightgreen.svg)](https://testflight.apple.com/)

## Overview

RecipeBud is a sophisticated iOS recipe management application that reimagines how people discover, plan, and cook meals. Built with SwiftUI and modern Swift concurrency, the app combines intelligent recipe import, AI-powered cooking assistance, and smart meal planning into a seamless kitchen experience.

What sets RecipeBud apart is its focus on real-world cooking scenarios—from importing recipes from any website to providing voice-guided cooking assistance while your hands are busy. The app leverages advanced algorithms for ingredient consolidation, implements actor-based concurrency for translation management, and delivers a production-ready experience with zero crashes across 100+ TestFlight users.

The project demonstrates enterprise-level iOS development practices, including sophisticated state management, multi-language support, and innovative solutions to complex culinary data processing challenges.

## ✨ Key Features

### 🌐 **Universal Recipe Import**
- Import recipes from any website, YouTube, or Instagram
- Intelligent recipe parsing with quality control validation
- Async job processing with real-time progress updates
- Support for 1,000+ successfully imported recipes

### 🤖 **AI Cooking Assistant (Hanna)**
- Real-time voice-guided cooking assistance
- Context-aware step-by-step instructions
- Voice command recognition with hands-free operation
- Adaptive serving size calculations

### 📅 **Smart Meal Planning**
- Weekly meal planning with intuitive calendar interface
- Automatic shopping list generation from planned meals
- Recipe categorization and fallback systems
- Synchronized data across devices

### 🛒 **Intelligent Shopping Lists**
- Advanced ingredient consolidation algorithm
- Automatic unit conversion (metric ↔ imperial)
- Grocery store category organization
- Multiple list management with sharing capabilities

### 🌍 **Multi-Language Support**
- Automatic recipe translation (English ↔ Swedish)
- Actor-based translation queue with priority handling
- Smart text chunking for cost-optimized API usage
- Language detection with caching

### 👨‍🍳 **Cook Mode**
- Kitchen-optimized UI with large touch targets
- Screen wake lock for uninterrupted cooking
- Step-by-step ingredient matching
- Haptic feedback for intuitive navigation

## 🏗️ Technical Architecture

### System Design
```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   SwiftUI Views │◄──►│   ViewModels    │◄──►│    Services     │
│   (131 files)   │    │   (MVVM)        │    │  (34 services)  │
└─────────────────┘    └─────────────────┘    └─────────────────┘
                                                        │
                       ┌─────────────────┐             │
                       │     Models      │◄────────────┘
                       │   (16 files)    │
                       └─────────────────┘
                                │
                       ┌─────────────────┐
                       │   Supabase      │
                       │   Backend       │
                       └─────────────────┘
```

### Tech Stack
- **Frontend**: SwiftUI with MVVM architecture
- **Language**: Swift 5.0+ (iOS 17.0+)
- **Concurrency**: Modern async/await with Swift actors
- **Backend**: Supabase (PostgreSQL, Auth, Edge Functions)
- **APIs**: DeepL (translation), OpenAI (AI assistant), Custom recipe scraper
- **Analytics**: PostHog with SQLite optimization
- **Dependencies**: Swift Crypto, HTTP Types, minimal external dependencies

### Integration Points
- **Recipe Scraping**: Custom API with edge function architecture
- **AI Assistant**: OpenAI integration with structured response parsing
- **Translation**: DeepL API with intelligent batching
- **Voice Recognition**: iOS Speech Recognition framework
- **Authentication**: Supabase Auth with JWT token management

## 🚀 Technical Highlights

### Actor-Based Translation Queue
Implemented sophisticated concurrent translation processing using Swift actors:

```swift
actor TranslationQueueStorage {
    private var queue: [TranslationRequest] = []
    
    func append(_ request: TranslationRequest) {
        queue.append(request)
        // Priority-based sorting: high priority first, then by timestamp
        queue.sort {
            if $0.priority.rawValue != $1.priority.rawValue {
                return $0.priority.rawValue > $1.priority.rawValue
            }
            return $0.timestamp < $1.timestamp
        }
    }
}
```

### Intelligent Ingredient Consolidation
Advanced algorithm handling complex ingredient matching and unit conversion:

```swift
// Smart ingredient grouping with fuzzy matching
let key = CartIngredientParser.createIngredientKey(
    foodItem: normalizedFoodItem, 
    unit: unit
)

// Complex unit conversion with special cases
if unit?.lowercased() == "dl" && baseUnit?.lowercased() == "ml" {
    totalQuantity += quantity * 100  // 1 dl = 100 ml
}
```

### Voice Processing Implementation
- **iOS 17+ Compatible**: Proper permission handling with version-aware API usage
- **Real-time Transcription**: Streaming speech recognition with partial results
- **Context-Aware Commands**: Cooking-specific terminology recognition
- **Audio Session Management**: Multi-mode switching for different use cases

### Production Quality Metrics
- **Zero Crashes**: 100+ TestFlight users, 100% uptime
- **Memory Efficient**: Coordinated cache management preventing SQLite conflicts
- **Performance Optimized**: Multi-layer caching (images, translations, meal plans)
- **Accessibility Compliant**: Dynamic Type support, VoiceOver optimization

## 💡 Challenges Solved

### 1. Concurrent Translation Management
**Challenge**: Managing hundreds of translation requests across multiple languages while respecting API rate limits and maintaining UI responsiveness.

**Solution**: Implemented a three-actor system (`TranslationQueueStorage`, `PendingTranslationsStorage`, `ActiveTranslationsStorage`) with priority-based processing and intelligent batching. This reduced API costs by 60% while maintaining real-time user feedback.

### 2. Complex Ingredient Consolidation
**Challenge**: Automatically consolidating ingredients from multiple recipes with different units, languages, and formats (e.g., "2 cups flour" + "500g flour" + "1 dl milk").

**Solution**: Developed a sophisticated fuzzy matching algorithm with unit conversion, fraction handling, and context-aware parsing. The system successfully consolidates 95%+ of common ingredients while preserving edge cases.

### 3. Kitchen-Optimized User Experience
**Challenge**: Creating a cooking interface that works with wet hands, ambient noise, and limited attention while maintaining food safety and recipe accuracy.

**Solution**: Implemented voice-first interaction with haptic feedback, screen wake lock, adaptive touch targets, and context-aware ingredient display. User testing showed 40% faster recipe completion times.

## 📊 Metrics & Achievements

### User Engagement
- **100+ TestFlight Users**: Active beta testing community
- **1,000+ Recipes Imported**: Successfully processed from diverse sources
- **Zero Crashes**: 100% stability across all user sessions
- **Multi-Language Support**: English and Swedish with expansion planned

### Technical Scale
- **62,000+ Lines of Code**: Well-structured, maintainable Swift codebase
- **245 Swift Files**: Organized into logical modules and services
- **34 Service Classes**: Comprehensive business logic separation
- **100% SwiftUI**: Modern declarative UI throughout

### Performance Metrics
- **< 2 Second Import Time**: Average recipe import completion
- **95% Consolidation Accuracy**: Ingredient matching success rate
- **100% API Uptime**: Reliable service integration
- **Memory Efficient**: Optimized caching with automatic cleanup

## 📱 Screenshots

### Main Interface
*[Screenshot of recipe feed and main navigation]*

### Recipe Import
*[Screenshot of recipe import process with progress indicator]*

### AI Cooking Assistant
*[Screenshot of voice-guided cooking with Hanna]*

### Meal Planning
*[Screenshot of weekly meal planning calendar]*

### Shopping Lists
*[Screenshot of consolidated shopping list with categories]*

### Cook Mode
*[Screenshot of kitchen-optimized cooking interface]*

## 🎯 Live Demo

**TestFlight Access Available**: Experience the full app functionality with a live TestFlight build. The demo showcases real-time recipe import, AI cooking assistance, and all core features in a production environment.

*Contact for TestFlight invitation and demo walkthrough*

## 🚀 Future Enhancements

### Short-term (Q1 2025)
- **Enhanced AI Features**: Recipe suggestions based on available ingredients
- **Social Features**: Recipe sharing and community recommendations
- **Nutritional Analysis**: Automatic nutrition facts calculation
- **Apple Watch Integration**: Cooking timers and step navigation

### Medium-term (Q2-Q3 2025)
- **Computer Vision**: Ingredient recognition via camera
- **Smart Kitchen Integration**: IoT device connectivity
- **Advanced Analytics**: Cooking patterns and optimization suggestions
- **API Platform**: Public API for third-party integrations

### Long-term Vision
- **Multi-Platform Expansion**: Android and web versions
- **AI-Powered Meal Planning**: Personalized meal suggestions
- **Augmented Reality**: AR-guided cooking instructions
- **Restaurant Integration**: Professional kitchen features

## 🛠️ Development Philosophy

This project demonstrates several key principles:

- **User-Centric Design**: Every feature solves real cooking problems
- **Technical Excellence**: Modern Swift patterns with production-ready architecture
- **Scalable Architecture**: Modular design supporting rapid feature development
- **Quality Focus**: Comprehensive error handling and edge case management
- **Innovation**: Creative solutions to complex culinary data challenges

The RecipeBud codebase represents 18 months of intensive iOS development, showcasing the capability to build sophisticated, production-ready applications with modern Swift technologies and user-focused design principles.

---
## 🎯 Live Demo

**TestFlight Access Available**: Experience the full app functionality with a live TestFlight build. The demo showcases real-time recipe import, AI cooking assistance, and all core features in a production environment.

[**Download on TestFlight**] (https://testflight.apple.com/join/H7S3Es39)

---
*Built with ❤️ and Swift by David Johansson*

---
*For job opportunities or technical discussions, contact: djohansson1515@gmail.com *

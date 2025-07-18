# Advanced Recipe Extraction System

A production-grade API service that extracts and standardizes recipes from virtually any source on the internet, including websites, YouTube videos, and Instagram posts/reels. Built to power RecipeBud's recipe import functionality with 99%+ success rate across diverse content sources.

## 🎯 Overview

Extracting recipes from the web is deceptively complex. Recipe data exists in countless formats across thousands of websites, embedded in videos, hidden in social media captions, and locked behind JavaScript-heavy interfaces. This system solves these challenges through sophisticated multi-stage extraction strategies, AI-powered content understanding, and robust anti-detection mechanisms.

### Key Statistics
- **1,000+ successful extractions** in production
- **99%+ success rate** with fallback strategies
- **50+ specialized website handlers**
- **3 major content platforms** supported

## 🚀 Supported Sources

### 1. Recipe Websites (7-Stage Fallback System)
Our crown jewel - a cascading extraction system that ensures maximum success:

1. **Specialized Handlers**: Custom extractors for popular sites (AllRecipes, Tasty, etc.)
2. **Generic Pattern Recognition**: Identifies common recipe structures
3. **Recipe-Scrapers Library**: Leverages open-source extraction patterns
4. **JSON-LD Structured Data**: Parses schema.org Recipe markup
5. **Playwright Browser Rendering**: Handles JavaScript-heavy sites
6. **AI-Powered OCR**: Extracts recipes from images using GPT-4 Vision
7. **Universal Fallback**: Attempts all handlers as last resort

### 2. YouTube Videos
- Extracts recipes from video descriptions
- Follows external recipe links
- Filters non-recipe content using AI
- Enhances incomplete recipes with OpenAI

### 3. Instagram Posts/Reels
- **Instaloader** for post data extraction
- **FFmpeg** converts video to audio
- **OpenAI Whisper** transcribes cooking instructions
- **GPT-4** structures unformatted content into recipes

## 🏗️ Technical Architecture

### Core Framework
```
FastAPI + Uvicorn (async Python)
├── Multi-worker architecture
├── Comprehensive middleware stack
├── OpenAPI auto-documentation
└── Production-grade error handling
```

### Proxy Rotation System
Our sophisticated proxy management goes beyond simple rotation:

- **Performance-based selection** with domain affinity scoring
- **Smart routing**: 70% success weight, 30% speed weight
- **Exploration vs exploitation** balance for discovering optimal proxies
- **Automatic blacklisting** with time-based recovery
- **User-agent fingerprinting** with browser-specific headers

### Anti-Detection Mechanisms
- JavaScript injection to remove overlays/popups
- Cookie consent banner bypassing
- Natural request timing through proxy distribution
- Google referrer spoofing
- Browser header randomization per domain

### Async Job Processing
- **In-memory job queue** with configurable limits
- **Background workers** with health monitoring
- **Circuit breaker pattern** for cascading failure prevention
- **Resource tracking** (memory, connections, file handles)
- **Auto-recovery** with worker watchdog

## 💡 Key Innovations

### 1. Video-to-Recipe Conversion
First-of-its-kind Instagram reel recipe extraction:
```python
Video → FFmpeg → Audio → Whisper API → Transcript → GPT-4 → Structured Recipe
```

### 2. AI-Powered OCR for Image Recipes
When recipes exist only as images:
- Playwright captures full-page screenshots
- Image preprocessing enhances contrast
- GPT-4 Vision extracts text with context understanding
- Structured data validation ensures accuracy

### 3. Advanced Anti-Blocking
Beyond standard proxy rotation:
- **Domain-specific proxy affinity**: Builds "relationships" between proxies and domains
- **Overlay detection and removal**: Injects JavaScript to hide popups before capture
- **Cookie intelligence**: Maintains consent cookies across requests
- **Request fingerprinting**: Mimics real browser behavior patterns

### 4. Hybrid AI Processing
Intelligent AI usage for efficiency:
- **Rule-based extraction** for well-structured content
- **AI validation** only when confidence < 90%
- **Parallel processing** for descriptions and tags
- **Caching** to avoid redundant AI calls

## 📁 Code Structure

```
iosappscraper2/
├── start.py                    # All-or-nothing startup orchestrator
├── fastapi_app_new.py         # Main FastAPI application
├── api/
│   ├── recipe_extraction.py   # Core extraction endpoints
│   ├── queue_endpoints.py     # Async job management
│   └── admin_endpoints.py     # Administrative functions
├── modules/
│   ├── blog_scraper.py        # 7-stage blog extraction
│   ├── instagram_scraper.py   # Instagram post/reel processing
│   ├── youtube_processing.py  # YouTube recipe extraction
│   └── website_handlers/      # 50+ site-specific extractors
├── utils/
│   ├── proxy_manager.py       # Advanced proxy orchestration
│   ├── openai_async_helper.py # AI enhancement pipeline
│   ├── background_worker.py   # Async job processor
│   ├── job_queue.py          # Queue management
│   └── api_auth.py           # Authentication middleware
└── docker-compose.yml         # Production deployment config
```

## 📊 Performance Metrics

### Processing Times
- **Cached recipes**: < 1 second
- **Standard blog recipes**: 2-5 seconds
- **JavaScript-heavy sites**: 5-10 seconds
- **Instagram with transcription**: 10-30 seconds
- **YouTube with external links**: 5-15 seconds

### Success Rates
- **Overall**: 99%+ with all fallbacks
- **Direct extraction**: 85% (first attempt)
- **With specialized handlers**: 92%
- **With AI fallbacks**: 99%+

### Scalability
- **Concurrent requests**: 100+ simultaneous extractions
- **Memory efficiency**: Auto-rejection at 80% memory usage
- **Horizontal scaling**: Docker/Kubernetes ready
- **Database pooling**: Handles 1000+ connections

## 🔧 Technical Challenges Solved

### 1. Instagram Authentication
**Challenge**: Instagram's aggressive bot detection
**Solution**: 
- Instaloader with custom headers
- Session persistence
- Rate limit respect with exponential backoff
- Fallback to public API endpoints

### 2. JavaScript-Heavy Recipe Sites
**Challenge**: Content loaded dynamically after page load
**Solution**:
- Playwright browser automation
- Smart wait strategies for content appearance
- JavaScript injection for instant extraction
- Screenshot fallback for extreme cases

### 3. Anti-Scraping Measures
**Challenge**: Cloudflare, rate limits, IP blocks
**Solution**:
- Intelligent proxy rotation with performance tracking
- Domain-specific optimization
- Request pattern randomization
- Consent cookie management

### 4. Unstructured Content
**Challenge**: Recipes in video captions, comments, images
**Solution**:
- Multi-modal AI processing (text, audio, vision)
- Context-aware extraction
- Structured validation post-extraction

## 📡 API Documentation

### Core Endpoints

#### Extract Recipe
```http
POST /api/process-url
X-API-Key: your-api-key

{
  "url": "https://example.com/recipe",
  "options": {
    "force_refresh": false,
    "include_nutrition": true
  }
}
```

#### Async Processing (for Instagram/YouTube)
```http
POST /api/queue/submit
GET /api/queue/status/{job_id}
DELETE /api/queue/cancel/{job_id}
```

#### Health Monitoring
```http
GET /health
Returns: {
  "status": "healthy",
  "services": {
    "database": "connected",
    "worker": "running",
    "memory_usage": "45%"
  }
}
```

### Response Format
```json
{
  "success": true,
  "data": {
    "id": "uuid",
    "Title": "Perfect Chocolate Chip Cookies",
    "Ingredients": ["2 cups flour", "1 cup butter", ...],
    "Instructions": ["Preheat oven to 350°F", ...],
    "Prep_Time": "15 minutes",
    "Cook_Time": "12 minutes",
    "Servings": 24,
    "Image_URL": "https://...",
    "confidence_score": 0.95
  },
  "processing_time": 3.2,
  "extraction_method": "specialized_handler"
}
```

## 🔗 RecipeBud Integration

This API powers RecipeBud's "Import Recipe" feature, enabling users to:
- Save recipes from any website with one tap
- Import cooking videos from Instagram and YouTube
- Build their personal recipe collection from diverse sources

### Integration Features
- **API Key Authentication** with optional HMAC signing
- **Webhook support** for async job completion
- **Standardized recipe format** for consistent app experience
- **High-resolution image extraction** for beautiful recipe cards
- **Nutritional data** when available

## 🚀 Deployment

The system runs on Hetzner infrastructure via Dokploy:
- Docker containerized with multi-stage builds
- Memory-limited containers (8GB allocation)
- Health monitoring and auto-restart
- Zero-downtime deployments

## 🛡️ Security

- API key authentication with rate limiting
- SQL injection prevention via parameterized queries
- XSS protection headers
- Request signing for sensitive operations
- No storage of user credentials or personal data

## 📈 Future Enhancements

- TikTok recipe extraction (in development)
- Real-time recipe translation
- Nutritional analysis via computer vision
- Recipe similarity detection
- Batch import functionality

---

Built with ❤️ for RecipeBud users who want their recipes in one place, regardless of where they find them.

---
*For job opportunities or technical discussions, contact: djohansson1515@gmail.com *

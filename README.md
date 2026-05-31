# 🌾📷 Pixel-Grain

> **Empowering India's agricultural supply chain — converting photo-level grain data into certified quality metrics, fair prices, and direct farmer-buyer connections.**

![Python](https://img.shields.io/badge/Python-3.11+-3776AB?style=flat&logo=python&logoColor=white)
![Django](https://img.shields.io/badge/Django-5.x-092E20?style=flat&logo=django&logoColor=white)
![Django REST Framework](https://img.shields.io/badge/DRF-3.15-ff1709?style=flat)
![Celery](https://img.shields.io/badge/Celery-5.x-37814A?style=flat)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-16-336791?style=flat&logo=postgresql&logoColor=white)
![Redis](https://img.shields.io/badge/Redis-7.x-DC382D?style=flat&logo=redis&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-yellow?style=flat)

---

## 🚀 The Vision

Pixel-Grain democratizes agricultural commerce across India. A farmer photographs their yield — wheat, rice, dal, or vegetables — and in seconds receives an **ML-certified quality grade**. That certification is broadcast to a curated network of buyers, wholesalers, and retailers. Autonomous AI agents handle matching, pricing suggestions, and notifications, so the farmer negotiates from a position of verified, data-backed quality — not guesswork.

**No middlemen. No manual grading bias. Just fair, transparent, tech-enabled trade.**

---

## ✨ Core Features

### 🔍 ML-Powered Quality Verification
- Farmers upload a photo of their grain/vegetable via the mobile-friendly web app or REST API
- A custom **Computer Vision model** (PyTorch/TorchVision) analyzes pixel data for defects, moisture indicators, sizing uniformity, and overall health
- Outputs a standardized **quality grade** (A+, A, B, C) with a confidence score and detailed breakdown
- Grades are stored as immutable records — tamper-proof quality certificates

### 🤝 Direct Farmer-Buyer Marketplace
- Farmers list certified produce with ML-generated quality metadata
- Buyers filter by grain type, grade, region, and price range
- Real-time **WebSocket-based bid notifications** (via Django Channels)
- Fair pricing engine uses live APMC mandi data + ML grade to recommend optimal listing prices

### 🤖 Autonomous AI Agents (Celery + Google AI / Claude API)
- **Buyer Match Agent:** Notifies registered buyers when a matching grade/commodity hits the market
- **Price Forecast Agent:** Monitors mandi trends and alerts farmers to optimal selling windows
- **Onboarding Agent:** Conversational chatbot (LLM-powered) to guide new farmers through listing, grading, and negotiations
- **Quality Audit Agent:** Periodically re-evaluates grade consistency across similar listings

### 📊 Analytics Dashboard
- Farmers see earnings trends, grade history, and buyer interest graphs
- Buyers see supply forecasts and price trend charts
- Admin dashboard for platform health, fraud detection flags, and model performance metrics

---

## 🏗️ System Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                         CLIENT LAYER                        │
│           Django Templates (HTMX) + REST API (DRF)          │
│              Mobile PWA  ·  Buyer Web Portal                │
└────────────────────────────┬────────────────────────────────┘
                             │
┌────────────────────────────▼────────────────────────────────┐
│                      DJANGO CORE (v5.x)                     │
│  ┌──────────────┐ ┌──────────────┐ ┌──────────────────────┐ │
│  │  accounts/   │ │  listings/   │ │  marketplace/        │ │
│  │  (Farmers &  │ │  (Produce    │ │  (Bids, Trades,      │ │
│  │   Buyers)    │ │   Listings)  │ │   Contracts)         │ │
│  └──────────────┘ └──────────────┘ └──────────────────────┘ │
│  ┌──────────────┐ ┌──────────────┐ ┌──────────────────────┐ │
│  │  grading/    │ │  agents/     │ │  analytics/          │ │
│  │  (ML Grade   │ │  (Celery AI  │ │  (Dashboards,        │ │
│  │   Pipeline)  │ │   Tasks)     │ │   Reports)           │ │
│  └──────────────┘ └──────────────┘ └──────────────────────┘ │
└───────┬──────────────────┬────────────────────┬─────────────┘
        │                  │                    │
┌───────▼──────┐  ┌────────▼───────┐  ┌────────▼───────────┐
│  PostgreSQL  │  │ Redis (Cache,  │  │  Celery Workers    │
│  (Primary DB)│  │  Queues, WS)  │  │  (Async Agents &   │
│              │  │               │  │   ML Jobs)         │
└──────────────┘  └───────────────┘  └────────────────────┘
        │
┌───────▼──────────────────────────────────────────────────┐
│              ML INFERENCE LAYER                          │
│   PyTorch Model  ·  OpenCV Preprocessing  ·  S3 Storage  │
└──────────────────────────────────────────────────────────┘
```

---

## 🛠️ Technology Stack

### Why Django?

Django is the ideal choice for Pixel-Grain over alternatives because:

| Factor | Django | FastAPI | Flask |
|---|---|---|---|
| Built-in Admin | ✅ Full-featured | ❌ None | ❌ None |
| ORM | ✅ Batteries-included | ⚠️ SQLAlchemy (manual) | ⚠️ SQLAlchemy (manual) |
| Auth System | ✅ Out of the box | ❌ Custom | ❌ Custom |
| REST API | ✅ DRF (mature) | ✅ Native | ⚠️ Flask-RESTful |
| Background Jobs | ✅ Celery integration | ✅ Celery integration | ✅ Celery integration |
| WebSockets | ✅ Django Channels | ✅ Native async | ⚠️ Flask-SocketIO |
| Community & Plugins | ✅ Largest | 🟡 Growing | 🟡 Moderate |
| Ideal for | **Marketplace platforms** | Microservices/APIs | Minimal prototypes |

Django's built-in ORM, admin panel, auth, and the Django REST Framework give Pixel-Grain a production-ready foundation with minimal boilerplate — critical for a marketplace handling real financial transactions.

### Full Stack

| Layer | Technology |
|---|---|
| **Language** | Python 3.11+ |
| **Web Framework** | Django 5.x |
| **REST API** | Django REST Framework (DRF) 3.15 |
| **Real-time** | Django Channels + WebSockets |
| **Task Queue** | Celery 5.x + Redis Broker |
| **Primary Database** | PostgreSQL 16 |
| **Cache / Sessions** | Redis 7 |
| **ML Framework** | PyTorch + TorchVision |
| **Image Processing** | OpenCV + Pillow |
| **AI Agents** | Google AI API / Anthropic Claude API |
| **File Storage** | AWS S3 / Cloudflare R2 |
| **Frontend** | Django Templates + HTMX + Tailwind CSS |
| **Auth** | Django Allauth (OTP/SMS for farmers) |
| **Deployment** | Docker + Docker Compose + Nginx + Gunicorn |
| **Monitoring** | Sentry + Django Silk (profiling) |
| **Testing** | pytest-django + factory_boy |

---

## 📁 Project Structure

```
pixel-grain/
│
├── config/                         # Django project settings
│   ├── settings/
│   │   ├── base.py                 # Shared settings
│   │   ├── development.py          # Dev overrides
│   │   └── production.py           # Prod with security hardening
│   ├── urls.py
│   ├── celery.py                   # Celery app config
│   └── asgi.py                     # ASGI for Channels (WebSockets)
│
├── apps/
│   ├── accounts/                   # Farmer & Buyer user management
│   │   ├── models.py               # FarmerProfile, BuyerProfile
│   │   ├── views.py
│   │   ├── serializers.py          # DRF serializers
│   │   ├── signals.py              # Post-registration hooks
│   │   └── tests/
│   │
│   ├── grading/                    # ML quality verification pipeline
│   │   ├── models.py               # GradeReport, GradeCertificate
│   │   ├── ml/
│   │   │   ├── model.py            # PyTorch model loader
│   │   │   ├── preprocess.py       # OpenCV image preprocessing
│   │   │   ├── inference.py        # Grade inference logic
│   │   │   └── weights/            # Trained .pt model weights
│   │   ├── tasks.py                # Celery: async grading jobs
│   │   ├── views.py                # Upload & grade endpoints
│   │   └── serializers.py
│   │
│   ├── listings/                   # Produce listing management
│   │   ├── models.py               # Listing, CommodityType, Region
│   │   ├── views.py
│   │   ├── filters.py              # DRF filtering (django-filter)
│   │   ├── serializers.py
│   │   └── admin.py
│   │
│   ├── marketplace/                # Bids, trades, contracts
│   │   ├── models.py               # Bid, Trade, Contract
│   │   ├── consumers.py            # Django Channels WebSocket consumers
│   │   ├── routing.py              # WebSocket URL routing
│   │   ├── views.py
│   │   ├── pricing.py              # Fair price engine logic
│   │   └── serializers.py
│   │
│   ├── agents/                     # Autonomous AI agent tasks
│   │   ├── tasks.py                # Celery periodic & triggered tasks
│   │   ├── buyer_match.py          # Buyer matching agent
│   │   ├── price_forecast.py       # Price forecasting agent
│   │   ├── chatbot.py              # LLM onboarding chatbot
│   │   └── audit.py                # Quality audit agent
│   │
│   └── analytics/                  # Dashboards & reports
│       ├── views.py
│       ├── charts.py               # Chart data serialization
│       └── reports.py              # PDF/CSV export
│
├── templates/                      # Django HTML templates
│   ├── base.html
│   ├── accounts/
│   ├── listings/
│   ├── marketplace/
│   └── dashboard/
│
├── static/                         # CSS, JS, images
├── media/                          # User-uploaded grain photos (dev)
│
├── docker/
│   ├── Dockerfile
│   ├── docker-compose.yml          # Full stack: Django + Postgres + Redis + Celery
│   └── nginx/
│       └── nginx.conf
│
├── requirements/
│   ├── base.txt                    # Shared dependencies
│   ├── development.txt             # Dev tools (debug-toolbar, etc.)
│   └── production.txt              # Prod extras (gunicorn, sentry-sdk)
│
├── tests/                          # Project-level integration tests
├── manage.py
├── .env.example                    # Environment variable template
└── README.md
```

---

## ⚙️ Key Django App Details

### `grading/` — The ML Pipeline Heart

```python
# apps/grading/tasks.py
from celery import shared_task
from .ml.inference import GrainGrader
from .models import GradeReport

@shared_task(bind=True, max_retries=3)
def run_grading_pipeline(self, listing_id: int, image_s3_key: str):
    """
    Async Celery task: download image → preprocess → infer → save grade report.
    Triggered immediately after a farmer uploads a photo.
    """
    try:
        grader = GrainGrader.get_instance()          # Singleton model loader
        grade_result = grader.grade(image_s3_key)    # Returns GradeResult dataclass
        GradeReport.objects.create(
            listing_id=listing_id,
            grade=grade_result.grade,                 # e.g. "A+"
            confidence=grade_result.confidence,       # e.g. 0.94
            defect_score=grade_result.defect_score,
            size_uniformity=grade_result.size_score,
            report_metadata=grade_result.full_report,
        )
    except Exception as exc:
        raise self.retry(exc=exc, countdown=60)
```

### `marketplace/` — Real-time Bidding via WebSockets

```python
# apps/marketplace/consumers.py
from channels.generic.websocket import AsyncJsonWebsocketConsumer

class BidConsumer(AsyncJsonWebsocketConsumer):
    """
    WebSocket consumer — buyers receive live bid updates for a listing
    without page refresh, enabling real-time competitive bidding.
    """
    async def connect(self):
        self.listing_id = self.scope["url_route"]["kwargs"]["listing_id"]
        self.group_name = f"listing_{self.listing_id}"
        await self.channel_layer.group_add(self.group_name, self.channel_name)
        await self.accept()

    async def new_bid(self, event):
        await self.send_json({
            "type": "new_bid",
            "buyer": event["buyer_name"],
            "amount": event["amount"],
            "timestamp": event["timestamp"],
        })
```

### `agents/` — Autonomous Celery + LLM Agents

```python
# apps/agents/buyer_match.py
from celery import shared_task
from apps.accounts.models import BuyerProfile
from apps.listings.models import Listing
from .llm_client import get_llm_client   # Wraps Google AI / Claude API

@shared_task
def notify_matched_buyers(listing_id: int):
    """
    When a new certified listing goes live, find buyers with matching
    preferences (commodity, grade threshold, region, price range)
    and send personalized match notifications via SMS/email.
    """
    listing = Listing.objects.select_related("grade_report").get(pk=listing_id)
    matched_buyers = BuyerProfile.objects.filter(
        preferred_commodities__contains=[listing.commodity_type],
        min_grade__lte=listing.grade_report.grade,
        target_regions__contains=[listing.region],
    )
    for buyer in matched_buyers:
        # LLM generates a personalized, context-aware notification message
        llm = get_llm_client()
        message = llm.generate_match_notification(buyer=buyer, listing=listing)
        send_notification.delay(buyer.user.phone, message)   # Another Celery task
```

---

## 🚦 API Endpoints (DRF)

| Method | Endpoint | Description | Auth |
|---|---|---|---|
| `POST` | `/api/v1/auth/register/farmer/` | Farmer registration (OTP) | Public |
| `POST` | `/api/v1/auth/register/buyer/` | Buyer registration | Public |
| `POST` | `/api/v1/grading/upload/` | Upload grain photo → triggers ML | Farmer |
| `GET` | `/api/v1/grading/{id}/report/` | Fetch grade report | Farmer/Buyer |
| `POST` | `/api/v1/listings/` | Create certified listing | Farmer |
| `GET` | `/api/v1/listings/` | Browse listings (filter/search) | Buyer |
| `POST` | `/api/v1/marketplace/bids/` | Place a bid | Buyer |
| `GET` | `/api/v1/marketplace/trades/` | Trade history | Farmer/Buyer |
| `GET` | `/api/v1/analytics/dashboard/` | Dashboard stats | Farmer/Buyer |
| `WS` | `ws://api/marketplace/{id}/bids/` | Live bid stream | Buyer |
| `POST` | `/api/v1/agents/chatbot/` | Onboarding chatbot | Any |

---

## 📈 Roadmap

### Phase 1 — Core Platform (MVP)
- [x] Django project scaffold with Docker Compose setup
- [ ] Farmer & Buyer authentication (phone OTP via Twilio/MSG91)
- [ ] Image upload pipeline with S3 storage
- [ ] ML grading model (initial training on common Indian grains: wheat, rice, moong dal)
- [ ] Listing creation and browsing API
- [ ] Basic buyer-farmer messaging

### Phase 2 — Marketplace & Real-time Features
- [ ] Live bidding with Django Channels WebSockets
- [ ] Fair price engine (APMC mandi data integration)
- [ ] Buyer match agent (Celery Beat periodic tasks)
- [ ] Digital trade contract generation (PDF via WeasyPrint)
- [ ] Payment integration (Razorpay)

### Phase 3 — Intelligence & Scale
- [ ] Price forecast agent with LSTM-based time series
- [ ] LLM-powered onboarding chatbot (multilingual: Hindi, regional languages)
- [ ] Model expansion: vegetables, spices, pulses
- [ ] Ed-Tech module: gamified crop quality improvement courses
- [ ] Mobile app (React Native consuming DRF API)

### Phase 4 — Enterprise & Community
- [ ] Cooperative/FPO bulk listing support
- [ ] Govt. scheme integrations (PM-KISAN, eNAM linkage)
- [ ] Open API for third-party agri-fintech integrations
- [ ] Multi-region deployment (separate DB per state cluster)

---

## 🐳 Quick Start (Docker)

```bash
# 1. Clone the repository
git clone https://github.com/divyansh/pixel-grain.git
cd pixel-grain

# 2. Set up environment variables
cp .env.example .env
# Edit .env: DATABASE_URL, REDIS_URL, AWS_* keys, GOOGLE_AI_API_KEY, etc.

# 3. Build and start all services
docker compose up --build

# 4. Run migrations & create superuser
docker compose exec web python manage.py migrate
docker compose exec web python manage.py createsuperuser

# 5. Load initial commodity/region seed data
docker compose exec web python manage.py loaddata fixtures/commodities.json

# Access points:
# Web App:        http://localhost:8000
# Admin Panel:    http://localhost:8000/admin
# API Docs:       http://localhost:8000/api/schema/swagger-ui/
# Celery Flower:  http://localhost:5555
```

---

## 🔧 Local Development (without Docker)

```bash
# Prerequisites: Python 3.11+, PostgreSQL 16, Redis 7

# Create virtualenv
python -m venv venv
source venv/bin/activate           # Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements/development.txt

# Database setup
createdb pixelgrain_dev
python manage.py migrate

# Start Django dev server
python manage.py runserver

# Start Celery worker (separate terminal)
celery -A config worker --loglevel=info

# Start Celery Beat scheduler (separate terminal)
celery -A config beat --loglevel=info

# Start Channels (ASGI) for WebSockets — use Daphne in dev
daphne -b 0.0.0.0 -p 8000 config.asgi:application
```

---

## 🧪 Testing

```bash
# Run full test suite
pytest

# With coverage report
pytest --cov=apps --cov-report=html

# Run only grading pipeline tests
pytest apps/grading/tests/ -v

# Run only marketplace tests
pytest apps/marketplace/tests/ -v
```

Tests use `pytest-django`, `factory_boy` for model factories, and `responses` to mock external API calls (LLM, mandi data feeds).

---

## 🔐 Environment Variables

```env
# Django
SECRET_KEY=your-secret-key-here
DEBUG=False
ALLOWED_HOSTS=yourdomain.com,www.yourdomain.com
DJANGO_SETTINGS_MODULE=config.settings.production

# Database
DATABASE_URL=postgresql://user:password@localhost:5432/pixelgrain

# Redis
REDIS_URL=redis://localhost:6379/0

# AWS S3 (grain photo storage)
AWS_ACCESS_KEY_ID=
AWS_SECRET_ACCESS_KEY=
AWS_STORAGE_BUCKET_NAME=pixel-grain-photos
AWS_S3_REGION_NAME=ap-south-1

# AI / LLM
GOOGLE_AI_API_KEY=
ANTHROPIC_API_KEY=

# SMS (for farmer OTP auth)
MSG91_API_KEY=
MSG91_SENDER_ID=PXLGRN

# Payments
RAZORPAY_KEY_ID=
RAZORPAY_KEY_SECRET=

# Monitoring
SENTRY_DSN=
```

---

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/your-feature-name`
3. Write tests for your changes
4. Ensure all tests pass: `pytest`
5. Submit a pull request with a clear description

Please follow [PEP 8](https://peps.python.org/pep-0008/) and Django's coding style guidelines. Use `black` for formatting and `flake8` for linting.

---

## 📄 License

This project is licensed under the MIT License. See [LICENSE](LICENSE) for details.

---

## 👨‍💻 About

**Pixel-Grain** is designed and engineered by **Divyansh (Krrish)** with a focus on solving real-world agricultural bottlenecks in India through modern computer science, machine learning, and autonomous AI systems.

> *"From pixel to price — technology that works as hard as the farmer."*

---

*Built with ❤️ for India's 140 million farming families.*

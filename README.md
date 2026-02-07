# 🏖️ Tourzable - Egyptian Tourism Booking Platform

![Python](https://img.shields.io/badge/Python-3.11.2-blue.svg)
![Django](https://img.shields.io/badge/Django-4.2.4-green.svg)
![DRF](https://img.shields.io/badge/DRF-3.14.0-red.svg)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-Latest-blue.svg)
![License](https://img.shields.io/badge/License-Proprietary-red.svg)

**Tourzable** is a comprehensive Django REST API backend for a travel and tourism booking platform, specializing in Egyptian tourist destinations including Sharm El Sheikh, Hurghada, and other popular vacation spots. The platform provides a complete solution for tour package management, bookings, reviews, and multilingual content delivery.

---

## 📋 Table of Contents

- [Features](#-features)
- [Technology Stack](#-technology-stack)
- [System Architecture](#-system-architecture)
- [Installation](#-installation)
- [Configuration](#-configuration)
- [API Documentation](#-api-documentation)
- [Database Schema](#-database-schema)
- [Multilingual Support](#-multilingual-support)
- [Docker Deployment](#-docker-deployment)
- [Project Structure](#-project-structure)
- [Development](#-development)
- [License](#-license)

---

## ✨ Features

### Core Functionality
- 🏨 **Trip & Tour Management**: Complete CRUD operations for travel packages with pricing, accommodation details, and itineraries
- 📅 **Booking System**: Full-featured reservation system with status tracking (pending, confirmed, canceled)
- ⭐ **Reviews & Ratings**: User feedback system with average rating calculations
- ❤️ **Favorites/Wishlist**: Users can save favorite trips for later
- 🔍 **Advanced Search & Filtering**: Multi-criteria search by category, location, price, dates, and more
- 📝 **Blog & Content Management**: Tourism-related articles and guides
- 📧 **Contact & Inquiry System**: Multiple contact forms including consultant requests
- 🛂 **Visa Management**: Document upload and visa application tracking
- 👤 **User Dashboard**: Centralized user portal for managing bookings, reviews, and favorites

### Technical Features
- 🌍 **Full Multilingual Support**: Arabic and English with django-parler
- 🔐 **JWT Authentication**: Secure token-based authentication with 30-day access tokens
- 🎨 **RESTful API Design**: Clean, consistent API endpoints following REST principles
- 📱 **CORS Enabled**: Ready for frontend integration (React, Vue, etc.)
- 🐳 **Docker Ready**: Complete containerization setup
- 📦 **Database Fixtures**: Pre-loaded sample data for quick setup
- 🖼️ **Media Management**: Image handling for trips, galleries, profiles, and documents

---

## 🛠️ Technology Stack

### Backend Framework
- **Django** 4.2.4 - High-level Python web framework
- **Django REST Framework** 3.14.0 - Powerful toolkit for building Web APIs
- **Python** 3.11.2

### Database
- **PostgreSQL** - Production-grade relational database
- **psycopg2-binary** 2.9.7 - PostgreSQL adapter

### Authentication & Security
- **djangorestframework-simplejwt** 5.2.2 - JWT authentication
- **PyJWT** 2.8.0 - JSON Web Token implementation
- **cryptography** 41.0.3

### Multilingual & Content
- **django-parler** 2.3 - Model translations
- **django-parler-rest** 2.2 - REST API support for parler
- **django-taggit** 4.0.0 - Tag management

### Additional Libraries
- **django-cors-headers** 4.2.0 - CORS handling
- **django-filter** 23.2 - Advanced filtering
- **Pillow** 10.0.0 - Image processing
- **bleach** 6.0.0 - HTML sanitization

---

## 🏗️ System Architecture

### Django Applications

```
tourzable/
├── accounts/          # User authentication & profile management
├── property/          # Core trip/tour management & bookings
├── blog/             # Content management system
├── about/            # Static pages & contact forms
├── settings/         # Site-wide configuration
└── tourzable/        # Main project settings
```

#### **accounts** - User Management
- Custom user model extending `AbstractBaseUser`
- JWT-based authentication (sign-up, sign-in)
- Profile management with language preferences
- User dashboard with bookings and favorites

#### **property** - Core Business Logic
- **Trip**: Tour packages with detailed information
- **Place**: Tourist destinations
- **Category**: Trip classifications (4-star, 5-star hotels)
- **TripGallery**: Image galleries for trips
- **Reservations**: Booking management with status tracking
- **Reviews**: User ratings and feedback
- **Favorites**: User wishlist
- **PropertyAvailabilityCheck**: Inquiry system
- **Visa**: Visa document management

#### **blog** - Content Management
- Blog posts with categories and tags
- Multilingual article support
- Tag-based filtering

#### **about** - Static Content
- Company information (About Us, Mission, Goals)
- FAQ management
- Contact forms (general & consultant requests)

#### **settings** - Site Configuration
- Global site settings
- Contact information
- Social media links
- Logo and branding

---

## 📥 Installation

### Prerequisites
- Python 3.11.2
- PostgreSQL
- pip (Python package manager)
- virtualenv (recommended)

### Step 1: Clone the Repository
```bash
git clone https://github.com/Andro0o0o0w-Romany/tourzable.git
cd tourzable
```

### Step 2: Create Virtual Environment
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

### Step 3: Install Dependencies
```bash
pip install -r requirments.txt
```

### Step 4: Configure PostgreSQL Database
Create a PostgreSQL database:
```sql
CREATE DATABASE tourzabledb;
CREATE USER tourzable WITH PASSWORD 'Y0uCAnN0tP@$$';
ALTER ROLE tourzable SET client_encoding TO 'utf8';
ALTER ROLE tourzable SET default_transaction_isolation TO 'read committed';
ALTER ROLE tourzable SET timezone TO 'UTC';
GRANT ALL PRIVILEGES ON DATABASE tourzabledb TO tourzable;
```

### Step 5: Update Settings
Update database credentials in `tourzable/settings.py`:
```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'tourzabledb',
        'USER': 'tourzable',
        'PASSWORD': 'Y0uCAnN0tP@$$',
        'HOST': '127.0.0.1',
        'PORT': '5432',
    }
}
```

### Step 6: Run Migrations
```bash
python manage.py makemigrations
python manage.py migrate
```

### Step 7: Load Initial Data (Optional)
```bash
python manage.py loaddata properties.json
python manage.py loaddata blogs.json
```

### Step 8: Create Superuser
```bash
python manage.py createsuperuser
```

### Step 9: Run Development Server
```bash
python manage.py runserver
```

The API will be available at: `http://127.0.0.1:8000/`

---

## ⚙️ Configuration

### Environment Variables
For production, use environment variables instead of hardcoded values:

```bash
# .env file
SECRET_KEY=your-secret-key-here
DEBUG=False
ALLOWED_HOSTS=yourdomain.com,www.yourdomain.com

# Database
DB_NAME=tourzabledb
DB_USER=tourzable
DB_PASSWORD=secure-password
DB_HOST=127.0.0.1
DB_PORT=5432

# JWT Settings
JWT_ACCESS_TOKEN_LIFETIME=30  # days
JWT_REFRESH_TOKEN_LIFETIME=90  # days
```

### CORS Configuration
Update `CORS_ALLOWED_ORIGINS` in settings for your frontend domain:
```python
CORS_ALLOWED_ORIGINS = [
    "http://localhost:3000",
    "https://yourdomain.com",
]
```

### Media Files
Ensure media directory exists and has proper permissions:
```bash
mkdir -p media/{client_user,post,property,trip_images,places,visas,personal_photos,settings}
chmod -R 755 media/
```

---

## 📚 API Documentation

### Base URL
```
http://127.0.0.1:8000/
```

### Authentication
All protected endpoints require JWT authentication:
```http
Authorization: Bearer <your-jwt-token>
```

### API Endpoints

#### **Authentication** (`/accounts/`)
| Method | Endpoint | Description | Auth |
|--------|----------|-------------|------|
| POST | `/sign-up/` | User registration with JWT token | No |
| POST | `/sign-in/` | User login with JWT token | No |
| GET | `/myprofile/` | Get authenticated user profile | Yes |
| PUT | `/myprofile/<id>/` | Update user profile | Yes |

#### **Trips/Properties** (`/property/api/`)
| Method | Endpoint | Description | Auth |
|--------|----------|-------------|------|
| GET | `/list` | List all trips (English) | No |
| GET | `/list/ar` | List all trips (Arabic) | No |
| GET | `/list/<id>` | Trip details with gallery | No |
| GET | `/category` | List all categories | No |
| GET | `/places` | List all destinations | No |
| GET | `/filtering/<slug>` | Advanced filter search | No |
| POST | `/inquiry` | Submit availability inquiry | Yes |
| POST | `/visa` | Submit visa documents | Yes |
| POST | `/list/<id>/reservation` | Book a trip | Yes |
| POST | `/list/<id>/review` | Submit review | Yes |
| POST | `/list/<id>/fav` | Add to favorites | Yes |
| GET | `/dashboard` | User dashboard | Yes |

#### **Blog** (`/blog/api/`)
| Method | Endpoint | Description | Auth |
|--------|----------|-------------|------|
| GET | `/list` | List all blog posts | No |
| GET | `/list/<id>` | Post details | No |
| GET | `/category/<slug>` | Filter by category/tags | No |

#### **About** (`/about/`)
| Method | Endpoint | Description | Auth |
|--------|----------|-------------|------|
| GET | `/about` | Company information | No |
| GET | `/faq` | List FAQs | No |
| POST | `/contact_us` | Submit contact form | No |
| POST | `/contact_consultant` | Request consultant | No |

#### **Home/Settings** (`/`)
| Method | Endpoint | Description | Auth |
|--------|----------|-------------|------|
| GET | `/` | Home page data | No |
| GET | `/category_filter/<query>` | Search and filter | No |

### Example API Calls

#### Sign Up
```bash
curl -X POST http://127.0.0.1:8000/accounts/sign-up/ \
  -H "Content-Type: application/json" \
  -d '{
    "username": "john_doe",
    "email": "john@example.com",
    "password": "secure_password",
    "phone": "+201234567890"
  }'
```

#### Get Trip List
```bash
curl http://127.0.0.1:8000/property/api/list
```

#### Book a Trip (with JWT)
```bash
curl -X POST http://127.0.0.1:8000/property/api/list/1/reservation \
  -H "Authorization: Bearer YOUR_JWT_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "check_in": "2026-03-15",
    "check_out": "2026-03-20",
    "number_of_guests": 2,
    "room_type": "double"
  }'
```

---

## 🗄️ Database Schema

### Core Models

#### **Account** (User Model)
```python
- username: CharField (unique)
- email: EmailField (unique)
- phone: CharField
- profile_image: ImageField
- language: CharField (ar-SA / en-US)
- is_active: BooleanField
- is_staff: BooleanField
```

#### **Trip** (Tour Package)
```python
- title: CharField (translatable)
- description: TextField (translatable)
- slug: SlugField (translatable)
- image: ImageField
- place: ForeignKey(Place)
- category: ForeignKey(Category)
- price_of_single_room_by_person_night: PositiveIntegerField
- price_of_double_room_by_person_night: PositiveIntegerField
- price_of_triple_room_by_person_night: PositiveIntegerField
- stars: CharField
- number_of_guests: PositiveIntegerField
- number_of_rooms: PositiveIntegerField
- duration: PositiveIntegerField
- check_in: DateField
- check_out: DateField
- created_at: DateTimeField
```

#### **Reservations**
```python
- trip: ForeignKey(Trip)
- client: ForeignKey(Account)
- check_in: DateField
- check_out: DateField
- status: CharField (pending/confirmed/canceled)
- number_of_guests: PositiveIntegerField
- total_price: DecimalField
- created_at: DateTimeField
```

#### **Reviews**
```python
- trip: ForeignKey(Trip)
- client: ForeignKey(Account)
- rate: PositiveIntegerField (1-5)
- comment: TextField
- created_at: DateTimeField
```

### Entity Relationships

```
┌─────────────┐
│   Account   │
│   (User)    │
└──────┬──────┘
       │
       ├──────> Reservations
       ├──────> Reviews
       ├──────> Favorites
       └──────> Visa Applications

┌─────────────┐       ┌──────────┐
│    Trip     │<──────│  Place   │
│ (Property)  │       └──────────┘
└──────┬──────┘
       │              ┌──────────┐
       ├──────────────│ Category │
       │              └──────────┘
       ├──────> TripGallery
       ├──────> Reservations
       ├──────> Reviews
       └──────> Favorites

┌─────────────┐       ┌──────────┐
│    Post     │<──────│ Category │
│   (Blog)    │       └──────────┘
└──────┬──────┘
       │
       └──────> Tags (django-taggit)
```

---

## 🌍 Multilingual Support

Tourzable supports **Arabic** (ar-SA) and **English** (en-US) using **django-parler**.

### Supported Languages
- **Arabic** (ar-SA) - Default fallback language
- **English** (en-US)

### Translatable Models
All content models support translations:
- Trip (title, description, slug, accommodation, etc.)
- Place (name, description)
- Category (title)
- Post (title, content)
- About (content)
- Settings (site metadata)

### Language Switching
#### Via API Endpoints
```bash
# English version
GET /property/api/list

# Arabic version
GET /property/api/list/ar
```

#### Via HTTP Headers
```http
Accept-Language: ar-SA
```

#### Via Query Parameter
```bash
GET /property/api/list?lang=ar
```

### Adding New Languages
1. Add language to `PARLER_LANGUAGES` in settings:
```python
PARLER_LANGUAGES = {
    None: (
        {'code': 'ar-SA',},
        {'code': 'en-US',},
        {'code': 'fr-FR',},  # New language
    ),
}
```

2. Run migrations:
```bash
python manage.py makemigrations
python manage.py migrate
```

3. Create translation files:
```bash
python manage.py makemessages -l fr
python manage.py compilemessages
```

---

## 🐳 Docker Deployment

### Using Docker Compose

#### Step 1: Build and Start Containers
```bash
docker-compose up -d
```

This will start:
- **PostgreSQL database** on port 6003
- **Django application** on port 8000

#### Step 2: Run Migrations in Container
```bash
docker exec -it tourzable_web python manage.py migrate
```

#### Step 3: Create Superuser
```bash
docker exec -it tourzable_web python manage.py createsuperuser
```

#### Step 4: Load Sample Data
```bash
docker exec -it tourzable_web python manage.py loaddata properties.json
docker exec -it tourzable_web python manage.py loaddata blogs.json
```

### Docker Configuration

**docker-compose.yaml:**
```yaml
version: '3'
services:
  pgdb:
    image: postgres
    container_name: tourzable
    restart: always
    ports:
      - "6003:5432"
    environment:
      - POSTGRES_DB=tourzableDB
      - POSTGRES_USER=tourzable
      - POSTGRES_PASSWORD=Y0uCAnN0tP@$$
```

**Dockerfile:**
```dockerfile
FROM python:3.11.2
RUN apt-get update && apt-get install -y postgresql-client
WORKDIR /usr/src/app
COPY requirements.txt ./
RUN pip install -r requirements.txt
COPY . .
EXPOSE 8000
CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]
```

### Stopping Containers
```bash
docker-compose down
```

---

## 📂 Project Structure

```
tourzable/
├── about/                      # About & contact app
│   ├── models.py              # About, FAQ, ContactUs models
│   ├── serializers.py         # DRF serializers
│   ├── api_view.py            # API views
│   └── urls.py                # URL routing
│
├── accounts/                   # User authentication
│   ├── models.py              # Custom Account model
│   ├── accounts_serializer.py # User serializers
│   ├── api_view.py            # Auth API views
│   └── urls.py                # Auth URLs
│
├── blog/                       # Blog/CMS app
│   ├── models.py              # Post, Category models
│   ├── serializers.py         # Blog serializers
│   ├── api_view.py            # Blog API views
│   └── urls.py                # Blog URLs
│
├── property/                   # Core trip management
│   ├── models.py              # Trip, Place, Reservation, Review, etc.
│   ├── serializers.py         # Property serializers
│   ├── api_view.py            # Property API views
│   ├── filters.py             # Advanced filtering
│   └── urls.py                # Property URLs
│
├── settings/                   # Site settings app
│   ├── models.py              # Settings model
│   ├── api_view.py            # Settings API
│   └── urls.py                # Settings URLs
│
├── tourzable/                  # Main project
│   ├── settings.py            # Django settings
│   ├── urls.py                # Root URL config
│   └── wsgi.py                # WSGI config
│
├── media/                      # User-uploaded files
│   ├── property/              # Trip images
│   ├── client_user/           # Profile pictures
│   ├── visas/                 # Visa documents
│   └── ...
│
├── templates/                  # HTML templates
├── locale/                     # Translation files
├── backups/                    # Database backups
│
├── manage.py                   # Django CLI
├── requirments.txt            # Python dependencies
├── Dockerfile                 # Docker configuration
├── docker-compose.yaml        # Docker Compose config
├── properties.json            # Trip fixtures
├── blogs.json                 # Blog fixtures
└── data.json                  # Complete DB dump
```

---

## 👨‍💻 Development

### Running Tests
```bash
python manage.py test
```

### Creating Migrations
```bash
python manage.py makemigrations
python manage.py migrate
```

### Django Admin
Access the admin panel at: `http://127.0.0.1:8000/admin/`

### API Browseable Interface
Django REST Framework provides a browseable API at each endpoint when accessed via browser.

### Code Style
Follow PEP 8 style guide:
```bash
pip install flake8
flake8 .
```

### Database Backups
Create a database backup:
```bash
python manage.py dumpdata > backup.json
```

Load from backup:
```bash
python manage.py loaddata backup.json
```

### Collecting Static Files
```bash
python manage.py collectstatic
```

---

## 🔐 Security Considerations

### For Production Deployment:

1. **Environment Variables**: Never commit credentials to version control
   ```bash
   pip install python-decouple
   ```

2. **SECRET_KEY**: Generate a new secret key
   ```python
   from django.core.management.utils import get_random_secret_key
   print(get_random_secret_key())
   ```

3. **DEBUG**: Set to False in production
   ```python
   DEBUG = False
   ```

4. **ALLOWED_HOSTS**: Specify your domain
   ```python
   ALLOWED_HOSTS = ['yourdomain.com', 'www.yourdomain.com']
   ```

5. **HTTPS**: Use HTTPS in production
   ```python
   SECURE_SSL_REDIRECT = True
   SESSION_COOKIE_SECURE = True
   CSRF_COOKIE_SECURE = True
   ```

6. **Database**: Use strong passwords and restrict access

7. **CORS**: Limit CORS origins to your frontend domain only

---

## 🚀 Deployment Checklist

- [ ] Set `DEBUG = False`
- [ ] Configure `ALLOWED_HOSTS`
- [ ] Use environment variables for secrets
- [ ] Set up PostgreSQL with strong password
- [ ] Configure HTTPS
- [ ] Set up proper CORS origins
- [ ] Configure static file serving (WhiteNoise/CDN)
- [ ] Set up media file storage (S3/CloudFlare)
- [ ] Configure logging
- [ ] Set up monitoring (Sentry)
- [ ] Configure backup strategy
- [ ] Set up CI/CD pipeline
- [ ] Performance optimization (caching, CDN)

---

## 🤝 Contributing

This project is under a proprietary license. All rights reserved to Andrew Romany.

For authorized contributors:
1. Create a feature branch
2. Make your changes
3. Write/update tests
4. Submit a pull request

---

## 📝 License

**Proprietary License - All Rights Reserved**

Copyright © 2026 Andrew Romany. All Rights Reserved.

This software and associated documentation files are the exclusive property of Andrew Romany. No part of this software may be reproduced, distributed, or used without prior written permission.

For licensing inquiries, please contact Andrew Romany.

---

## 📞 Contact & Support

**Project Owner**: Andrew Romany
**Repository**: [https://github.com/Andro0o0o0w-Romany/tourzable](https://github.com/Andro0o0o0w-Romany/tourzable)

For support, feature requests, or bug reports, please open an issue on GitHub.

---

## 🙏 Acknowledgments

- Django Software Foundation
- Django REST Framework
- All open-source contributors whose libraries made this project possible

---

<div align="center">

**Built with ❤️ for Egyptian Tourism**

*Making travel booking seamless and accessible for everyone*

</div>

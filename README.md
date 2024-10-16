# Musicify Fullstack 🎶

Musicify is a full-stack web application that allows users to explore, upload, and interact with music. The app features a Spotify-like experience for discovering top artists and tracks. It integrates a Shopify-like frontend with a robust Django and PostgreSQL backend, and AWS for storage. The app uses Gunicorn for production and includes real-time data scraping from Spotify.

> **Note**: This project is for **non-commercial purposes** only. The Spotify Scraper API and other components used within the project are intended for personal or educational use. Please ensure you comply with the terms of use of the APIs and libraries involved.

## Features
- User authentication with social login (via `django-allauth`)
- Discover and display top artists and tracks using the Spotify API
- Search for tracks and retrieve detailed metadata, including audio files and images
- Responsive, Shopify-like user interface (HTML/CSS)
- PostgreSQL as the primary database
- AWS S3 and Google Drive for media storage
- Deployed with Gunicorn for production environments

## Tech Stack
- **Frontend**: HTML5, CSS3
- **Backend**: Django 4.1, Python 3, Gunicorn
- **Database**: PostgreSQL
- **Storage**: AWS S3, Google Drive (via `django-googledrive-storage`)
- **Production**: Gunicorn, Whitenoise for static files

---

## Getting Started

### Prerequisites
Ensure you have the following installed:
- Python 3.9+
- PostgreSQL
- Virtualenv or Conda (for virtual environment management)

### Setup Instructions

1. **Clone the repository:**
   ```bash
   git clone https://github.com/yourusername/musicify_fullstack.git
   cd musicify_fullstack
   ```

2. **Create a virtual environment and activate it:**
   ```bash
   python3 -m venv env
   source env/bin/activate  # On Windows use `env\Scripts\activate`
   ```

3. **Install dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

4. **Set up PostgreSQL database:**

   Create a PostgreSQL database and user:
   ```sql
   CREATE DATABASE musicify_db;
   CREATE USER musicify_user WITH PASSWORD 'yourpassword';
   ALTER ROLE musicify_user SET client_encoding TO 'utf8';
   ALTER ROLE musicify_user SET default_transaction_isolation TO 'read committed';
   ALTER ROLE musicify_user SET timezone TO 'UTC';
   GRANT ALL PRIVILEGES ON DATABASE musicify_db TO musicify_user;
   ```

5. **Configure environment variables:**

   Create a `.env` file in the root directory and add the following details:
   ```bash
   SECRET_KEY=your-secret-key
   DEBUG=True
   DATABASE_URL=postgres://musicify_user:yourpassword@localhost/musicify_db
   AWS_ACCESS_KEY_ID=your-aws-access-key
   AWS_SECRET_ACCESS_KEY=your-aws-secret-key
   AWS_STORAGE_BUCKET_NAME=your-s3-bucket
   RAPIDAPI_KEY=your-rapidapi-key
   ```

6. **Apply migrations:**
   ```bash
   python manage.py migrate
   ```

7. **Create a superuser for Django admin:**
   ```bash
   python manage.py createsuperuser
   ```

8. **Run the development server:**
   ```bash
   python manage.py runserver
   ```

   Access the app at `http://127.0.0.1:8000/`.

---

## API Integration

This project uses the Spotify Scraper API to retrieve top artists, tracks, and metadata for music search and exploration.

- **Top Artists**: Fetches the top artists from Spotify.
- **Top Tracks**: Retrieves the top tracks from Spotify.
- **Track Metadata**: Gets detailed track metadata, including audio download links and images.

> **Disclaimer**: The Spotify Scraper API used here is for **non-commercial** and **educational** purposes only. Please ensure that you are compliant with Spotify's terms and the API usage terms.

---

## Deployment

### Gunicorn Setup for Production
1. **Install Gunicorn:**
   ```
   pip install gunicorn
   ```

2. **Run Gunicorn server:**
   ```bash
   gunicorn musicify.wsgi:application --bind 0.0.0.0:8000
   ```

3. **Static Files Setup with Whitenoise:**
   Ensure `Whitenoise` is installed and configured in `settings.py`:
   ```python
   MIDDLEWARE = [
       'whitenoise.middleware.WhiteNoiseMiddleware',
       # other middlewares
   ]

   STATIC_ROOT = os.path.join(BASE_DIR, 'staticfiles')
   STATICFILES_STORAGE = 'whitenoise.storage.CompressedManifestStaticFilesStorage'
   ```

4. **Serving Static Files**:
   Run `collectstatic` before deploying:
   ```bash
   python manage.py collectstatic
   ```

---

## Requirements

This project uses the following libraries (available in `requirements.txt`):
```plaintext
asgiref==3.7.2
beautifulsoup4==4.12.2
bs4==0.0.1
defusedxml==0.7.1
dj-database-url==2.1.0
Django==4.1.13
django-allauth==0.54.0
django-extensions==3.2.1
django-googledrive-storage==1.6.0
django-storages==1.13.2
gunicorn==21.2.0
html5lib==1.1
httpcore==0.9.1
httplib2==0.22.0
httpx==0.13.3
Jinja2==3.1.2
lxml==4.9.2
multidict==6.0.4
Pillow==9.4.0
psycopg2-binary==2.9.9
python3-openid==3.2.0
regex==2023.10.3
requests==2.28.2
soupsieve==2.5
sqlparse==0.4.3
urllib3==1.26.14
websockets==11.0.3
whitenoise==6.6.0
```

---

## License

This project is licensed under the MIT License.

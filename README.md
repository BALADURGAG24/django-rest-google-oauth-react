
# Django REST API with Token Auth & Google OAuth2

A modern Django 5 REST API project template with:

✅ Django REST Framework (DRF)   
✅ Token-based authentication (via dj-rest-auth)   
✅ Google OAuth2 login (via django-allauth)    
✅ Session authentication for browser clients     
✅ User management (`users` app)     
✅ SQLite for development  
✅ Easily extendable for production (PostgreSQL, CORS, API versioning, etc.) 
 
---

## ✨ Features

- REST API built with Django REST Framework (DRF)
- Token-based authentication (using DRF tokens + dj-rest-auth)
- Social login via Google OAuth2 (django-allauth)
- Standard Django login (username/password or email/password)
- Ready for web apps or mobile apps (React, React Native, Flutter, etc.)
- Basic `users` app scaffolded for user customization
- Session authentication for browser testing (Django Admin, browsable API)
- Secure middleware and sensible defaults

---

## 🚀 Getting Started

### 1️⃣ Clone the repository

```bash
git clone https://github.com/BALADURGAG24/django-rest-google-oauth-react.git
cd django-rest-google-oauth-react
```

### 2️⃣ Create and activate a virtual environment

```bash
python -m venv venv
source venv/bin/activate   # On Windows: venv\Scripts\activate
```

### 3️⃣ Install dependencies

```bash
pip install -r requirements.txt
```

You can generate `requirements.txt` like this:

```bash
pip freeze > requirements.txt
```

Example `requirements.txt` based on your settings:

```
Django==5.2.2
djangorestframework
dj-rest-auth
django-allauth
djangorestframework-simplejwt  # Optional, if using JWT later
```

### 4️⃣ Apply migrations

```bash
python manage.py migrate
```

### 5️⃣ Create a superuser (admin account)

```bash
python manage.py createsuperuser
```

### 6️⃣ Run the development server

```bash
python manage.py runserver
```

---

## 🏗 Project Structure

```
project-root/
├── backend/ (Django project)
│   ├── myproject/              # Django project settings and main config
│   │   ├── __init__.py
│   │   ├── asgi.py
│   │   ├── settings.py
│   │   ├── urls.py
│   │   ├── wsgi.py
│   ├── users/                  # Custom users app
│   │   ├── __init__.py
│   │   ├── admin.py
│   │   ├── apps.py
│   │   ├── models.py
│   │   ├── serializers.py
│   │   ├── signals.py
│   │   ├── tests.py
│   │   ├── urls.py
│   │   ├── views.py
│   │   ├── migrations/
│   │   ├── __pycache__/
│   ├── db.sqlite3
│   ├── manage.py
│   ├── __pycache__/
│
├── social-logins-frontend/ (React project)
│   ├── public/
│   ├── src/
│   │   ├── components/
│   │   │   ├── GoogleLoginButton.js
│   │   │   ├── Profile.js
│   │   ├── App.css
│   │   ├── App.js
│   │   ├── App.test.js
│   │   ├── index.css
│   │   ├── index.js
│   │   ├── logo.svg
│   │   ├── reportWebVitals.js
│   │   ├── setupTests.js
│   ├── .env
│   ├── .gitignore
│   ├── package-lock.json
│   ├── package.json
│   ├── README.md

```

---

## 🔐 Authentication Setup

### Session Authentication (Browser Clients)

- Built-in via `SessionAuthentication` (for Django Admin, Browsable API)

### Token Authentication (Mobile Apps / API Clients)

- Enabled via `rest_framework.authentication.TokenAuthentication`
- Token endpoints provided by `dj-rest-auth`:

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST   | /dj-rest-auth/login/ | Login and get auth token |
| POST   | /dj-rest-auth/logout/ | Logout |
| POST   | /dj-rest-auth/registration/ | Register new user |
| GET    | /accounts/google/login/ | Redirect to Google login |

### Google OAuth2

- Configured via `django-allauth`
- Example settings:

```python
SOCIALACCOUNT_PROVIDERS = {
    'google': {
        'APP': {
            'client_id': '<YOUR_GOOGLE_CLIENT_ID>',
            'secret': '<YOUR_GOOGLE_CLIENT_SECRET>',
            'key': ''
        },
        'SCOPE': [
            'profile',
            'email',
        ],
        'AUTH_PARAMS': {
            'access_type': 'online',
        }
    }
}
```

- Use `/accounts/google/login/` or configure with your frontend app.

---

## ⚙️ Environment Configuration

**Basic settings you can customize in `settings.py`:**

- `DEBUG = True` → Set `False` in production.
- `ALLOWED_HOSTS = ['yourdomain.com']`
- `SECRET_KEY` → Change for production.
- `DATABASES` → Use PostgreSQL in production.

---

## 🛠 API Endpoints

### Auth

| Method | Endpoint                      | Description               |
|--------|-------------------------------|---------------------------|
| POST   | `/dj-rest-auth/login/`        | Login and get auth token  |
| POST   | `/dj-rest-auth/logout/`       | Logout                    |
| POST   | `/dj-rest-auth/registration/` | Register new user         |
| GET    | `/accounts/google/login/`     | Redirect to Google login  |

### Example Protected API View

```python
from rest_framework.views import APIView
from rest_framework.response import Response
from rest_framework.permissions import IsAuthenticated

class HelloView(APIView):
    permission_classes = [IsAuthenticated]

    def get(self, request):
        return Response({"message": "Hello, authenticated user!"})
```

---

## 🧑‍💻 Development Notes

- **Django Admin:** `/admin/`
- **Browsable API:** Available in development
- **Token Auth:** Ideal for mobile apps and SPA (React, Flutter, React Native, etc.)
- **Social Login:** Google OAuth2 configured, add more providers easily.

---

## 🚀 Deployment

- Use `DEBUG = False` in production
- Add proper `ALLOWED_HOSTS`
- Use PostgreSQL for production database
- Configure CORS if serving from different domain
- Set up static files (with `collectstatic`)
- Use HTTPS and a secure reverse proxy (NGINX, Caddy, etc.)

---

## 🤝 Contributing

Pull requests welcome! For major changes, please open an issue first to discuss what you would like to change.

---

## 📜 License

MIT License

---

## 🙏 Credits

Built with:

- [Django](https://www.djangoproject.com/)
- [Django REST Framework](https://www.django-rest-framework.org/)
- [dj-rest-auth](https://dj-rest-auth.readthedocs.io/)
- [django-allauth](https://django-allauth.readthedocs.io/)

---

Happy coding! 🚀

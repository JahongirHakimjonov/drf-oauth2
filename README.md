# drf-oauth2

OAuth2 implementation for Django Rest Framework.

## Installation

To install the package, use pip:

```bash
pip install drf-oauth2
```

## Requirements

- Python >= 3.7
- Django >= 4.0
- djangorestframework >= 3.12

## Setup

Add `oauth2` to your `INSTALLED_APPS` in your Django settings:

```python
INSTALLED_APPS = [
    # Your apps
    'oauth2',
]
```

Include the `oauth2` URLs in your project's `urls.py`:

```python
from django.urls import path, include

urlpatterns = [
    # Your URLs
    path('auth/', include('oauth2.urls')),
]
```

## Configuration

Configure your OAuth2 providers in your Django settings:

```python
import os

SOCIAL_AUTH_CONFIG = {
    "google": {
        "client_id": os.getenv("GOOGLE_CLIENT_ID", ""),
        "client_secret": os.getenv("GOOGLE_CLIENT_SECRET", ""),
        "redirect_uri": os.getenv("GOOGLE_REDIRECT_URI", ""),
    },
    "github": {
        "client_id": os.getenv("GITHUB_CLIENT_ID", ""),
        "client_secret": os.getenv("GITHUB_CLIENT_SECRET", ""),
        "redirect_uri": os.getenv("GITHUB_REDIRECT_URI", ""),
    },
    "facebook": {
        "client_id": os.getenv("FACEBOOK_CLIENT_ID", ""),
        "client_secret": os.getenv("FACEBOOK_CLIENT_SECRET", ""),
        "redirect_uri": os.getenv("FACEBOOK_REDIRECT_URI", ""),
        "api_version": os.getenv("FACEBOOK_API_VERSION", "v21.0"),
    },
}
```

## Usage

### Endpoints

- `POST /auth/social/register/` - Authenticate with a social provider.
- `GET /auth/social/list/` - List available OAuth2 providers.

### Example Request

#### Authenticate with a social provider

```http
GET /auth/social/register/
Content-Type: application/json

Request body:
{
    "provider": "google"
}

Response body:
{
    "success": true,
    "message": "Redirecting to provider",
    "data": {
        "url": "https://github.com/login/oauth/authorize?client_id=CLIENTID&redirect_uri=http://localhost:3001/auth/github/redirect/&scope=user:email"
    }
}
```

```http
POST /auth/social/register/
Content-Type: application/json

Request body:
{
    "provider": "google",
    "code": "authorization-code"
}

Response body:
{
    "success": true,
    "message": "Authentication successful",
    "data": {
        "refresh": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ0b2tlbl90eXBlIjoicmVmcmVzaCIsImV4cCI6MTczODI0MTc0MCwiaWF0IjoxNzM4MTU1MzQwLCJqdGkiOiJiNzU3NWQzNzM1MTg0NDIxYmUzZWVjNmUxZmQwZGJkZiIsInVzZXJfaWQiOjJ9.ZaOaoYgXdaoyyPNWHnywkd97kVA6NwGHTLL2BnIrhQA",
        "access": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ0b2tlbl90eXBlIjoiYWNjZXNzIiwiZXhwIjoxNzM4MTU1NjQwLCJpYXQiOjE3MzgxNTUzNDAsImp0aSI6IjUzNzBhODQ4MDk4MzRmMzA5ZjdiZmE0ODgzNzFiZGI1IiwidXNlcl9pZCI6Mn0.4CimC7CL25EFeZyiWVTgqSE-KxTsnnjl_CXSCmPDITc",
        "user": 2,
        "expired_at": "2025-02-28T12:55:40.058390Z"
    }
}
```

#### List available providers

```http
GET /auth/social/list/

Response body:
{
    "success": true,
    "message": "Available providers",
    "data": [
        "github"
    ]
}
```

## Development

To install development dependencies, use:

```bash
pip install -e .[dev]
```

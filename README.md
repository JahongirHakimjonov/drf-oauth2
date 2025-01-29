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

- `POST /auth/social/` - Authenticate with a social provider.
- `GET /auth/providers/` - List available OAuth2 providers.

### Example Request

#### Authenticate with a social provider

```http
POST /auth/social/
Content-Type: application/json

{
    "provider": "google",
    "code": "authorization-code"
}
```

#### List available providers

```http
GET /auth/providers/
```

## Development

To install development dependencies, use:

```bash
pip install -e .[dev]
```

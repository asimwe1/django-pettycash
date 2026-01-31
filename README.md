# Django PettyCash Management System

<div align="center">
    <h1>PettyCash - Simple Cash Management Solution</h1>
    
    ![Python](https://img.shields.io/badge/python-3.11-blue.svg)
    ![Django](https://img.shields.io/badge/django-4.2.18-green.svg)
    ![Poetry](https://img.shields.io/badge/poetry-dependency%20manager-orange.svg)
    ![License](https://img.shields.io/badge/license-MIT-brightgreen.svg)
    ![GitHub last commit](https://img.shields.io/github/last-commit/asimwe1/pettycash-system)
    
</div>

## 📋 Overview

Django PettyCash is a comprehensive web application for managing petty cash transactions in organizations. It provides a simple yet powerful interface for tracking expenses, managing accounts, and generating reports.

## ✨ Features

### ✅ **Core Features**
- **Transaction Management**: Create, read, update, and delete petty cash transactions
- **Account Management**: Multiple petty cash accounts with individual balances
- **Location Tracking**: Track expenses by department or location
- **Purchase Categories**: Categorize expenses for better reporting
- **Receipt Management**: Upload and store transaction receipts

### 🔐 **Authentication & Security**
- Django authentication system
- Google OAuth integration via django-allauth
- Role-based access control
- Secure session management

### 📊 **Reporting & Analytics**
- Real-time transaction dashboards
- Expense summaries and trends
- Customizable reporting periods
- Export functionality

### 🚀 **Advanced Features**
- **Async Notifications**: Real-time updates using Django Channels
- **File Storage**: MongoDB GridFS for scalable file storage
- **AJAX Interface**: Smooth, responsive user experience
- **RESTful API**: Built-in API endpoints for integration

## 🛠️ Technology Stack

| Component | Technology |
|-----------|------------|
| **Backend** | Django 4.2, Python 3.11 |
| **Database** | PostgreSQL/MySQL, MongoDB (GridFS) |
| **Async** | Django Channels, Daphne |
| **Auth** | django-allauth, Google OAuth |
| **Frontend** | HTML5, Bootstrap, JavaScript (AJAX) |
| **Tools** | Poetry (dependency management) |

## 🚀 Quick Start

### Prerequisites
- Python 3.11 or higher
- Poetry (dependency manager)
- MongoDB (for file storage)
- MySQL/PostgreSQL/SQLite (for main database)

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/asimwe1/pettycash-system.git
   cd pettycash-system
   ```

2. **Install dependencies with Poetry**
   ```bash
   poetry install
   poetry shell
   ```

3. **Configure environment variables**
   ```bash
   cd src
   cp django_pettycash/.env.example django_pettycash/.env
   # Edit .env with your configuration
   ```

4. **Configure database in `.env` file**
   ```env
   # For SQLite (development)
   ENGINE=django.db.backends.sqlite3
   NAME=db.sqlite3
   
   # For PostgreSQL (production)
   # ENGINE=django.db.backends.postgresql
   # NAME=pettycash_db
   # USER=postgres_user
   # PASSWORD=your_password
   # HOST=localhost
   # PORT=5432
   
   # MongoDB for file storage
   MONGO_HOST=mongodb://localhost:27017
   MONGO_DB=pettycash_files
   ```

5. **Run database migrations**
   ```bash
   python manage.py migrate
   ```

6. **Create superuser**
   ```bash
   python manage.py createsuperuser
   ```

7. **Load sample data (optional)**
   ```bash
   python manage.py loaddata */fixtures/*.json
   ```

8. **Start development server**
   ```bash
   python manage.py runserver
   ```

9. **Access the application**
   - Main site: http://localhost:8000
   - Admin panel: http://localhost:8000/admin
   - Login: Use your superuser credentials

## 🐛 Common Issues & Solutions

### Issue 1: Poetry not found
```bash
# Install Poetry
curl -sSL https://install.python-poetry.org | python3 -
export PATH="$HOME/.local/bin:$PATH"
```

### Issue 2: Python 3.14 compatibility with cffi
If using Python 3.14, update pyproject.toml:
```toml
python = ">=3.11,<3.15"
```

### Issue 3: django-allauth configuration error
Ensure only one `ACCOUNT_EMAIL_VERIFICATION` setting exists in settings.py:
```python
ACCOUNT_EMAIL_VERIFICATION = 'none'  # Remove any duplicates
```

### Issue 4: MongoDB connection error
If MongoDB is not available, modify `transaction/views.py`:
```python
# Add error handling around MongoDB connection
try:
    client = MongoClient(settings.MONGO_HOST)
    db = client[settings.MONGO_DB]
    collection = db['pettycash']
except:
    client = db = collection = None
```

## 📁 Project Structure

```
django_pettycash/
├── src/
│   ├── dashboard/          # Dashboard views and analytics
│   ├── django_pettycash/   # Main Django project settings
│   ├── location/           # Location management app
│   ├── pettycash_account/  # Account management app
│   ├── transaction/        # Transaction management app
│   ├── user/              # User management and authentication
│   ├── report/            # Reporting module
│   ├── static/            # Static files (CSS, JS, images)
│   ├── templates/         # HTML templates
│   └── manage.py          # Django management script
├── requirements.txt       # Production dependencies
├── pyproject.toml        # Poetry configuration
├── poetry.lock          # Poetry lock file
└── README.md            # This file
```

## 🔧 Configuration Tips

### For Development
- Use SQLite for simplicity
- Set `DEBUG = True` in `.env`
- Use `ACCOUNT_EMAIL_VERIFICATION = 'none'`
- Set email backend to console: `EMAIL_BACKEND = 'django.core.mail.backends.console.EmailBackend'`

### For Production
- Use PostgreSQL or MySQL
- Set `DEBUG = False`
- Configure proper email backend
- Set `ALLOWED_HOSTS` to your domain
- Use environment variables for secrets

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Commit your changes
4. Push to the branch
5. Open a Pull Request

## 📄 License

MIT License - see LICENSE file for details.

---

<div align="center">
  Made with ❤️ using Django | Improved by <a href="https://github.com/asimwe1">@asimwe1</a>
</div>

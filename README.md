# 🚀 FastAPI + Supabase Boilerplate

A modern, production-ready FastAPI boilerplate with Supabase integration, featuring proper async support, dependency injection, comprehensive error handling, and structured logging.

## ✨ Features

### 🏗️ **Architecture**
- **Clean Architecture** with separated concerns (controllers, services, models)
- **Dependency Injection** using FastAPI's built-in DI system
- **Async/Await** with proper thread pool execution for Supabase operations
- **Structured Error Handling** with request ID tracing
- **Comprehensive Logging** with contextual information

### 🔧 **Technical Features**
- **Database-Level Pagination** for efficient data retrieval
- **Flexible Filtering** with support for multiple operators (`ilike`, `gte`, `lte`, etc.)
- **Consistent Response Format** across all endpoints
- **CORS Support** for cross-origin requests
- **Request ID Tracing** for distributed system debugging
- **Health Check Endpoints** for monitoring

### 🛠️ **API Endpoints**
- **CRUD Operations** for items management
- **Advanced Search** with partial matching and price range filtering
- **Pagination Support** on all list endpoints
- **Interactive Documentation** with Swagger UI and ReDoc

## 🚀 Quick Start

### Prerequisites
- Python 3.9+
- Poetry (recommended) or pip
- Supabase account and project

### 1. Clone and Setup
```bash
git clone <your-repo-url>
cd fast-api-playground
```

### 2. Install Dependencies
```bash
# With Poetry (recommended)
poetry install

# Or with pip
pip install -r requirements.txt
```

### 3. Environment Configuration
```bash
# Copy environment template
cp .env.example .env

# Edit .env with your Supabase credentials
# SUPABASE_PROJECT_URL=https://your-project.supabase.co
# SUPABASE_API_KEY=your-anon-key
```

### 4. Database Setup
1. Go to your Supabase dashboard → SQL Editor
2. Copy and paste the content of `setup_db.sql`
3. Execute the script to create tables and sample data

### 5. Run the Application
```bash
# Option 1: Using the enhanced startup script
python run.py

# Option 2: Direct FastAPI
python main.py

# Option 3: Using uvicorn directly
uvicorn main:app --reload
```

### 6. Explore the API
- **API Documentation**: http://localhost:8000/docs
- **Alternative Docs**: http://localhost:8000/redoc
- **Health Check**: http://localhost:8000/api/v1/health

## 📚 API Documentation

### Core Endpoints

#### Items Management
```
GET    /api/v1/items/              # List all items (with pagination)
POST   /api/v1/items/              # Create new item
GET    /api/v1/items/{id}          # Get specific item
PUT    /api/v1/items/{id}          # Update item
DELETE /api/v1/items/{id}          # Delete item
```

#### Search & Filtering
```
GET    /api/v1/items/search/              # General search
GET    /api/v1/items/search/offers        # Items on offer
GET    /api/v1/items/search/name/{name}   # Search by name
GET    /api/v1/items/search/price-range/  # Price range filtering
```

#### System
```
GET    /api/v1/health/     # Health check
GET    /api/v1/health/ready # Readiness check
```

### Example Requests

**Create Item:**
```bash
curl -X POST "http://localhost:8000/api/v1/items/" \
  -H "Content-Type: application/json" \
  -d '{
    "name": "Coffee Mug",
    "price": 12.99,
    "is_offer": false
  }'
```

**Search Items:**
```bash
curl "http://localhost:8000/api/v1/items/search/?q=coffee&skip=0&limit=10"
```

**Price Range Filter:**
```bash
curl "http://localhost:8000/api/v1/items/search/price-range/?min_price=10&max_price=50"
```

## 🏗️ Project Structure

```
├── controllers/           # API route handlers
│   ├── __init__.py
│   ├── health_controller.py
│   └── items_controller.py
├── middleware/           # Custom middleware
│   ├── __init__.py
│   ├── cors.py
│   ├── error_handling.py
│   └── logging.py
├── models/              # Pydantic models
│   ├── __init__.py
│   └── item.py
├── services/            # Business logic
│   ├── __init__.py
│   ├── db_service.py
│   └── items_service.py
├── config.py            # Configuration settings
├── dependencies.py      # Dependency injection
├── main.py             # FastAPI application
├── run.py              # Enhanced startup script
├── setup_db.sql        # Database schema
└── requirements.txt    # Dependencies
```

## 🔧 Configuration

### Environment Variables
```bash
# Required
SUPABASE_PROJECT_URL=https://your-project.supabase.co
SUPABASE_API_KEY=your-anon-key

# Optional
HOST=0.0.0.0
PORT=8000
RELOAD=true
LOG_LEVEL=info
```

### Database Schema
The project includes a complete database schema (`setup_db.sql`) with:
- Items table with proper constraints
- Performance indexes
- Sample data for testing

## 🧪 Testing

### Manual Testing
Visit the interactive API documentation at `http://localhost:8000/docs` to test all endpoints.

### Health Checks
- `GET /api/v1/health/` - Basic health check
- `GET /api/v1/health/ready` - Readiness check with dependencies

## 🚀 Production Deployment

### Environment Setup
1. Set `RELOAD=false` in production
2. Configure proper logging levels
3. Use environment-specific `.env` files
4. Set up proper database credentials

### Docker (Optional)
```dockerfile
FROM python:3.9-slim

WORKDIR /app
COPY requirements.txt .
RUN pip install -r requirements.txt

COPY . .
CMD ["python", "main.py"]
```

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📈 Key Improvements

This boilerplate includes several production-ready improvements:

1. **✅ Proper Async Support** - Real async with thread pool execution
2. **✅ Centralized Logging** - Structured logging with request tracing
3. **✅ Flexible Filtering** - Multiple operators and advanced search
4. **✅ Consistent Returns** - Standardized response format
5. **✅ Database Pagination** - Efficient data retrieval
6. **✅ Dependency Injection** - Clean, testable architecture

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 🙏 Acknowledgments

- [FastAPI](https://fastapi.tiangolo.com/) for the amazing framework
- [Supabase](https://supabase.com/) for the backend-as-a-service platform
- [Pydantic](https://pydantic-docs.helpmanual.io/) for data validation

---

**Happy coding! 🚀** 
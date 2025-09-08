# 🛒 UrbanCart - Secure E-Commerce Web Application

## 🔍 Overview

UrbanCart is a **secure e-commerce platform** developed as part of a course project, designed to simulate real-world online shopping systems while emphasizing **security best practices**. The application integrates a modular frontend (React), backend (Flask), and database (PostgreSQL on AWS RDS), deployed inside Docker containers for consistency and isolation.

This project demonstrates how to implement modern web technologies with a focus on **authentication, authorization, and secure payments**, serving as a blueprint for building production-ready e-commerce platforms.

## 🎯 Problem Statement

Modern e-commerce platforms face numerous security challenges:
- **Data Breaches**: Sensitive customer information and payment data at risk
- **Authentication Vulnerabilities**: Weak user verification and session management
- **Payment Security**: Ensuring secure transaction processing
- **Scalability Issues**: Managing growing user bases and transaction volumes
- **Deployment Complexity**: Consistent environments across development and production

UrbanCart addresses these challenges by implementing a **security-first architecture** with robust authentication, encrypted data handling, and containerized deployment.

## 🔑 Key Features

### **🔐 Authentication & Security**
- **JWT-based Authentication**: Secure user sessions with HTTP-only cookies
- **CSRF Protection**: Token validation for request integrity
- **OTP Verification**: Firebase-based phone verification for account creation & payments
- **Password Security**: Bcrypt hashing with salt for secure password storage
- **HTTPS Support**: SSL/TLS encryption via ngrok (demo) with planned Route53 + CA cert for production

### **💾 Database Security (PostgreSQL on AWS RDS)**
- **Normalized Schema**: Complete e-commerce data model covering Users, Products, Categories, Orders, Payments, Reviews, and Carts
- **ACID Compliance**: Reliable transactions ensuring data integrity
- **Encryption**: AES-256 at rest and SSL/TLS in transit
- **SQL Injection Prevention**: SQLAlchemy ORM for secure database interactions

### **💳 Payment Integration**
- **Stripe API**: Secure online payment processing
- **Tokenization**: Safe handling of payment information
- **Webhook Handling**: Real-time order status updates
- **OTP Verification**: Additional security layer before transaction completion

### **⚛️ Frontend (React)**
- **Component Architecture**: Modular and scalable design
- **Core Features**: Product browsing, cart management, user authentication, secure checkout
- **Stripe Elements**: Integrated payment UI components
- **XSS Protection**: Automatic escaping and Content Security Policy (CSP)

### **🐍 Backend (Flask)**
- **REST APIs**: Stateless, JWT-secured client-server communication
- **SQLAlchemy ORM**: Secure database interaction preventing SQL injection
- **Docker Containerization**: Reproducible and isolated deployment
- **Microservices Ready**: Modular architecture for scalability

## 🏗️ System Architecture

```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   React         │───▶│   Flask API     │───▶│   PostgreSQL    │
│   Frontend      │    │   (Docker)      │    │   (AWS RDS)     │
└─────────────────┘    └─────────────────┘    └─────────────────┘
         │                       │                       │
         ▼                       ▼                       ▼
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   Firebase      │    │   Stripe API    │    │   Nginx         │
│   OTP Auth      │    │   Payments      │    │   Reverse Proxy │
└─────────────────┘    └─────────────────┘    └─────────────────┘
```

## 🛠️ Tech Stack

### **Frontend Technologies**
- **React.js**: Component-based UI framework
- **Material-UI**: Modern design system
- **React Router**: Client-side routing
- **Stripe Elements**: Secure payment components

### **Backend Technologies**
- **Flask**: Lightweight Python web framework
- **SQLAlchemy**: Python ORM for database operations
- **JWT**: JSON Web Tokens for authentication
- **Bcrypt**: Password hashing library

### **Database & Infrastructure**
- **PostgreSQL**: Relational database on AWS RDS
- **Docker**: Containerization platform
- **AWS EC2**: Cloud computing instances
- **Nginx**: Reverse proxy and load balancer

### **Security & Payments**
- **Firebase**: OTP authentication service
- **Stripe API**: Payment processing platform
- **SSL/TLS**: Encryption in transit
- **CSRF Tokens**: Cross-site request forgery protection

## 📊 Database Schema

```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│     Users       │    │    Products     │    │   Categories    │
├─────────────────┤    ├─────────────────┤    ├─────────────────┤
│ id (PK)         │    │ id (PK)         │    │ id (PK)         │
│ name            │    │ name            │    │ name            │
│ email (Unique)  │    │ description     │    │ description     │
│ password_hash   │    │ price           │    │ parent_id (FK)  │
│ phone           │    │ category_id (FK)│    └─────────────────┘
│ created_at      │    │ stock_quantity  │
└─────────────────┘    │ created_at      │
         │              └─────────────────┘
         │                       │
         ▼                       ▼
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│     Orders      │    │    Payments     │    │     Carts       │
├─────────────────┤    ├─────────────────┤    ├─────────────────┤
│ id (PK)         │    │ id (PK)         │    │ id (PK)         │
│ user_id (FK)    │    │ order_id (FK)   │    │ user_id (FK)    │
│ total_amount    │    │ payment_status  │    │ product_id (FK) │
│ status          │    │ payment_method  │    │ quantity        │
│ created_at      │    │ stripe_id       │    │ created_at      │
└─────────────────┘    │ created_at      │    └─────────────────┘
                       └─────────────────┘
```

## 📁 Project Structure

```
UrbanCart/
├── 🎨 Frontend (React)
│   ├── src/
│   │   ├── components/          # Reusable UI components
│   │   ├── pages/               # Page components
│   │   ├── services/            # API service layer
│   │   ├── utils/               # Utility functions
│   │   └── App.js               # Main application component
│   ├── public/                  # Static assets
│   └── package.json             # Frontend dependencies
├── 🐍 Backend (Flask)
│   ├── src/
│   │   ├── models/              # Database models
│   │   ├── routes/              # API endpoints
│   │   ├── services/            # Business logic
│   │   ├── utils/               # Helper functions
│   │   └── app.py               # Flask application
│   ├── requirements.txt         # Python dependencies
│   └── Dockerfile              # Container configuration
├── 🗄️ Database
│   ├── migrations/              # Database schema changes
│   ├── seeds/                   # Sample data
│   └── schema.sql              # Database structure
├── 🐳 Docker
│   ├── docker-compose.yml      # Multi-container setup
│   ├── nginx.conf              # Reverse proxy config
│   └── Dockerfile              # Backend container
└── 📋 Documentation
    ├── README.md               # This file
    ├── API.md                  # API documentation
    └── DEPLOYMENT.md           # Deployment guide
```

## 🚀 Quick Start

### Prerequisites
- **Node.js 16+**
- **Python 3.8+**
- **Docker & Docker Compose**
- **AWS Account** (for RDS)
- **Stripe Account** (for payments)
- **Firebase Project** (for OTP)

### Installation

1. **Clone the Repository**
```bash
git clone https://github.com/omkar04gaikwad/UrbanCart.git
cd UrbanCart
```

2. **Backend Setup**
```bash
# Install Python dependencies
pip install -r requirements.txt

# Set environment variables
export DATABASE_URL="postgresql://user:pass@host:port/db"
export STRIPE_SECRET_KEY="<your_stripe_secret_key>"
export FIREBASE_API_KEY="<your_firebase_key>"
export JWT_SECRET_KEY="<your_jwt_token>"

# Initialize database
python src/models/model.py
```

3. **Frontend Setup**
```bash
cd frontend
npm install
npm start
```

4. **Docker Deployment**
```bash
# Build and start all services
docker-compose up --build -d

# Check running containers
docker ps
```

## 🔧 API Endpoints

### **Authentication**
```python
POST /api/users/register     # Register new user with OTP
POST /api/users/login        # Authenticate user (JWT)
POST /api/users/verify-otp   # Verify phone number
POST /api/users/logout       # Invalidate JWT token
```

### **Products**
```python
GET  /api/products/         # Get all products
GET  /api/products/{id}      # Get product details
GET  /api/categories/        # Get product categories
POST /api/products/search    # Search products
```

### **Cart & Orders**
```python
GET  /api/cart/{user_id}     # Get user's cart
POST /api/cart/add           # Add item to cart
PUT  /api/cart/update        # Update cart item
DELETE /api/cart/remove      # Remove cart item
POST /api/orders/create      # Create new order
GET  /api/orders/{user_id}   # Get user's orders
```

### **Payments**
```python
POST /api/payments/create-intent    # Create Stripe payment intent
POST /api/payments/confirm          # Confirm payment
POST /api/payments/webhook          # Stripe webhook handler
GET  /api/payments/{order_id}       # Get payment status
```

## 🛡️ Security Features

### **Authentication Security**
- **JWT Tokens**: Stateless authentication with configurable expiration
- **HTTP-Only Cookies**: Prevent XSS token theft
- **CSRF Protection**: Validate tokens on all state-changing requests
- **OTP Verification**: Multi-factor authentication via Firebase

### **Data Protection**
- **Password Hashing**: Bcrypt with salt rounds
- **SQL Injection Prevention**: SQLAlchemy ORM parameterized queries
- **XSS Protection**: Input sanitization and CSP headers
- **Encryption**: AES-256 at rest, SSL/TLS in transit

### **Payment Security**
- **Stripe Tokenization**: Never store raw payment data
- **Webhook Verification**: Validate Stripe webhook signatures
- **OTP Confirmation**: Additional verification before transactions
- **PCI Compliance**: Stripe handles PCI DSS requirements

## 📊 Testing & Security Validation

### **Security Testing Results**
- **SQL Injection**: All endpoints tested with SQLMap → returned 400 Bad Request (✅ Secure)
- **JWT Validation**: Enforced across all API endpoints (✅ Secure)
- **CSRF Protection**: Tokens validated for critical operations (✅ Secure)
- **XSS Prevention**: Input sanitization and CSP implemented (✅ Secure)

### **Performance Testing**
- **Load Testing**: Simulated high traffic scenarios
- **Database Performance**: Optimized queries and indexing
- **Container Scaling**: Docker Compose load balancing
- **API Response Times**: Sub-200ms for most endpoints

## 🎯 Use Cases

### **E-Commerce Applications**
- **Online Retail**: Complete shopping platform for retail businesses
- **Marketplace**: Multi-vendor e-commerce solution
- **Subscription Services**: Recurring payment management
- **Digital Products**: Software and media sales platform

### **Enterprise Solutions**
- **B2B Commerce**: Business-to-business transaction platform
- **Internal Stores**: Employee purchase systems
- **Partner Portals**: Vendor and supplier management
- **Custom Solutions**: Tailored e-commerce implementations

## 🚀 Future Enhancements

### **Security Improvements**
- **Multi-Factor Authentication**: Email + phone OTP for stronger authentication
- **Container Security**: Docker Bench or AWS Fargate integration
- **Domain & Certificates**: Route53 with CA-signed SSL certificates
- **Fraud Detection**: AI/ML-based anomaly detection for payment security

### **Feature Additions**
- **Advanced Analytics**: Sales reporting and business intelligence
- **Inventory Management**: Real-time stock tracking and alerts
- **Customer Support**: Integrated chat and ticket system
- **Mobile App**: React Native mobile application

### **Technical Upgrades**
- **Microservices**: Break down into smaller, independent services
- **Kubernetes**: Container orchestration for better scalability
- **CDN Integration**: Global content delivery network
- **Caching**: Redis for improved performance

## 🌍 Impact

UrbanCart serves as a **learning blueprint** for building secure, scalable, and production-ready e-commerce platforms. It showcases how to integrate modern technologies (React, Flask, PostgreSQL, Stripe, Docker, AWS) while applying **security-first principles** to protect sensitive user data and transactions.

### **Educational Value**
- **Security Best Practices**: Comprehensive implementation of web security
- **Modern Architecture**: Full-stack development with containerization
- **Payment Integration**: Real-world payment processing implementation
- **DevOps Practices**: Docker deployment and AWS cloud integration

### **Industry Relevance**
- **Production Ready**: Scalable architecture for real-world deployment
- **Security Focused**: Enterprise-grade security implementations
- **Technology Stack**: Industry-standard tools and frameworks
- **Best Practices**: Following modern development methodologies

## 👨‍💻 Author

**Omkar Gaikwad**
- **GitHub**: [@omkar04gaikwad](https://github.com/omkar04gaikwad)
- **Portfolio**: [omkar04gaikwad.github.io](https://omkar04gaikwad.github.io/Omkar_Gaikwad/)
- **LinkedIn**: [Connect with me](https://linkedin.com/in/omkar-gaikwad)

## 🤝 Contributing

We welcome contributions to improve this project! Please see our [Contributing Guidelines](CONTRIBUTING.md) for details.

### How to Contribute
1. **Fork the repository**
2. **Create a feature branch** (`git checkout -b feature/AmazingFeature`)
3. **Commit your changes** (`git commit -m 'Add some AmazingFeature'`)
4. **Push to the branch** (`git push origin feature/AmazingFeature`)
5. **Open a Pull Request**

### Areas for Contribution
- **Security Enhancements**: Additional security measures and testing
- **Feature Development**: New e-commerce functionality
- **Documentation**: Improved guides and tutorials
- **Testing**: Comprehensive test coverage
- **Performance**: Optimization and scalability improvements

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## ⚠️ Important Notes

### Security Considerations
- **Production Deployment**: Ensure proper SSL certificates and domain configuration
- **Environment Variables**: Never commit sensitive keys to version control
- **Database Security**: Use strong passwords and network security groups
- **Regular Updates**: Keep all dependencies updated for security patches

### Limitations
- **Demo Environment**: Current setup uses ngrok for HTTPS tunneling
- **Payment Testing**: Uses Stripe test mode for development
- **Scalability**: Single-instance deployment for demonstration purposes
- **Monitoring**: Basic logging without comprehensive monitoring stack

---

⭐ **Star this repository** if you find it helpful for e-commerce development!

🔔 **Watch for updates** to stay informed about new features and improvements.

📧 **Contact**: For questions, collaborations, or security feedback, please reach out through GitHub.

🛒 **Mission**: Building secure, scalable e-commerce solutions for the modern web.

# On-Campus Social Network

A comprehensive software engineering project following Agile/Scrum methodology to design, develop, and deploy a social networking platform specifically tailored for university campus communities. Built iteratively across 5 labs with full documentation of the development process.

## Table of Contents

- [Overview](#overview)
- [Project Structure](#project-structure)
- [Development Methodology](#development-methodology)
- [Lab Milestones](#lab-milestones)
- [Key Features](#key-features)
- [System Architecture](#system-architecture)
- [Getting Started](#getting-started)
- [Documentation](#documentation)
- [Technologies Used](#technologies-used)


## Overview

This project represents a complete software development lifecycle for building a campus-focused social networking application. The platform enables students, faculty, and staff to connect, collaborate, and engage within their university community.

### Project Goals

- **Community Building**: Foster connections within the campus ecosystem
- **Academic Collaboration**: Facilitate study groups and project collaboration
- **Event Management**: Share and discover campus events and activities
- **Resource Sharing**: Exchange academic resources, notes, and materials
- **Campus Engagement**: Increase participation in university life

### Target Users

- **Students**: Undergraduate, graduate, and exchange students
- **Faculty**: Professors, lecturers, and teaching assistants
- **Staff**: Administrative and support personnel
- **Alumni**: Graduated students maintaining campus connections

## Project Structure

```
On-Campus_Social-Network/
├── Lab 1/                         # Requirements & Planning
│   ├── SVN/                       # Version control artifacts
│   │   ├── requirements_spec.pdf  # Functional requirements
│   │   ├── use_cases.pdf          # Use case diagrams
│   │   └── user_stories.pdf       # Agile user stories
│   └── Archive/                   # Historical versions
├── Lab 2/                         # System Design
│   ├── SVN/
│   │   ├── architecture.pdf       # System architecture
│   │   ├── database_design.pdf    # ER diagrams, schema
│   │   ├── ui_mockups.pdf         # Interface designs
│   │   └── design_patterns.pdf    # Software patterns used
│   └── Archive/
├── Lab 3/                         # Implementation Sprint 1
│   ├── SVN/
│   │   ├── source_code/           # Backend and frontend code
│   │   ├── unit_tests/            # Test suites
│   │   └── sprint_retrospective.pdf
│   └── Archive/
├── Lab 4/                         # Implementation Sprint 2
│   ├── SVN/
│   │   ├── source_code/           # Continued development
│   │   ├── integration_tests/     # System integration tests
│   │   └── sprint_review.pdf
│   └── Archive/
├── Lab 5/                         # Testing & Deployment
│   ├── SVN/
│   │   ├── test_plans.pdf         # Comprehensive testing
│   │   ├── deployment_guide.pdf   # Production deployment
│   │   ├── user_manual.pdf        # End-user documentation
│   │   └── final_presentation.pdf
│   └── Archive/
├── Meeting Minutes/               # Scrum ceremonies documentation
│   ├── Lab 1/
│   ├── Lab 2/
│   ├── Lab 3/
│   ├── Lab 4/
│   └── Lab 5/
├── Informal Meeting Notes/        # Team discussions
├── Inspiration - TeamBacklog.xlsx # Product backlog management
├── .gitignore
├── LICENSE
└── README.md
```

## Development Methodology

### Agile/Scrum Framework

This project follows Agile principles with Scrum ceremonies:

**Sprint Structure:**
- **Sprint Duration**: 2 weeks per lab
- **Total Sprints**: 5 (aligned with lab milestones)
- **Team Size**: 4-6 members

**Scrum Ceremonies:**

1. **Sprint Planning** (documented in Meeting Minutes)
   - Review product backlog
   - Select user stories for sprint
   - Define sprint goals and acceptance criteria
   - Estimate story points

2. **Daily Standups** (documented in Informal Meeting Notes)
   - What did I accomplish yesterday?
   - What will I do today?
   - Any blockers or impediments?

3. **Sprint Review** (end of each lab)
   - Demo completed features
   - Gather stakeholder feedback
   - Update product backlog

4. **Sprint Retrospective** (documented in each lab)
   - What went well?
   - What could be improved?
   - Action items for next sprint

### Version Control Strategy

- **Trunk-Based Development**: Single main branch with feature branches
- **Commit Conventions**: Descriptive messages with task IDs
- **Code Reviews**: Peer review before merging
- **SVN Integration**: Documented in each lab's SVN folder

## Lab Milestones

### Lab 1: Requirements Gathering & Planning

**Duration**: Weeks 1-2  
**Focus**: Understanding user needs and project scope

**Deliverables:**
- Product vision statement
- User personas and scenarios
- Functional and non-functional requirements
- Use case diagrams
- Initial product backlog
- Project charter

**Key Activities:**
- Stakeholder interviews
- Market research (competitive analysis)
- Requirements elicitation workshops
- Priority ranking with MoSCoW method

**User Stories Examples:**
```
US-001: As a student, I want to create a profile 
        so that I can connect with classmates.
        (Priority: Must Have, Points: 5)

US-002: As a faculty member, I want to create study groups 
        so that students can collaborate on coursework.
        (Priority: Should Have, Points: 8)

US-003: As a user, I want to see a news feed 
        so that I can stay updated on campus activities.
        (Priority: Must Have, Points: 13)
```

### Lab 2: System Design & Architecture

**Duration**: Weeks 3-4  
**Focus**: Technical design and architecture decisions

**Deliverables:**
- System architecture diagram
- Database schema and ER diagrams
- API design and documentation
- UI/UX mockups and wireframes
- Technology stack selection
- Security architecture

**Architecture Components:**

```
┌─────────────────────────────────────────┐
│          Presentation Layer             │
│   (React Frontend, Mobile Apps)         │
└──────────────┬──────────────────────────┘
               │
┌──────────────▼──────────────────────────┐
│          Application Layer              │
│   (REST API, Business Logic)            │
│   - User Management Service             │
│   - Content Service                     │
│   - Messaging Service                   │
│   - Notification Service                │
└──────────────┬──────────────────────────┘
               │
┌──────────────▼──────────────────────────┐
│            Data Layer                   │
│   (PostgreSQL, Redis Cache)             │
│   - User Database                       │
│   - Content Database                    │
│   - Message Queue                       │
└─────────────────────────────────────────┘
```

**Design Patterns Used:**
- **MVC**: Separation of concerns
- **Repository Pattern**: Data access abstraction
- **Observer Pattern**: Real-time notifications
- **Singleton Pattern**: Database connections
- **Factory Pattern**: Object creation

### Lab 3: Implementation Sprint 1

**Duration**: Weeks 5-6  
**Focus**: Core functionality development

**Features Implemented:**
- User authentication and authorization
- Profile creation and management
- Friend connections and requests
- Basic news feed
- Post creation and sharing

**Code Example - User Authentication:**

```python
from flask import Blueprint, request, jsonify
from werkzeug.security import generate_password_hash, check_password_hash
from models import User, db
from auth import generate_token

auth_bp = Blueprint('auth', __name__)

@auth_bp.route('/register', methods=['POST'])
def register():
    """User registration endpoint"""
    data = request.get_json()
    
    # Validate required fields
    required_fields = ['email', 'password', 'first_name', 'last_name']
    if not all(field in data for field in required_fields):
        return jsonify({'error': 'Missing required fields'}), 400
    
    # Check if user exists
    if User.query.filter_by(email=data['email']).first():
        return jsonify({'error': 'User already exists'}), 409
    
    # Create new user
    user = User(
        email=data['email'],
        password_hash=generate_password_hash(data['password']),
        first_name=data['first_name'],
        last_name=data['last_name'],
        university_id=data.get('university_id')
    )
    
    db.session.add(user)
    db.session.commit()
    
    # Generate JWT token
    token = generate_token(user.id)
    
    return jsonify({
        'user': user.to_dict(),
        'token': token
    }), 201

@auth_bp.route('/login', methods=['POST'])
def login():
    """User login endpoint"""
    data = request.get_json()
    
    user = User.query.filter_by(email=data.get('email')).first()
    
    if not user or not check_password_hash(user.password_hash, data.get('password')):
        return jsonify({'error': 'Invalid credentials'}), 401
    
    token = generate_token(user.id)
    
    return jsonify({
        'user': user.to_dict(),
        'token': token
    }), 200
```

**Testing:**
- Unit tests for all API endpoints
- Integration tests for authentication flow
- Code coverage: 85%+

### Lab 4: Implementation Sprint 2

**Duration**: Weeks 7-8  
**Focus**: Advanced features and integrations

**Features Implemented:**
- Real-time messaging system
- Event creation and RSVP
- Study group formation
- File sharing and resources
- Notification system
- Search functionality

**Code Example - Real-Time Messaging:**

```javascript
// WebSocket integration for real-time chat
import io from 'socket.io-client';

class MessagingService {
  constructor() {
    this.socket = null;
    this.messageHandlers = [];
  }
  
  connect(userId, token) {
    this.socket = io('http://localhost:5000', {
      auth: { token }
    });
    
    this.socket.on('connect', () => {
      console.log('Connected to messaging server');
      this.socket.emit('join', { userId });
    });
    
    this.socket.on('new_message', (message) => {
      this.messageHandlers.forEach(handler => handler(message));
    });
    
    this.socket.on('user_typing', (data) => {
      this.handleTypingIndicator(data);
    });
  }
  
  sendMessage(conversationId, content) {
    this.socket.emit('send_message', {
      conversation_id: conversationId,
      content: content,
      timestamp: new Date().toISOString()
    });
  }
  
  onMessage(handler) {
    this.messageHandlers.push(handler);
  }
  
  disconnect() {
    if (this.socket) {
      this.socket.disconnect();
    }
  }
}

export default new MessagingService();
```

**Performance Optimization:**
- Database query optimization
- Caching strategy implementation
- CDN for static assets
- Lazy loading for images

### Lab 5: Testing, Deployment & Documentation

**Duration**: Weeks 9-10  
**Focus**: Quality assurance and production readiness

**Testing Strategy:**

1. **Unit Testing**
   - Individual component tests
   - API endpoint testing
   - Coverage: 90%+

2. **Integration Testing**
   - End-to-end user flows
   - Service integration tests
   - Database transaction tests

3. **System Testing**
   - Performance testing (load, stress)
   - Security testing (penetration, vulnerability)
   - Usability testing with real users

4. **Acceptance Testing**
   - User acceptance criteria validation
   - Stakeholder sign-off
   - Beta testing with student group

**Deployment Pipeline:**

```yaml
# CI/CD Pipeline (GitHub Actions)
name: Deploy

on:
  push:
    branches: [main]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Run tests
        run: |
          npm install
          npm test
          
  build:
    needs: test
    runs-on: ubuntu-latest
    steps:
      - name: Build Docker image
        run: docker build -t campus-network .
        
  deploy:
    needs: build
    runs-on: ubuntu-latest
    steps:
      - name: Deploy to production
        run: |
          kubectl apply -f k8s/
          kubectl rollout status deployment/campus-network
```

**Documentation Delivered:**
- Technical architecture document
- API reference documentation
- User manual and tutorials
- Deployment guide
- Maintenance and troubleshooting guide

## Key Features

### User Management
- Registration with university email verification
- Profile customization (bio, interests, major)
- Privacy settings and visibility controls
- Role-based access (student, faculty, staff)

### Social Networking
- Friend connections and follower system
- News feed with algorithmic ranking
- Post creation (text, images, links)
- Likes, comments, and shares
- Profile discovery and search

### Academic Collaboration
- Study group creation and management
- Course-specific discussion boards
- Resource sharing (notes, slides, documents)
- Collaborative document editing
- Calendar integration

### Messaging & Communication
- Real-time one-on-one messaging
- Group chat functionality
- File sharing in conversations
- Typing indicators and read receipts
- Push notifications

### Events & Activities
- Event creation and promotion
- RSVP and attendance tracking
- Calendar integration
- Event discovery and recommendations
- Photo sharing from events

### Campus Integration
- University course catalog integration
- Campus map and location services
- Dining hall menus and hours
- Library resource links
- Administrative announcements

## System Architecture

### Technology Stack

**Frontend:**
- React.js for web application
- React Native for mobile apps
- Redux for state management
- Material-UI for components
- Socket.io-client for real-time features

**Backend:**
- Python/Flask for REST API
- Node.js for WebSocket server
- PostgreSQL for relational data
- Redis for caching and sessions
- Celery for background tasks

**Infrastructure:**
- Docker for containerization
- Kubernetes for orchestration
- AWS/GCP for cloud hosting
- Nginx for reverse proxy
- GitHub Actions for CI/CD

### Database Schema

```sql
-- Users table
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    email VARCHAR(255) UNIQUE NOT NULL,
    password_hash VARCHAR(255) NOT NULL,
    first_name VARCHAR(100) NOT NULL,
    last_name VARCHAR(100) NOT NULL,
    university_id VARCHAR(50),
    role VARCHAR(20) DEFAULT 'student',
    profile_picture_url TEXT,
    bio TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Friendships table
CREATE TABLE friendships (
    id SERIAL PRIMARY KEY,
    user_id INTEGER REFERENCES users(id),
    friend_id INTEGER REFERENCES users(id),
    status VARCHAR(20) DEFAULT 'pending',
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    UNIQUE(user_id, friend_id)
);

-- Posts table
CREATE TABLE posts (
    id SERIAL PRIMARY KEY,
    user_id INTEGER REFERENCES users(id),
    content TEXT NOT NULL,
    image_url TEXT,
    visibility VARCHAR(20) DEFAULT 'friends',
    likes_count INTEGER DEFAULT 0,
    comments_count INTEGER DEFAULT 0,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Events table
CREATE TABLE events (
    id SERIAL PRIMARY KEY,
    creator_id INTEGER REFERENCES users(id),
    title VARCHAR(255) NOT NULL,
    description TEXT,
    location VARCHAR(255),
    start_time TIMESTAMP NOT NULL,
    end_time TIMESTAMP NOT NULL,
    max_attendees INTEGER,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### Security Measures

- **Authentication**: JWT tokens with refresh mechanism
- **Authorization**: Role-based access control (RBAC)
- **Data Protection**: HTTPS/TLS for all communications
- **Input Validation**: Sanitization to prevent XSS/SQL injection
- **Rate Limiting**: Prevent API abuse
- **Password Security**: Bcrypt hashing with salt
- **CORS**: Configured cross-origin policies
- **GDPR Compliance**: Data privacy and user rights

## Getting Started

### Prerequisites

```bash
Python 3.9+
Node.js 16+
PostgreSQL 13+
Redis 6+
Docker (optional)
```

### Installation

```bash
# Clone the repository
git clone https://github.com/manav-ar/On-Campus_Social-Network.git
cd On-Campus_Social-Network

# Backend setup
cd backend
python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate
pip install -r requirements.txt

# Database setup
createdb campus_network
python manage.py db upgrade

# Frontend setup
cd ../frontend
npm install

# Environment variables
cp .env.example .env
# Edit .env with your configuration
```

### Running the Application

```bash
# Start backend (terminal 1)
cd backend
python app.py

# Start frontend (terminal 2)
cd frontend
npm start

# Start WebSocket server (terminal 3)
cd websocket
npm start
```

Access the application at `http://localhost:3000`


## Documentation

All project documentation is organized by lab milestone:

- **Lab 1**: Requirements specifications, use cases, user stories
- **Lab 2**: System design, architecture diagrams, database schemas
- **Lab 3**: Sprint 1 code, unit tests, retrospective
- **Lab 4**: Sprint 2 code, integration tests, review
- **Lab 5**: Test plans, deployment guide, user manual

**Meeting Minutes** folder contains detailed notes from all Scrum ceremonies.

## Technologies Used

### Development
- **Languages**: Python, JavaScript, SQL
- **Frameworks**: Flask, React, Redux
- **Database**: PostgreSQL, Redis
- **Real-time**: Socket.io, WebSockets

### Testing
- **Unit Testing**: pytest, Jest
- **Integration Testing**: Postman, Selenium
- **Load Testing**: JMeter, Locust
- **Code Quality**: ESLint, Pylint, SonarQube

### DevOps
- **Containerization**: Docker, Docker Compose
- **Orchestration**: Kubernetes
- **CI/CD**: GitHub Actions, Jenkins
- **Monitoring**: Prometheus, Grafana
- **Logging**: ELK Stack (Elasticsearch, Logstash, Kibana)

## Future Enhancements

- **Mobile Application**: Native iOS and Android apps
- **AI Recommendations**: Personalized content and connections
- **Video Chat**: Integrated video calling for study groups
- **Gamification**: Points, badges, and leaderboards
- **Analytics Dashboard**: Usage statistics for administrators
- **Multi-University**: Expand beyond single campus
- **Marketplace**: Buy/sell textbooks and course materials
- **Career Services**: Job postings and networking


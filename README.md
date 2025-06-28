# Scaling Conference Room Reservation Systems in Cloud Environments: Analysis of Architectural Approaches and Expansion Strategies

## 📋 About This Work

This repository contains a master's thesis that analyzes the practical implementation of a conference room reservation system through the lens of modern cloud-native technologies and architectural approaches. The work explores when and why certain architectural approaches become justified based on business requirements and technical constraints.

### 🎯 Objectives

- **Evaluate architectural approaches** - Comprehensive analysis of monolithic vs microservices architecture
- **Define scaling strategies** - Concrete plans for horizontal and vertical system scaling
- **Analyze cloud-native best practices** - CI/CD pipelines, containerization, and deployment patterns
- **Provide practical recommendations** - Guidelines for architecture decision-making in similar projects

## 🏗️ System Implementation

### Features
- **Authentication**: JWT-based auth with role-based access (USER/MANAGER)
- **Reservations**: Calendar-based interface with conflict detection and cleanup intervals
- **Email notifications**: SMTP automation for lifecycle events
- **Management**: CRUD operations with MySQL persistence

### Tech Stack
- **Backend**: Java/Spring Boot
- **Database**: MySQL 8.0
- **Containerization**: Docker + Docker Compose
- **CI/CD**: GitHub Actions
- **Cloud**: Netcup VPS
- **Frontend**: React (separate repository)

### Architecture
```
┌─────────────────────────────────┐    ┌─────────────────────────────────┐
│         Application             │    │          Database               │
│      Container (Spring)         │◄──►│       Container (MySQL)         │
│  ┌─────────┬─────────┬────────┐ │    │                                 │
│  │  Auth   │Booking  │ Email  │ │    │   - Users                       │
│  │Service  │Service  │Service │ │    │   - Reservations                │
│  └─────────┴─────────┴────────┘ │    │   - Working_Hours               │
└─────────────────────────────────┘    └─────────────────────────────────┘
              Docker Network: conf_room_network
```

## 📊 Thesis Structure

### 1. Introduction
- Problem and motivation
- Technologies and approach
- Objectives and methodology

### 2. Architectural Patterns: Monolith vs Microservices
- Theoretical foundations
- Comparative analysis
- Decision-making factors

### 3. System Description and Implementation
- System functionality
- Current architecture
- CI/CD automation
- Cloud deployment

### 4. Rationale for Choosing Monolithic Architecture
- Context analysis
- Advantages in given context
- Critical evaluation

### 5. Scalability and Future Modularization
- Horizontal monolith scaling
- Transition to microservices
- Inter-service communication
- Kubernetes orchestration

### 6. Conclusion
- Key findings
- Practical contributions
- Final considerations

## 🔑 Key Findings

### Context-Driven Architecture
The choice of monolithic architecture was justified by specific constraints:
- **Team size**: 2 developers (frontend + backend/DevOps)
- **Timeline**: 1.5 months development
- **Traffic**: 10s of concurrent users
- **Scope**: Single building, single conference room

### Performance Insights
- **In-process communication**: ~100μs latency
- **HTTP API calls**: ~10ms latency
- **Deployment automation**: 15min → 3min reduction

### Decision Framework
| **Factor** | **Monolith** | **Microservices** |
|------------|--------------|------------------|
| Team size | < 5 | > 10 |
| Traffic | < 100 users | > 1000 users |
| Deploy frequency | Weekly | Daily/Hourly |
| Geographic scope | Single region | Multi-region |

## 🚀 Migration Strategy

### Gradual Decomposition (Strangler Fig Pattern)
1. **Phase 1**: Email Service extraction (lowest coupling)
2. **Phase 2**: Auth Service separation + API Gateway
3. **Phase 3**: Complete microservices decomposition

### Trigger Points
- **100+ concurrent users**: Horizontal scaling with load balancer
- **1000+ concurrent users**: Microservices architecture justified
- **Team > 5 people**: Service boundaries enable parallel development

## 🎓 Academic Information

- **University**: Faculty of Computer Science, Union University
- **Program**: Master's Studies
- **Course**: Cloud Computing
- **Supervisor**: Prof. Mira Radivojević
- **Year**: 2024/2025

## 📄 License

This work was created for academic purposes. All code and documentation are available under the MIT license for educational and research purposes.

---

**Keywords**: cloud computing, microservices, monolith architecture, Docker, Spring Boot, scalability, CI/CD, architectural patterns

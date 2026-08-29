# ADR-001: Modular Monolith

## Status

Accepted

## Context

TravelAI is initially being developed as a single application.

The platform will contain multiple business domains including:

- Authentication
- Hotel Management
- Hotel Search
- Booking
- Payments
- Reviews
- Notifications
- AI Travel Planning

Although these domains are logically separate, the initial scale and development team do not justify deploying each domain as an independent microservice.

Introducing microservices too early would add operational and distributed-system complexity such as:

- Network communication
- Service discovery
- Distributed tracing
- Independent deployments
- Failure handling between services
- Data consistency across services
- Infrastructure and monitoring overhead

## Decision

We will initially implement TravelAI as a modular monolith.

The application will be deployed as one Spring Boot application, but the codebase will be organized around business modules.

Example:

com.travelai.agent

├── auth
├── user
├── hotel
├── room
├── booking
├── review
├── payment
├── notification
└── ai

Each module should have clear responsibilities and minimize unnecessary coupling with other modules.

## Consequences

### Advantages

- Simple deployment
- Low infrastructure overhead
- Easy local development
- Simple database transactions
- Easier debugging
- Clear business boundaries
- Easier initial development

### Disadvantages

- Application is still deployed as one unit
- Poor module boundaries could create a tightly coupled codebase
- Individual modules cannot scale independently
- A failure in the application can affect all modules

## Future Evolution

If specific modules develop independent scaling, deployment, or operational requirements, they may later be extracted into microservices.

Potential candidates include:

- Search
- Notification
- AI services
- Recommendation engine
- Payment processing

The migration to microservices should be driven by actual requirements rather than premature optimization.
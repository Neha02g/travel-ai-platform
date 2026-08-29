# ADR-002: PostgreSQL as Primary Database

## Status

Accepted

## Context

TravelAI requires persistent storage for:

- Users
- Hotels
- Rooms
- Bookings
- Reviews
- Payments

The booking domain requires strong consistency and transactional guarantees.

The system also contains highly relational data:

User → Booking → Room → Hotel

and:

Hotel → Reviews

## Decision

We will use PostgreSQL as the primary transactional database.

PostgreSQL will be the source of truth for transactional business data.

## Why PostgreSQL

PostgreSQL provides:

- ACID transactions
- Foreign keys
- Constraints
- Indexes
- Strong consistency
- Row-level locking
- Rich SQL querying
- Excellent support for relational data

These capabilities are particularly important for booking and inventory management.

## Consequences

### Advantages

- Strong transactional guarantees
- Referential integrity
- Mature ecosystem
- Powerful query capabilities
- Suitable for booking and payment state management

### Disadvantages

- Horizontal scaling is more complex than simply adding application servers
- Schema changes require migration management
- Very high-scale search workloads may require specialized systems

## Future Evolution

Additional systems may be introduced for specialized workloads:

- Redis for caching and temporary holds
- Elasticsearch for advanced hotel search
- S3 for images/documents
- Kafka for asynchronous event processing

PostgreSQL remains the source of truth for transactional data.
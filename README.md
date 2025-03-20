# What's Fresh Documentation

## Overview
What's Fresh is a traceability solution designed for small-scale food producers and artisanal makers. In response to FDA's Food Traceability Final Rule, the application simplifies ingredient tracking from procurement through production, ensuring regulatory compliance without overwhelming administrative overhead.

### Key Features
- Ingredient batch tracking
- Product recipe management 
- Production batch documentation
- Automated traceability reports
- Multi-account support

### System Architecture
The application uses a multi-tier architecture:
1. Source database (`whatsfresh`) stores core business data
2. API database (`api_wf`) provides optimized views for data access
3. Server processes handle business logic and event management
4. Client interface delivers intuitive maker-focused workflows

## Project Structure
```mermaid
graph LR
    A[Whatsfresh] --> DB[db.whatsfresh]
    DB[db.api_wf] --> |dbViews|DBV[db.api_wf]
    DBV --> C[Server/APIs]
    C --> |listEvents|B[Client] 
    B --> |DML Requests|C
```

### Client Documentation (`/client`)
- **architecture/** - System design and patterns
  - State management
  - Event system
  - Authentication flow
- **components/** - Reusable component specifications
  - CRUD operations
  - Common components
- **pages/** - Page-specific flows and implementations

### Server Documentation (`/server`)
- **api/** - API endpoints and protocols
- **architecture/** - Backend system design
- **database/** 
  - [Database Schema](./server/database/MySQL.mmd)
  - Event types
  - Schema design
  - Stored procedures

## Quick Navigation
- [Client Architecture](./client/architecture/)
- [Server Database](./server/database/)
- [API Documentation](./server/api/)


1. Create new documentation:
   - Follow existing templates
   - Use Markdown formatting
   - Include Mermaid diagrams where helpful
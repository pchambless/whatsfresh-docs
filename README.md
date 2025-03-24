# What's Fresh Today?

## Overview
Whatfresh is a traceability solution designed for small-scale food producers and artisanal makers. In response to the FDA's Food Traceability Final Rule, the application simplifies ingredient tracking from procurement through production—ensuring regulatory compliance without overwhelming administrative overhead.

### Key Features
- Ingredient batch tracking
- Product recipe management 
- Production batch documentation
- Automated traceability reports
- Multi-account support

### System Architecture
The application uses a multi-tier architecture:
1. **MySQL Operational Database (whatsfresh):** Stores core business data.
2. **API Database Views (api_wf):** Provides optimized views for data access.
3. **Server Processes:** Handle business logic and event management.
4. **Client Interface:** Delivers intuitive maker-focused workflows.

#### Quick Navigation
- [Whatsfresh](#1-whatsfresh)
- [db.whatsfresh](#2-dbwhatsfresh)
- [db.api_wf - dbViews](#3-dbapi_wf---dbviews)
- [Server/APIs](#4-serverapis)
- [Client](#5-client)

## High Level Project Structure
```mermaid
graph LR
    A[Whatsfresh] --> DB[db.whatsfresh]
    DB --> DBV[db.api_wf - dbViews]
    DBV --> C[Server/APIs]
    C --> |listEvents| B[Client] 
    B --> |DML Requests| C
```

---

### 1. Whatsfresh
*Description:*  
This represents the overall application and serves as the top-level entity in our architecture.

*Details to add:*  
- Application purpose  
- High-level components  
- How it interconnects with the underlying databases

---
### 2. db.whatsfresh - Database operational tables.

*Description:*  
This database stores the primary, operational data for WhatFresh. It uses both tables and views (to normalize data for reporting purposes).

[See Table List...](./docs/database/db_whatsfresh.md)

---

### 3. db.api_wf - dbViews
*Description:*  
This database stores API-optimized views derived from the whatsfresh database. These views provide a simplified and performance-tuned representation of the underlying data, helping to support reporting and external API consumption.

[See View List...](./docs/database/db_api_wf.md)

*Other Details to add:*  
- Overview of source-to-view mappings  
- How these views are consumed by the API layer  
- Update strategies, caching, or refresh schedules

---

### 4. Server/APIs
*Description:*  
This layer implements business logic and exposes data through APIs. It processes event data and manages traceability workflows.

**Server Components Flowchart:**

[Component Flowchart](./docs/server/FlowChart.md)

---

### 5. Client
*Description:*  
The client interface delivers maker-focused workflows with interactive screens for traceability tasks.

*Details to add:*  
- UI overview  
- Key components and page flows  
- How the client consumes data from the server APIs

---

## Quick Navigation
- [Client Architecture](./client/architecture/)
- [Server Database](./server/database/)
- [API Documentation](./server/api/)

---

## Data Flow
Below is the detailed database flow diagram showing how data flows from the source tables to API views and then into the server for event processing. The EventTypes generated are then utilized by the Client for various operations.

```mermaid
graph LR
    %% Database subgraphs
    subgraph WhatsFresh[whatsfresh DB]
        direction LR
        accounts[accounts]
        users[users]
        measures[global_measure_units]
        acc_users[accounts_users]
        ingr_types[ingredient_types]
        brands[brands]
        ingr_batches[ingredient_batches]
        ingredients[ingredients]
        prod_batches[product_batches]
        products[products]
        prod_types[product_types]
        prod_recipes[product_recipes]
        tasks[tasks]
        vendors[vendors]
        workers[workers]
    end

    subgraph API_WF[api_wf DB Views]
        direction LR
        acctList_view[("acctList")]
        userList_view[("userList")]
        measList_view[("measList")]
        ingrTypeList_view[("ingrTypeList")]
        brndList_view[("brndList")]
        ingrBtchList_view[("ingrBtchList")]
        ingrList_view[("ingrList")]
        prodBtchList_view[("prodBtchList")]
        prodList_view[("prodList")]
        prodTypeList_view[("prodTypeList")]
        rcpeList_view[("rcpeList")]
        taskList_view[("taskList")]
        vndrList_view[("vndrList")]
        wrkrList_view[("wrkrList")]
        userAcctList_view[("userAcctList")]
    end

    subgraph WF_Server[WF-Server EventTypes]
        direction LR
        acctList[acctList]
        userList[userList]
        measList[measList]
        ingrTypeList[ingrTypeList]
        brndList[brndList]
        ingrBtchList[ingrBtchList]
        ingrList[ingrList]
        prodBtchList[prodBtchList]
        prodList[prodList]
        prodTypeList[prodTypeList]
        rcpeList[rcpeList]
        taskList[taskList]
        vndrList[vndrList]
        wrkrList[wrkrList]
        userAcctList[userAcctList]
    end

    %% Database to View relationships
    accounts --> |"source"| acctList_view
    users --> |"source"| userList_view
    measures --> |"source"| measList_view
    ingr_types --> |"source"| ingrTypeList_view
    brands --> |"source"| brndList_view
    ingr_batches --> |"source"| ingrBtchList_view
    ingredients --> |"source"| ingrList_view
    prod_batches --> |"source"| prodBtchList_view
    products --> |"source"| prodList_view
    prod_types --> |"source"| prodTypeList_view
    prod_recipes --> |"source"| rcpeList_view
    tasks --> |"source"| taskList_view
    vendors --> |"source"| vndrList_view
    workers --> |"source"| wrkrList_view
    users & acc_users & accounts --> |"source"| userAcctList_view

    %% View to Server EventType relationships
    acctList_view --> |"⚡"| acctList
    userList_view --> |"⚡"| userList
    measList_view --> |"⚡"| measList
    ingrTypeList_view --> |"⚡"| ingrTypeList
    brndList_view --> |"⚡"| brndList
    ingrBtchList_view --> |"⚡"| ingrBtchList
    ingrList_view --> |"⚡"| ingrList
    prodBtchList_view --> |"⚡"| prodBtchList
    prodList_view --> |"⚡"| prodList
    prodTypeList_view --> |"⚡"| prodTypeList
    rcpeList_view --> |"⚡"| rcpeList
    taskList_view --> |"⚡"| taskList
    vndrList_view --> |"⚡"| vndrList
    wrkrList_view --> |"⚡"| wrkrList
    userAcctList_view --> |"⚡"| userAcctList
```

---

## Creating New Documentation
- Follow the existing templates and style.
- Use Markdown for text and Mermaid for diagrams.
- Expand each section as the project evolves.

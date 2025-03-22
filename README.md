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

### 2. db.whatsfresh
*Description:*  
This database stores the primary, operational data for WhatFresh. It uses both tables and views (to normalize data for reporting purposes).

*Global Tables:*
- **<span style="color:#00008B;">accounts</span>** – Stores account and customer information.
- **<span style="color:#00008B;">users</span>** – Contains maker and administrative users.
- **<span style="color:#00008B;">global_measure_units</span>** – Defines standardized measurement units.
- **<span style="color:#00008B;">accounts_users</span>** – Maps users to their accounts.

*Account Tables:*
- **<span style="color:#00008B;">brands</span>** – Lists brands for products and ingredients.
- **<span style="color:#00008B;">vendors</span>** – Stores vendor information.
- **<span style="color:#00008B;">workers</span>** – Contains data on production workers.
  
*Ingredient Tables:*
- **<span style="color:#00008B;">ingredient_types</span>** – Catalogs types of ingredients.
- **<span style="color:#00008B;">ingredient_batches</span>** – Tracks purchase and usage of ingredients.
- **<span style="color:#00008B;">ingredients</span>** – Stores detailed ingredient data.
  
*Product Tables:*
- **<span style="color:#00008B;">product_types</span>** – Classifies products.
- **<span style="color:#00008B;">tasks</span>** – Details the tasks involved with a Product Type.
- **<span style="color:#00008B;">products</span>** – Contains the list of an Account's product line.
- **<span style="color:#00008B;">product_recipes</span>** – Manages recipes and formulations.
- **<span style="color:#00008B;">product_batches</span>** – Documents production batches.

*Product Batch Mapping:*
- **<span style="color:#00008B;">product_batch_ingredients</span>** – Maps Ingredient batches to Product Batches.
- **<span style="color:#00008B;">product_batch_tasks</span>** – Details task information (steps, workers, measurements, etc.) for production.

*Other Details to add:*  
- Data sources and update frequency  
- Backup and recovery considerations

---

### 3. db.api_wf - dbViews
*Description:*  
This holds the API-optimized views derived from the whatsfresh database. These views provide a simplified and performance-tuned representation of the underlying data.

*Details to add:*  
- Overview of key views (e.g., acctList, userList, etc.)  
- Source-to-view mappings  
- How these views are used by the API layer

<details>
  <summary>View Data Flow for db.api_wf - dbViews</summary>

  ```mermaid
  graph LR
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
  ```
</details>

---

### 4. Server/APIs
*Description:*  
This layer implements business logic and exposes data through APIs. It processes event data and manages traceability workflows.

**Server Components Flowchart:**

```mermaid
flowchart LR

subgraph 0["server"]
    1["app.js"]
    subgraph 2["controller"]
        3["Initialize.js"]
        4["execEventType.js"]
        B["fetchApiColumns.js"]
        E["fetchEventTypes.js"]
        F["listRegisteredRoutes.js"]
        G["queryResolver.js"]
        H["restartServer.js"]
        J["userLogin.js"]
    end
    subgraph K["middleware"]
        L["apiColumns.js"]
        M["eventRoutes.js"]
    end
    subgraph N["routes"]
        O["index.js"]
        R["registerRoutes.js"]
    end
    Z["server.js"]
    subgraph 13["utils"]
        14["db.js"]
        15["dbConfig.js"]
        16["dbUtils.js"]
        17["queryResolver.js"]
    end
end

subgraph 5["@middleware"]
    6["eventRoutes"]
end
subgraph 7["@utils"]
    8["dbConfig"]
    9["dbUtils"]
    A["queryResolver"]
end
C["fs"]
D["path"]
I["child_process"]
subgraph P["@routes"]
    Q["registerRoutes"]
end
subgraph S["@controller"]
    T["execEventType"]
    U["fetchApiColumns"]
    V["fetchEventTypes"]
    W["initialize"]
    X["listRegisteredRoutes"]
    Y["restartServer"]
end
subgraph 10["@root"]
    subgraph 11["server"]
        12["app"]
    end
end

4-->6
4-->8
4-->9
4-->A
B-->9
B-->C
B-->D
E-->C
E-->D
G-->6
G-->9
H-->I
J-->9
O-->Q
R-->T
R-->U
R-->V
R-->W
R-->X
R-->Y
Z-->U
Z-->V
Z-->12
Z-->Q
```

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

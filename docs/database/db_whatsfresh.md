
**Global Tables:**
- **accounts** – Stores account and customer information.
- **users** – Contains maker and administrative users.
- **global_measure_units** – Defines standardized measurement units.
- **accounts_users** – Maps users to their accounts.

**Account Tables:**
- **brands** – Lists brands for products and ingredients.
- **vendors** – Stores vendor information.
- **workers** – Contains data on production workers.

**Ingredient Tables:**
- **ingredient_types** – Catalogs types of ingredients.
- **ingredient_batches** – Tracks purchase and usage of ingredients.
- **ingredients** – Stores detailed ingredient data.

**Product Tables:**
- **product_types** – Classifies products.
- **tasks** – Details the tasks involved with a Product Type.
- **products** – Contains the list of an Account's product line.
- **product_recipes** – Manages recipes and formulations.
- **product_batches** – Documents production batches.

**Product Batch Mapping:**
- **product_batch_ingredients** – Maps ingredient batches to production batches.
- **product_batch_tasks** – Details task information (steps, workers, measurements, etc.) for production.

*Other Details to add:*  
- Data sources and update frequency  
- Backup and recovery considerations
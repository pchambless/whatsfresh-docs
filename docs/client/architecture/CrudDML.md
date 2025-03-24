# CRUD/DML Module

This module is responsible for preparing the request body for data manipulation (INSERT, UPDATE, DELETE) to be sent back to the server for execution. It takes in the columnMap for the listEvent of each Page/Tab and ensures that the appropriate data is included for the DML request.

## Operations

1. **INSERT**  
   The visible form fields are passed in the request body (no KeyField) along with the target table (dbTable) that will receive the new record.
   
2. **UPDATE**  
   The visible form fields are passed in the request body (including the KeyField) along with the target table (dbTable) that will be updated.
   
3. **DELETE**  
   Only the KeyField and dbTable are passed in the request body. The **server** will determine whether the row can be deleted directly or if a soft delete is necessary due to referential integrity restrictions.
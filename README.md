# CST8917 Lab 1: Building Azure Function Apps with Output Bindings

## 👨‍💻 Objective

This lab demonstrates how to build and deploy two Azure Function Apps using Python and Visual Studio Code with **output bindings** to:
- Azure Storage Queues
- Azure SQL Database

---

## 📁 Project Structure

lab1-8917/
│
├── AzureFunctionsToQueue/              
│   ├── .venv/                         
│   ├── HttpTriggerQueue/__init__.py     
│   ├── function_app.py                  
│   ├── local.settings.json              
│   ├── requirements.txt                 
│   ├── host.json                       
│   └── .funcignore                      
│
├── AzureFunctionsToSQL/                
│   ├── .venv/                          
│   ├── QueueTriggerSQL/__init__.py      
│   ├── function_app.py                  
│   ├── local.settings.json              
│   ├── requirements.txt                 
│   ├── host.json                        
│   └── .funcignore                     
│
└── README.md                            


---

## ⚙️ Setup Instructions

# Creating and Extending Azure Functions with Python in Visual Studio Code

## Quickstart: Creating a Python Azure Function in VS Code

This project demonstrates how to build and extend an Azure Function with Python using Visual Studio Code, following the Python v2 programming model (decorators for triggers and bindings).

---

## Environment Configuration

- **Azure Account** with active subscription
- **Python 3.10** installed
- **Visual Studio Code**
- **Python extension** for VS Code
- **Azure Functions extension** (v1.8.1+)
- **Azurite v3 extension** (for local Azure Storage emulation)
- **Azure Functions Core Tools** installed

---

## Local Project Creation

1. **Open VS Code** → `F1` → `Azure Functions: Create New Project...`
2. **Choose:**
   - Language: Python (Programming Model V2)
   - Function Template: HTTP trigger
   - Function Name: `HttpExample`
   - Authorization: Anonymous
3. **Generated files include:**
   - `function_app.py` with decorated HTTP trigger function
   - `local.settings.json` with:
     ```json
     "AzureWebJobsStorage": "UseDevelopmentStorage=true"
     ```

---

## Running Locally with Azurite

- Start Azurite: `F1` → `Azurite: Start`
- Run the function locally: Press `F5` (debug mode)
- Execute `HttpExample` from the Azure Functions extension
- Sample request body:
  ```json
  { "name": "Azure" }
  ```
- **Result:** Valid response in Terminal Output confirming successful execution

---

## Publishing to Azure

1. **Sign in** to Azure via VS Code sidebar
2. **Create Function App**: `Azure Functions: Create Function App in Azure`
   - Choose subscription, unique name, runtime stack, region
3. **Deploy**: `Azure Functions: Deploy to Function App`
4. **Verify**: `Azure Functions: Execute Function Now` (successful HTTP response)

---

## Extending Functionality: Queue Trigger Binding

### Setup: Queue Trigger Binding

- Create new function: `F1` → `Azure Functions: Create Function...` → Queue trigger
- Queue name: `myqueue-items`
- `function_app.py` updated with:
  ```python
  @queue_trigger(arg_name="msg", queue_name="myqueue-items", connection="AzureWebJobsStorage")
  ```
- Run Azurite and execute the queue-triggered function locally
- Use **Azure Storage Explorer** to:
  - Connect to Azurite
  - Add test messages to `myqueue-items` queue
  - Confirm function is triggered

---

## Next Step: SQL Output Binding

### Process

1. Copy queue-binding folder to create new function for SQL output
2. Update function with SQL output binding decorator:
   ```python
   @sql_output(arg_name="output", command_text="INSERT INTO SalesTable (Id, Name) VALUES (@Id, @Name)", connection_string_setting="SqlConnectionString")
   ```
3. **Create Azure SQL Database** via Azure Portal:
   - Create database and table (`SalesTable`)
   - Configure firewall rules for VS Code IP
   - Copy SQL connection string to `local.settings.json`:
     ```json
     "SqlConnectionString": "<actual-azure-sql-connection-string>"
     ```
4. **Test SQL output binding:**
   - Start Azurite, run locally with `F5`
   - Insert test queue messages (JSON matching table schema)
   - Use Azure Storage Explorer to trigger the queue
   - Verify new rows in SQL table via Azure Portal query editor

---

## Testing and Validation Steps

- **Local Execution:** Azurite started, functions run with `F5`
- **Queue Trigger:** Send test messages using Azure Storage Explorer, observe execution in VS Code
- **SQL Output:** Confirm inserted records in Azure SQL table using Azure Query Editor

---

## Conclusion

This process demonstrates:

- Creating a Python Azure Function in VS Code
- Local debugging with Azurite
- Extending with Queue trigger and SQL output binding
- End-to-end data flow: queue message → function → SQL database
- Complete local-to-cloud workflow using VS Code and Azure resources

---
## ✅ What I Learned

- How to structure Azure Function Apps using Python
- How to use output bindings to connect to external Azure services
- How to debug, test, and deploy function apps using VS Code
- Managing Azure credentials and app settings securely
## 🎥 Demo Video

Watch the full demo here:  
👉 [YouTube Demo Link](https://www.youtube.com/watch?v=Au96VLroNN0)

---



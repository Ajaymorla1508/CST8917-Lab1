# CST8917 Lab 1: Building Azure Function Apps with Output Bindings

## 👨‍💻 Objective

This lab demonstrates how to build and deploy two Azure Function Apps using Python and Visual Studio Code with **output bindings** to:
- Azure Storage Queues
- Azure SQL Database

---

## 📁 Project Structure

```
Lab1-8717/
│
├── azure/         # Azure Function with Queue output binding
│   └── HttpTrigger/
│       ├── function_app.py
│       ├── function.json
│       └── local.settings.json
│
├── database/      # Azure Function with SQL output binding
│   └── HttpTrigger1/
│       ├── function_app.py
│       ├── function.json
│       └── local.settings.json
│
└── README.md      # This file
```

---

## ⚙️ Setup Instructions

### Prerequisites

- Python 3.10+
- [Azure Functions Core Tools](https://learn.microsoft.com/en-us/azure/azure-functions/functions-run-local)
- [Azure CLI](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli)
- Visual Studio Code with Python and Azure Functions extensions
- An active Azure subscription

---

## 1️⃣ Azure Function with Storage Queue Output Binding

> Followed Microsoft Quickstart: [Add an Azure Storage Queue output binding to a function in Azure](https://learn.microsoft.com/en-us/azure/azure-functions/functions-add-output-binding-storage-queue?tabs=in-process%2Cfunctionsv2%2Cnodejs-v4)

### 🔧 Azure Setup

- Created a **Storage Account** and **Queue**
- Updated `local.settings.json` with:

```json
"AzureWebJobsStorage": "<your_storage_connection_string>"
```

### ▶️ Run Locally

```bash
cd azure
func start
```

### ☁️ Deploy to Azure

```bash
func azure functionapp publish <your-function-app-name>
```

---

## 2️⃣ Azure Function with SQL Output Binding

> Followed Microsoft Quickstart: [Add an Azure SQL output binding to a function in Azure](https://learn.microsoft.com/en-us/azure/azure-functions/functions-add-output-binding-azure-sql?tabs=in-process%2Cfunctionsv2%2Cnodejs-v4)

### 🔧 Azure Setup

- Created Azure SQL Database and table `dbo.ToDo`:

```sql
CREATE TABLE ToDo (
  Id UNIQUEIDENTIFIER PRIMARY KEY,
  title NVARCHAR(100),
  completed BIT,
  url NVARCHAR(255)
);
```

- Updated `local.settings.json` with:

```json
"SqlConnectionString": "<your_sql_connection_string>"
```

### ▶️ Run Locally

```bash
cd database
func start
```

### ☁️ Deploy to Azure

```bash
func azure functionapp publish <your-function-app-name>
```

---

## 🧪 Testing

- **Queue Function:** Sent a POST request with a JSON body; verified message appears in the Storage Queue.
- **SQL Function:** Sent a POST request with `{ "name": "Sample Task" }`; verified record inserted into the SQL database.

---

## 🎥 Demo Video

Watch the full demo here:  
👉 [YouTube Demo Link](#) ← (Replace this with your real link)

---

## ✅ What I Learned

- How to structure Azure Function Apps using Python
- How to use output bindings to connect to external Azure services
- How to debug, test, and deploy function apps using VS Code
- Managing Azure credentials and app settings securely

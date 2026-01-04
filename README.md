# 🚀 Azure Cosmos DB – Python Application (Local + Docker)

![Image](https://learn.microsoft.com/en-us/azure/cosmos-db/media/use-cases/iot.png)

![Image](https://s33046.pcdn.co/wp-content/uploads/2021/05/data-explorer-in-cosmos-db.png)

![Image](https://learn.microsoft.com/en-us/azure/cosmos-db/media/account-databases-containers-items/cosmos-entities.png)

![Image](https://miro.medium.com/1%2AEXQGr0N916cnrQRM-haEnw.png)

## 📌 Objective

Create an **Azure Cosmos DB (SQL API)** account using **Free Tier**, connect it to a **Python Flask app**, run it **locally** and inside a **Docker container**.

---

## 1️⃣ Create Azure Cosmos DB (Portal)

1. Go to **Azure Portal**
2. Search **Cosmos DB**
3. Click **Create**
4. Select:

   * API: **Core (SQL)**
   * Account Type: **Free Tier** ✅
   * Resource Group: `rg-cosmos-demo`
   * Account Name: `cosmos-atul-demo`
   * Region: `Central India` (or nearest)

---

## 2️⃣ Enable Free Tier

* Under **Basics**
* Enable **Free Tier**
  ✔️ 1000 RU/s
  ✔️ 25 GB storage

---

## 3️⃣ Configure Networking (Public + Private Endpoints)

![Image](https://learn-attachment.microsoft.com/api/attachments/1cd4d1c6-b4c7-491a-9c80-884f62661f0c?platform=QnA)

![Image](https://learn.microsoft.com/en-us/azure/cosmos-db/postgresql/media/howto-manage-firewall-using-portal/1-connection-security.png)

### Public Access

* Allow access from **All networks** (for lab)

### Private Endpoint (Optional – Advanced)

* Create **Private Endpoint**
* Attach to VNet
* Disable public access for production workloads

---

## 4️⃣ Create Database

1. Open Cosmos DB Account
2. Go to **Data Explorer**
3. Click **New Database**
4. Database Name:

   ```
   demoDB
   ```

---

## 5️⃣ Create Container

1. Inside `demoDB`
2. Click **New Container**
3. Container settings:

   ```
   Container name: items
   Partition key: /category
   Throughput: Shared
   ```

---

## 6️⃣ Create Python App from Azure Portal

1. Go to **Quick Start**
2. Select **Python**
3. Click **Download Code**
4. Extract the project

---

## 7️⃣ Run Application Locally (VS Code)

### Open Project

```bash
code .
```

### Install Python & Pip (Ubuntu/Linux)

```bash
sudo apt update
sudo apt install python3 -y
sudo apt install python3-pip -y
```

### Install Dependencies

```bash
sudo pip install -r requirements.txt
```

---

## 8️⃣ Update Cosmos DB Connection (cosmos.py)

![Image](https://i.sstatic.net/BVsBN.png)

![Image](https://learn.microsoft.com/en-us/azure/cosmos-db/media/access-secrets-from-keyvault/cosmos-keys-option.png)

### From Azure Portal

1. Go to **Keys**
2. Copy:

   * URI
   * PRIMARY KEY

### Update `cosmos.py`

```python
COSMOS_URI = "https://cosmos-atul-demo.documents.azure.com:443/"
COSMOS_KEY = "PASTE_PRIMARY_KEY_HERE"
DATABASE_NAME = "demoDB"
CONTAINER_NAME = "items"
```

---

## 9️⃣ Run Python App

```bash
python app.py
```

### Access Application

```
http://localhost:5000
http://127.0.0.1:5000
```

---

## 🤖 GitHub Copilot (AI Enhancement)

* Enable **GitHub Copilot**
* Improve:

  * Error handling
  * Logging
  * CRUD APIs
  * Environment variable support

Example:

```python
import os
COSMOS_KEY = os.getenv("COSMOS_KEY")
```

---

## 🐳 Running Application in Docker

![Image](https://user-images.githubusercontent.com/23358756/74426702-28d17580-4e99-11ea-846e-25f7fcc22d50.png)

![Image](https://miro.medium.com/v2/resize%3Afit%3A1200/1%2AxaV0lysSbRxqMAJdBlNc4A.png)

![Image](https://media.licdn.com/dms/image/v2/D5612AQGnn8DwSPPGmg/article-cover_image-shrink_720_1280/article-cover_image-shrink_720_1280/0/1681604245712?e=2147483647\&t=sRiztWBh2IvLMIeQhkxdSQy-xIkHD-GZR2PwV-X3bcQ\&v=beta)

### Build Docker Image

```bash
sudo docker buildx build \
-t atuljkamble/cosmosdbapp \
--load .
```

### Verify Image

```bash
sudo docker images
```

### Run Container

```bash
sudo docker run -d \
-p 8000:8000 \
atuljkamble/cosmosdbapp:latest
```

### Access App

```
http://localhost:8000
```

---

## 📁 Recommended Project Structure

```
cosmosdb-python-app/
│── app.py
│── cosmos.py
│── requirements.txt
│── Dockerfile
│── README.md
```

---

## 🔐 Best Practices

* Use **Azure Key Vault** for secrets
* Enable **Private Endpoint** for prod
* Store secrets in **Environment Variables**
* Enable **Autoscale RU/s**
* Monitor with **Azure Monitor**

---

## 📦 Docker + Cosmos DB Flow

```
User → Flask App → Cosmos DB SQL API
```

---

## 📌 Summary

✔ Azure Cosmos DB (Free Tier)
✔ Python Flask App
✔ Local + Docker Execution
✔ Secure Connection Handling
✔ Production-ready structure

---



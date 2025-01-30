 ---

# 📌 AI Chatbot for Customer Support  

This project is an **AI-powered chatbot** that provides customer support by answering questions about a **judicial circular**. The chatbot is designed with a **microservices architecture**, allowing modular development and scalability. It leverages **Retrieval-Augmented Generation (RAG)** to retrieve relevant information and generate context-aware responses.  

## 🚀 Services  

The project consists of the following services:  

1. **Frontend:** A **React** application styled with **TailwindCSS**, providing an interactive user interface to chat with the AI-powered assistant.  

2. **Service2 (API Gateway):** A **FastAPI**-based backend that acts as a communication bridge between the frontend and Service3. It also manages user interaction history.  

3. **Service3 (Chatbot Engine):** Another **FastAPI**-based backend hosting the chatbot logic. It uses **LangChain** and OpenAI’s API to retrieve information from the circular and generate accurate responses.  

4. **Redis:** A **Redis** server used as a vector database for state management and caching.  

5. **Postgres (pgvector):** A **PostgreSQL** server with **pgvector** extension, used for storing embeddings of the circular’s text to optimize retrieval operations.  

## 🏗️ Microservices Architecture  

This project follows a **microservices-based architecture**, which simulates a real-world software development environment. Each service is containerized using **Docker** for improved portability and deployment efficiency.  

### **Key Decisions**  

- **Technology Selection:** React, FastAPI, Redis, pgvector, LangChain, and Docker were chosen for their efficiency and compatibility.  
- **Chunk Size Optimization:** The judicial circular is split into **optimized chunks** to improve retrieval accuracy in the RAG pipeline.  
- **Microservices Implementation:** This ensures modularity, scalability, and better collaboration in a team setting.  
- **Vector Databases:** Using Redis and pgvector significantly improves query response time by leveraging efficient embedding-based searches.  
- **Docker for Portability:** All services are containerized, allowing seamless deployment across different environments.  

## 🛠️ Setup  

To run the project, ensure you have **Docker** installed on your system.  

Then, execute the following command:  

```bash
docker-compose up --build
```  

This will start all services as defined in `docker-compose.yml`, pulling necessary Docker images, creating containers, and running them together.  

## 📥 Data Population  

The database must be populated with embeddings from the judicial circular before the chatbot can function correctly.  

### **1️⃣ Set up a virtual environment (recommended)**  
It is recommended to use **Anaconda** to manage dependencies.  

```bash
python -m venv venv
.\venv\Scripts\activate
```  

### **2️⃣ Install dependencies**  
Ensure that all required libraries are installed before running the script:  

```bash
pip install -r requirements.txt
```  

### **3️⃣ Run the population script**  
Once the virtual environment is active and dependencies are installed, run the script:  

```bash
python insert_data.py
```  

This script will:  
✔ Connect to the **PostgreSQL (pgvector) database**  
✔ Create necessary tables (if they don’t exist)  
✔ Insert the processed embeddings into the vector database  

## 🔑 Environment Variables  

Rename the `.env.example` file to `.env` and configure your **OpenAI API Key** before running the application.  

## 📦 LangChain on Kubernetes (Local Setup)  

1. Run a local Docker Registry  

```bash
docker run -d -p 5000:5000 --name local-registry registry:2
```  

2. Build all images locally  

```shell
docker build -t mypostgres ./postgres
docker build -t myservice2 ./service2
docker build -t myservice3 ./service3
docker build -t myfrontend ./frontend
```  

3. Tag and push images to the local registry  

```shell
# For PostgreSQL
docker tag mypostgres localhost:5000/mypostgres
docker push localhost:5000/mypostgres

# For API Gateway (Service2)
docker tag myservice2 localhost:5000/myservice2
docker push localhost:5000/myservice2

# For Chatbot Engine (Service3)
docker tag myservice3 localhost:5000/myservice3
docker push localhost:5000/myservice3

# For Frontend
docker tag myfrontend localhost:5000/myfrontend
docker push localhost:5000/myfrontend
```  

---
# 🌍 Roamly-GPS-Application

Welcome to **Roamly-GPS**, a website project where you can connect with fellow travelers from all around the globe and plan your next group trip!

---

## ✨ How does it work?

You start by creating a personal profile, which gives you access to the platform’s main map. From there, you can view your current location, explore different countries you’d like to visit, discover points of interest (e.g. restaurants, museums, parks), and get directions to them.

You can also join existing travel groups or create your own, inviting friends or even new connections, and plan your trip together using the built-in live chat feature.

---

## ☁️ Architecture

Roamly-GPS was built as a **cloud-native microservice architecture** application, designed to run in distributed environments.  
The application was deployed on a **DigitalOcean cloud-hosted Kubernetes cluster**, using the **Enterprise Service Bus (ESB)** approach to ensure loose coupling, scalability, and security.

📌 Below is the **C2 level of a C4 container diagram** of Roamly-GPS, showcasing the overall structure of the system.  
Purple components = already developed   
Blue components = planned for future development 

![Roamly-GPS C2 Diagram](./docs/C4_Diagram_Roamly-Level2.png)


### 🔎 Diagram explanation

- **NGINX Frontend Server**  
  - Serves the React TS UI over HTTPS on a **nip.io domain**  
  - Acts as a **reverse proxy**, forwarding requests to the API Gateway over the internal network  

- **Multi-language Microservices**  
  - **Spring Boot (Java)** → API Gateway (Eureka)  
  - **FastAPI (Python)** → backend services (location-and-poi, travel groups etc.)  

- **Authentication & Security**  
  - User login handled directly in the **UI component**  
  - Authentication using **OAuth2** with **Amazon Cognito** as the identity provider  

- **Messaging**  
  - RabbitMQ used with **RPC communication** for offloading CRUD operations and data handling  
  - **TLS encryption enabled on all RabbitMQ message channels**, securing inter-service communication   

- **Databases**  
  - MongoDB Atlas cloud   

- **CI/CD & Quality**
  - Automated CI/CD pipelines created with GitHub actions  
  - SonarQube Cloud integrated for automated checks  

- **Deployment**  
  - Fully containerized with Docker, orchestrated with Kubernetes

👉 Since the project relied on cloud services (MongoDB Atlas, SonarQube Cloud, Kubernetes cluster), it cannot be cloned and started directly. However, all the microservice codebases are included in the  organization's repositories.

---

## 🔒 Security Approach

Security was implemented at multiple layers:

- **NGINX as Entry Point**  
  - Serves the frontend over HTTPS.
  - Forwards requests internally to the API Gateway over the cluster network
  - NGINX Ingress Controller serves the UI component over a HTTPS nip.io website domain in the Kubernetes cluster  

- **Authentication**  
  - Handled at the UI level with **OAuth2**  
  - **Amazon Cognito** manages identity, tokens, and secure user sessions  

- **Message Bus**  
  - RabbitMQ communication used **TLS encryption** for all RPC traffic  

- **Internal Network**  
  - All backend communication isolated within the Kubernetes cluster  
  - Private service-to-service traffic kept separate from external requests 

This layered security ensures that both **user-facing** and **internal service communications** are protected.

---

## 📂 Repository Structure

This organization contains multiple repositories, each focusing on a different part of the system:

- **UI Service (NGINX + React)** → user interface connected secured with **React Oidc Context** and **Amazon Cognito** + reverse proxy setup  
- **API-Gateway** → entry point to the  internal system (Spring Boot)   
- **Location-and-poi-service** → integrates with location APIs (FastAPI)  
- **Travel-group-service** → management of user travel groups (FastAPI)  
- **Chat-Service** → real-time messaging (FastAPI + RabbitMQ)  

Each repository has its own README with setup details.

---

## 🛠️ Tech Stack

- **Frontend**: React TS + Vite served by **NGINX** (HTTPS + reverse proxy)  
- **Backend**: Spring Boot (API Gateway), FastAPI (Python microservices)  
- **Authentication**: OAuth2 with Amazon Cognito (AWS)  
- **Messaging**: RabbitMQ (RPC communication with **TLS encryption**)  
- **Databases**: MongoDB Atlas cloud 
- **DevOps**: Docker, Kubernetes (cloud-hosted on DigitalOcean), SonarQube Cloud  
- **External APIs**: Geoapify API, OpenStreetMap

---

## 🤝 Project Background

This project was developed as part of the **Advanced Software Development** semester. 
Key focus areas included:

- Scalable and secure microservices architecture
- Cloud-native design and deployment using a Kubernetes cluster
- Creation of automated CI/CD pipelines
- System optimization and Code quality

---

## 🚀 Vision

Roamly-GPS is not just about navigation. It’s about **bringing people together**, making it easy to explore new destinations, and turning solo travel into a group adventure.

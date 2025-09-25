# Sales Store Deployment

This repository orchestrates full scale deployment for the Sales Store application, including backend (Spring Boot), frontend (Express), and PostgreSQL database.

- The frontend is individually hosted at: [sales-store-frontend](https://github.com/TsvetanDyulgerov/sales-store-frontend)
- The backend is individually hosted at: [sales-store-backend](https://github.com/TsvetanDyulgerov/sales-store-backend)

## About

Sales Store is a web-based e-commerce system which serves to unilaterally manage all business actions of an e-commerce business. 
The project was built as part of an internship program and is tailored to the needs and requirements of a specific client.

The app consists of three seperate parts:
1. PostgreSQL database for storing commerce related information
2. Back-end in Java which serves a REST API, built using the Spring Framework.
3. Front-end built as a standalone Express.js application

As per the client's needs and requirements, this web-application contains the following functionality:
- Registered users with the Admin role can create, update, read and delete entries of users, products and orders. Admins can also generate filtered reports on the orders (by range of order date, username and product name)
- Registered users without the Admin role can send new orders under their own account and see their previous order history.
- Non-athenticated users must either register as a new user or log into an existing account to access the application.

The entire three-part system is containerised and managed in a [docker](https://www.docker.com) container.

## Prerequisites
- Docker & Docker Compose installed

## Getting Started

1. **Clone the repository:**
   ```sh
   git clone https://github.com/TsvetanDyulgerov/sales-store-deployment
   
2. **Navigate to the project directory:**
   ```sh
   cd sales-store-deployment
   ```
   
3. **Set environment variables:**

    - Rename the existing .env.example file to .env and update the environment variables as needed.


4. **Start the application using Docker Compose:**
   ```sh
   docker-compose up --build
   ```



## Example .env File


### `/.env`
```# BACKEND
# Postgres
POSTGRES_DB=SalesStore
POSTGRES_USER=admin
POSTGRES_PASSWORD=youradminpassword

# App settings
SPRING_DATASOURCE_URL=jdbc:postgresql://db:5432/SalesStore
SPRING_DATASOURCE_USERNAME=admin
SPRING_DATASOURCE_PASSWORD=youradminpassword

# Backend
APP_PORT=8080
SPRING_PROFILES_ACTIVE=prod

# Security - VERY IMPORTANT: Use a strong 256-bit secret key for JWT
# You can generate one using online tools or libraries
JWT_SECRET=yourverysecure265bitjwtsecretkey

# UI
UI_PORT=3000

#FRONTEND
# Environment variables for the frontend application

# Port for the Express server
PORT=3001

```


## Stopping Services
```sh
docker-compose down
```

## Updating the Deployment Repo When Subrepos Change

If you update the backend or frontend code in their respective repositories, you need to update the deployment repo to use the latest versions. Here’s how:

1. **Pull Latest Changes in Subrepos**
   - Navigate to the subrepo directory (e.g., `backend/` or `frontend/`).
   - Run:
     ```sh
     git pull origin main
     ```
   - Or, if using a different branch, pull the appropriate branch.


2. **Rebuild Docker Images**
   - After updating the code, rebuild the containers to use the new code:
     ```sh
     docker-compose up --build
     ```
   - This ensures Docker uses the latest source code from the subrepos.

3. **Restart Services**
   - If the services are already running, restart them:
     ```sh
     docker-compose down
     docker-compose up --build
     ```


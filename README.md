# Sales Store Deployment

This repository orchestrates deployment for the Sales Store application, including backend (Spring Boot), frontend (Express), and PostgreSQL database.

## Prerequisites
- Docker & Docker Compose installed
- Clone this repository

## Setup
1. **Environment Variables**
   - Copy the provided `.env.example` files or create your own:
     - `/backend/.env` (for backend service)
     - `/frontend/.env` (for frontend service)
   - Fill in the required values (see below for example contents).

2. **Build & Start Services**
   ```sh
   docker-compose up --build
   ```
   This will start the backend, frontend, and database containers.

## Example .env Files

### `/backend/.env`
```
POSTGRES_DB=SalesStore
POSTGRES_USER=admin
POSTGRES_PASSWORD=adminpass1234
SPRING_DATASOURCE_URL=jdbc:postgresql://db:5432/SalesStore
SPRING_DATASOURCE_USERNAME=admin
SPRING_DATASOURCE_PASSWORD=adminpass1234
APP_PORT=8080
SPRING_PROFILES_ACTIVE=prod
JWT_SECRET=mIj0GqaAsF234cxcvnFRu1F1YIHgJzWg
UI_PORT=3000
```

### `/frontend/.env`
```
PORT=3001
```

## Notes
- `.env` files are **gitignored** for security. Each user must create their own.
- For troubleshooting, check container logs:
  ```sh
  docker-compose logs
  ```
- For custom configuration, edit the `.env` files and `docker-compose.yml` as needed.

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

4. **Check for New Environment Variables**
   - If the subrepo update requires new environment variables, update the corresponding `.env` file in the deployment repo.

5. **Troubleshooting**
   - Check logs for errors:
     ```sh
     docker-compose logs
     ```

## Questions?
Open an issue or contact the repository maintainer.

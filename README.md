# MEAN Stack CRUD Application with Docker & CI/CD

A full-stack CRUD application using the MEAN stack (MongoDB, Express, Angular 15, and Node.js) with complete containerization, CI/CD pipeline, and deployment automation.


## 🏗️ Architecture

- **Frontend**: Angular 15 application with HTTPClient for API communication
- **Backend**: Node.js with Express providing REST APIs
- **Database**: MongoDB for data persistence
- **Reverse Proxy**: Nginx for routing and load balancing
- **Containerization**: Docker & Docker Compose
- **CI/CD**: GitHub Actions for automated deployment

## 📋 Prerequisites

- Docker and Docker Compose installed
- Node.js 18+ (for local development)
- Angular CLI (for local development)
- Docker Hub account
- GitHub repository
- Ubuntu VM (for production deployment)

## 🚀 Quick Start

### Local Development

1. **Backend Setup**
   ```bash
   cd backend
   npm install
   node server.js
   ```

2. **Frontend Setup**
   ```bash
   cd frontend
   npm install
   ng serve --port 8081
   ```

3. **Access Application**
   - Frontend: http://localhost:8081
   - Backend API: http://localhost:8080

### Docker Development

1. **Build and Run with Docker Compose**
   ```bash
   docker-compose up --build
   ```

2. **Access Application via Nginx**
   - http://localhost (via Nginx reverse proxy)
   - Frontend: http://localhost:4200 (direct)
   - Backend: http://localhost:8080 (direct)

## 🐳 Docker Configuration

### Services

- **mongodb**: MongoDB 6 database (port 27017)
- **backend**: Node.js Express API (port 8080)
- **frontend**: Angular application served by Nginx (port 4200)
- **nginx**: Reverse proxy (port 80)

### Environment Variables

- `MONGO_URI`: MongoDB connection string (default: mongodb://mongodb:27017/cruddb)

## 🔄 CI/CD Pipeline

### GitHub Actions Setup

1. **Repository Secrets Required:**
   - `DOCKER_USERNAME`: Your Docker Hub username
   - `DOCKER_PASSWORD`: Your Docker Hub password or access token
   - `VM_IP`: Your Ubuntu VM public IP address
   - `SSH_PRIVATE_KEY`: SSH private key for VM access

2. **Pipeline Triggers:**
   - Automatically triggers on push to `main` branch
   - Builds and pushes Docker images to Docker Hub
   - Deploys to production VM via SSH

3. **Pipeline Steps:**
   - Checkout code
   - Set up Docker Buildx
   - Login to Docker Hub
   - Build and push backend image
   - Build and push frontend image
   - Deploy to VM with latest images

## 🌐 Production Deployment

### Ubuntu VM Setup

1. **Install Docker and Docker Compose**
   ```bash
   curl -fsSL https://get.docker.com -o get-docker.sh
   sudo sh get-docker.sh
   sudo usermod -aG docker ubuntu
   sudo curl -L "https://github.com/docker/compose/releases/download/v2.20.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
   sudo chmod +x /usr/local/bin/docker-compose
   ```

2. **Clone Repository**
   ```bash
   git clone <your-repository-url> mean-app
   cd mean-app
   ```

3. **Update Docker Compose Configuration**
   ```bash
   # Replace YOUR_DOCKER_USERNAME with your actual Docker Hub username
   sed -i 's/YOUR_DOCKER_USERNAME/your-username/g' docker-compose.yml
   ```

4. **Deploy Application**
   ```bash
   docker-compose pull
   docker-compose up -d
   ```

### Application Access

- **Primary URL**: http://<your-vm-ip> (via Nginx)
- **Direct Frontend**: http://<your-vm-ip>:4200
- **Backend API**: http://<your-vm-ip>:8080

## 🔧 Configuration

### Database Configuration

Update MongoDB connection in `backend/app/config/db.config.js`:
```javascript
module.exports = {
  url: process.env.MONGO_URI || "mongodb://localhost:27017/dd_db"
};
```

### Frontend API Configuration

Update API endpoint in `frontend/src/app/services/tutorial.service.ts`:
```typescript
private baseUrl = 'http://localhost:8080'; // Update for production
```

### Nginx Configuration

The `nginx.conf` file handles:
- Frontend routing (/)
- Backend API routing (/api/, /tutorials)
- Load balancing and reverse proxy

## 📊 Application Features

- **Create**: Add new tutorials with title, description, and published status
- **Read**: View all tutorials or search by title
- **Update**: Modify existing tutorial details
- **Delete**: Remove tutorials from the database
- **Search**: Find tutorials by title using the search box

## 🔍 API Endpoints

- `GET /` - Welcome message
- `GET /tutorials` - Get all tutorials
- `GET /tutorials/:id` - Get tutorial by ID
- `POST /tutorials` - Create new tutorial
- `PUT /tutorials/:id` - Update tutorial
- `DELETE /tutorials/:id` - Delete tutorial
- `DELETE /tutorials` - Delete all tutorials
- `GET /tutorials/published` - Get published tutorials
- `GET /tutorials?title=<title>` - Search tutorials by title

## 🛠️ Troubleshooting

### Common Issues

1. **MongoDB Connection Error**
   - Check MongoDB container status: `docker ps`
   - Verify environment variables in docker-compose.yml
   - Check logs: `docker logs mongo`

2. **Backend Not Responding**
   - Check backend container: `docker logs backend`
   - Verify port conflicts
   - Check MongoDB connectivity

3. **Frontend Not Loading**
   - Check frontend container: `docker logs frontend`
   - Verify build completed successfully
   - Check Nginx configuration

4. **CI/CD Pipeline Failures**
   - Verify GitHub repository secrets
   - Check Docker Hub credentials
   - Validate SSH key access to VM

### Useful Commands

```bash
# View all containers
docker ps

# View container logs
docker logs <container-name>

# Restart services
docker-compose restart

# Stop and remove containers
docker-compose down

# Clean up unused images
docker system prune -f
```

## 📸 Screenshots Documentation

### Required Screenshots for Documentation

1. **CI/CD Configuration**
   - GitHub repository secrets configuration
   - GitHub Actions workflow execution logs
   - Successful pipeline completion

2. **Docker Images**
   - Docker Hub repository showing pushed images
   - Docker build process logs
   - Image tags and versions

3. **Application Deployment**
   - Docker containers running on VM
   - Application accessible via browser
   - CRUD operations working

4. **Infrastructure**
   - Nginx configuration file
   - Docker Compose services
   - VM setup and networking

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Commit your changes
4. Push to the branch
5. Create a Pull Request

## 📝 License

This project is licensed under the ISC License.

## 📞 Support

For issues and questions:
- Check the troubleshooting section
- Review container logs
- Verify configuration files
- Ensure all prerequisites are met

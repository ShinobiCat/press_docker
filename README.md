# press terraformed (WORK IN PROGRESS)

Custom Docker image for Frappe with the `press` app pre-installed.  
This image is designed for use in containerized deployments, CI/CD pipelines, and reproducible environments.

![Docker Build](https://img.shields.io/github/actions/workflow/status/digikwal/press/docker-build.yml?label=build&style=flat-square)
![Docker Image Size](https://img.shields.io/docker/image-size/digikwal/press/latest?style=flat-square)
![Docker Pulls](https://img.shields.io/docker/pulls/digikwal/press?style=flat-square)

---

## 🚀 Features

- Based on `frappe:v15.66.1`
- Automatically installs the [`press`](https://github.com/frappe/press) app using `bench get-app`
- Includes required directories for Certbot integration and custom build workflows:
  - `/home/frappe/frappe-bench/press/.certbot/webroot`
  - `/home/frappe/frappe-bench/press/.clones`
  - `/home/frappe/frappe-bench/press/.docker-builds`
- Pre-installs `certbot-dns-route53` (required for frappe press)
- First time setup script for site creation and press installation
  - ['Documentation'](https://frappecloud.com/docs/local-fc-setup)

---

## 🐳 Usage

1. Clone this repo to your frappe home directory
```bash
git clone https://github.com/digikwal/press /home/frappe
```
2. Create a `.env` file (see `.env.example`)
```bash
cp example.env .env
```
3. Setup your '.env' by customizing the placeholders
   - DO NOT change $AWS_REGION
   - DO NOT use naked domain for $FRAPPE_PRESS_DOMAIN
4. Run first time setup script
```bash
bash /home/frappe/first_time_setup.sh
```
5. Follow instructions and have patience
6. To see passwords check your environment file
```bash
cat ~/.env
```

Here are some basic Docker commands to check container health and status:

### 1. **List All Containers**
   ```bash
   docker ps -a
   ```
   - Shows all running and stopped containers, along with their status.

### 2. **Check Logs of a Container**
   ```bash
   docker logs <container_name_or_id>
   ```
   - Displays the logs of a specific container. Use `-f` to follow logs in real-time.

### 3. **Inspect Container Health**
   ```bash
   docker inspect <container_name_or_id>
   ```
   - Provides detailed information about the container, including health status if a health check is defined.

### 4. **Check Health Status**
   ```bash
   docker ps --filter "name=<container_name>" --format "{{.Names}}: {{.Status}}"
   ```
   - Filters the output to show the health status of a specific container.

### 5. **Execute a Command Inside a Running Container**
   ```bash
   docker exec -it <container_name_or_id> bash
   ```
   - Opens an interactive shell inside the container for debugging.

### 6. **Restart a Container**
   ```bash
   docker restart <container_name_or_id>
   ```
   - Restarts a container if it's not functioning properly.

### 7. **Check Resource Usage**
   ```bash
   docker stats
   ```
   - Displays real-time resource usage (CPU, memory, etc.) of all running containers.
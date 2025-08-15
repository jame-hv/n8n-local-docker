# n8n Local Docker

This setup provides a complete n8n environment with queue mode support, includin

- **PostgreSQL**: Database for n8n data persistence
- **Redis**: Message queue for n8n queue mode
- **n8n Main**: Main n8n instance (web UI and API)
- **n8n Worker**: Worker instance for executing workflows

## Features

- 🚀 n8n in queue mode for better scalability
- 🐘 PostgreSQL database for data persistence
- 🔴 Redis for job queuing
- 📁 All data mounted to `./docker/` folder
- 🔐 Basic authentication enabled
- 🏥 Health checks for all services

## Quick Start

1. **Start all services:**

   ```bash
   docker-compose up -d
   ```

2. **View logs:**

   ```bash
   docker-compose logs -f
   ```

3. **Access n8n:**

   - URL: http://localhost:5678
   - Username: `admin`
   - Password: `admin123`

4. **Stop all services:**
   ```bash
   docker-compose down
   ```

## Data Persistence

All data is stored in the `./docker/` directory:

- `./docker/postgres-data/` - PostgreSQL database files
- `./docker/redis-data/` - Redis persistence files
- `./docker/n8n-data/` - n8n workflows, credentials, and settings

## Configuration

You can modify the environment variables in the `.env` file:

- Database credentials
- n8n authentication
- Port configurations
- Timezone settings

## Services

### PostgreSQL

- **Container**: `n8n-postgres`
- **Port**: 5432
- **Database**: n8n
- **User**: n8n

### Redis

- **Container**: `n8n-redis`
- **Port**: 6379

### n8n Main

- **Container**: `n8n-main`
- **Port**: 5678
- **Function**: Web UI, API, and workflow management

### n8n Worker

- **Container**: `n8n-worker`
- **Function**: Execute queued workflows

## Scaling

To add more workers for better performance:

```bash
docker-compose up -d --scale n8n-worker=3
```

## Troubleshooting

1. **Check service status:**

   ```bash
   docker-compose ps
   ```

2. **View specific service logs:**

   ```bash
   docker-compose logs n8n-main
   docker-compose logs n8n-worker
   docker-compose logs postgres
   docker-compose logs redis
   ```

3. **Restart a specific service:**

   ```bash
   docker-compose restart n8n-main
   ```

4. **Reset all data:**
   ```bash
   docker-compose down -v
   sudo rm -rf ./docker/
   docker-compose up -d
   ```

## Security Notes

- Change default passwords in `.env` file before production use
- Consider using environment-specific configurations
- Regularly backup the `./docker/` directory

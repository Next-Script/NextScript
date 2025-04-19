# Deployment Guide

## Deployment Options

### 1. Docker Deployment (Recommended)

#### Prerequisites
- Docker 20.x or later
- Docker Compose 2.x or later
- 4GB RAM minimum (8GB recommended)
- 2 CPU cores minimum (4 recommended)

#### Steps

1. **Build Docker Images**
```bash
# Build all services
docker-compose build

# Build specific service
docker-compose build api-gateway
```

2. **Configure Environment**
```bash
# Copy example env file
cp .env.example .env

# Edit environment variables
nano .env
```

3. **Deploy Services**
```bash
# Start all services
docker-compose up -d

# Check service status
docker-compose ps
```

### 2. Kubernetes Deployment

#### Prerequisites
- Kubernetes 1.22+
- Helm 3.x
- kubectl configured

#### Steps

1. **Add Helm Repository**
```bash
helm repo add nextscript https://charts.nextscript.dev
helm repo update
```

2. **Configure Values**
```yaml
# values.yaml
image:
  repository: nextscript
  tag: latest

resources:
  requests:
    cpu: 100m
    memory: 128Mi
  limits:
    cpu: 1000m
    memory: 1Gi
```

3. **Deploy**
```bash
helm install nextscript nextscript/platform -f values.yaml
```

### 3. Cloud Provider Deployments

#### AWS

1. **ECS Deployment**
   - Use provided CloudFormation templates
   - Configure Auto Scaling
   - Set up Application Load Balancer

2. **EKS Deployment**
   - Follow Kubernetes deployment guide
   - Use AWS specific storage classes
   - Configure IAM roles

#### Azure

1. **AKS Deployment**
   - Use Azure Container Registry
   - Configure Azure Monitor
   - Set up Azure Application Gateway

#### Google Cloud

1. **GKE Deployment**
   - Use Container Registry
   - Configure Cloud Monitoring
   - Set up Cloud Load Balancing

## Configuration

### Essential Environment Variables

```env
# Core Settings
NODE_ENV=production
PORT=3000
LOG_LEVEL=info

# Database
DATABASE_URL=postgresql://user:pass@host:5432/db
REDIS_URL=redis://host:6379

# Authentication
JWT_SECRET=your-secret-key
AUTH_PROVIDER=oauth2

# Services
AI_SERVICE_KEY=your-ai-service-key
STORAGE_PROVIDER=s3
```

### Security Configuration

1. **SSL/TLS Setup**
```bash
# Generate SSL certificate
certbot certonly --nginx -d yourdomain.com

# Configure nginx
nano /etc/nginx/sites-available/nextscript
```

2. **Firewall Rules**
```bash
# Allow necessary ports
ufw allow 80,443,3000/tcp
```

## Scaling

### Horizontal Scaling

1. **API Services**
```yaml
# kubernetes/api-deployment.yaml
apiVersion: apps/v1
kind: Deployment
spec:
  replicas: 3
  strategy:
    type: RollingUpdate
```

2. **Database Scaling**
   - Read replicas
   - Connection pooling
   - Sharding strategy

### Vertical Scaling

1. **Resource Allocation**
   - CPU optimization
   - Memory tuning
   - Disk IOPS

## Monitoring

### 1. Metrics Collection

```yaml
# prometheus/config.yaml
scrape_configs:
  - job_name: 'nextscript'
    static_configs:
      - targets: ['localhost:3000']
```

### 2. Logging

```yaml
# fluentd/config.yaml
<source>
  @type forward
  port 24224
</source>
```

### 3. Alerting

```yaml
# alertmanager/config.yaml
route:
  receiver: 'team-alerts'
  group_wait: 30s
```

## Backup and Recovery

### Database Backup

```bash
# Automated backup script
#!/bin/bash
pg_dump -U postgres nextscript > backup.sql
aws s3 cp backup.sql s3://backups/
```

### Recovery Procedures

1. **Service Recovery**
```bash
# Rollback deployment
kubectl rollout undo deployment/nextscript

# Restore database
psql -U postgres nextscript < backup.sql
```

## Performance Optimization

### 1. Caching Strategy

```yaml
# redis configuration
maxmemory 2gb
maxmemory-policy allkeys-lru
```

### 2. CDN Configuration

```nginx
# nginx cdn config
location /static/ {
    proxy_cache STATIC;
    proxy_cache_use_stale error timeout;
    proxy_cache_valid 200 24h;
}
```

## Troubleshooting

### Common Issues

1. **Database Connectivity**
```bash
# Check database connection
pg_isready -h hostname -p 5432

# Check logs
kubectl logs deployment/nextscript-db
```

2. **Service Health**
```bash
# Check service health
curl -f http://localhost:3000/health

# View service logs
docker-compose logs -f api-gateway
```

## Maintenance

### Regular Tasks

1. **Updates**
```bash
# Update services
docker-compose pull
docker-compose up -d

# Update dependencies
npm update
```

2. **Cleanup**
```bash
# Clean old images
docker image prune -a

# Clean logs
truncate -s 0 /var/log/nextscript/*.log
```

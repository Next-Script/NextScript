# Getting Started with NextScript

This guide will help you get up and running with NextScript, our integrated low-code development platform.

## System Requirements

- Operating System: Windows 10+, macOS 10.15+, or Linux (Ubuntu 20.04+ recommended)
- Node.js 18.x or higher
- Docker 20.x or higher
- Git 2.x or higher
- Minimum 8GB RAM (16GB recommended)
- 4 CPU cores (8 cores recommended)

## Installation Process

### 1. Development Environment Setup

```bash
# Clone the repository
git clone https://github.com/yourusername/NextScript.git

# Navigate to project directory
cd NextScript

# Install dependencies
npm install

# Configure environment
cp .env.example .env
```

### 2. Configuration

Edit your `.env` file with appropriate values:

```env
NODE_ENV=development
PORT=3000
DATABASE_URL=postgresql://user:password@localhost:5432/nextscript
REDIS_URL=redis://localhost:6379
```

### 3. Starting the Development Server

```bash
# Start the development server
npm run dev

# In a separate terminal, start the API server
npm run api:dev
```

The platform will be available at `http://localhost:3000`

## First Steps

1. **Access the Platform**: Open your browser and navigate to `http://localhost:3000`
2. **Create Your First Project**: Click "New Project" and select a template
3. **Explore the Visual Editor**: Familiarize yourself with the drag-and-drop interface
4. **Test the Development Environment**: Make some changes and see live updates

## Basic Concepts

- **Projects**: Container for your application
- **Components**: Reusable UI elements
- **Workflows**: Visual programming for business logic
- **Data Models**: Define your application's data structure
- **Services**: Backend API and integrations
- **Deployments**: Publishing your application

## Next Steps

- Read the [Architecture Overview](./architecture.md)
- Explore the [Development Guide](./development.md)
- Learn about [Security Best Practices](./security.md)
- Join our [Community Discord](https://discord.gg/nextscript)

## Troubleshooting

### Common Issues

1. **Port Already in Use**
   ```bash
   lsof -i :3000
   kill -9 <PID>
   ```

2. **Node Version Mismatch**
   ```bash
   nvm install 18
   nvm use 18
   ```

3. **Database Connection Issues**
   - Check PostgreSQL service is running
   - Verify database credentials in `.env`

### Getting Help

- Check our [FAQ](./faq.md)
- Search [GitHub Issues](https://github.com/yourusername/NextScript/issues)
- Join our [Discord Community](https://discord.gg/nextscript)

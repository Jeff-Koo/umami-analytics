# Umami Analytics

[Umami](https://umami.is/) is a simple, fast, privacy-focused alternative to Google Analytics. It's open-source and self-hosted, giving you complete control over your analytics data.

## Features

- 📊 Simple and clean analytics dashboard
- 🔒 Privacy-focused (GDPR compliant)
- 🚀 Fast and lightweight
- 🐳 Easy Docker deployment
- 📱 Mobile-friendly interface
- 🌍 Multi-language support

## Quick Start

### Prerequisites

- Docker and Docker Compose installed
- Port 3000 available on your system

### Installation

1. **Clone or download this repository**

2. **Create environment files**

   Create a `.env` file for the Umami application:
   ```bash
   DATABASE_URL=postgresql://umami:umami@umami-db-service:5432/umami
   DATABASE_TYPE=postgresql
   APP_SECRET=your-random-string-for-app-secret
   ```

   Create a `.env.db` file for the PostgreSQL database:
   ```bash
   POSTGRES_DB=umami
   POSTGRES_USER=umami
   POSTGRES_PASSWORD=umami
   ```

3. **Start the services**
   ```bash
   docker-compose up -d
   ```

4. **Access Umami**
   - Open your browser and go to `http://localhost:3000`
   - **Default login credentials:**
     - Username: `admin`
     - Password: `umami`

## Configuration

### Environment Variables

The main configuration is done through the `.env` file:

- `DATABASE_URL`: PostgreSQL connection string
- `DATABASE_TYPE`: Database type (postgresql)
- `APP_SECRET`: Random string for password hashing (change this!)

### Database

The setup uses PostgreSQL 15 with persistent storage. Data is stored in the `./umami-db-data` directory.

## Usage

### Adding Your Website

1. Log in to the Umami dashboard
2. Click "Add Website"
3. Enter your website details
4. Copy the tracking code and add it to your website's `<head>` section. 
The tracking code can be found under the Tracking Code tab.

### Tracking Code Example

```html
<script async defer
  src="http://localhost:3000/script.js"
  data-website-id="your-website-id-here">
</script>
```

## Management

### Start Services
```bash
docker-compose up -d
```

### Stop Services
```bash
docker-compose down
```

### View Logs
```bash
docker-compose logs -f
```

### Update Umami
```bash
docker-compose pull
docker-compose up -d
```

## Security Notes

- Change the default `APP_SECRET` in your `.env` file
- Consider changing the default database credentials
- Use HTTPS in production
- Regularly update the Docker images

## Troubleshooting

### Port Already in Use
If port 3000 is already in use, modify the port mapping in `docker-compose.yaml`:
```yaml
ports:
  - "3001:3000"  # Change 3001 to any available port
```

### Database Connection Issues
- Ensure the `.env.db` file exists and has correct credentials
- Check that the database container is healthy: `docker-compose ps`

### Can't Access Dashboard
- Verify the containers are running: `docker-compose ps`
- Check the logs: `docker-compose logs umami-app`
- Ensure you're using the correct URL and port

**Note:** If you are using a reverse proxy such as Traefik, make sure to update the domain in your `docker-compose.yaml` file to match your own domain name.

## Support

- [Official Documentation](https://umami.is/docs)
- [GitHub Repository](https://github.com/umami-software/umami)
- [Community Discussions](https://github.com/umami-software/umami/discussions)

## License

Umami is open-source software licensed under the MIT License.

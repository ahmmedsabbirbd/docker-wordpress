# Docker WordPress Setup

A complete WordPress development environment using Docker Compose with MySQL database and phpMyAdmin.

## 🚀 Features

- **WordPress**: Latest WordPress version running on Apache
- **MySQL 5.7**: Database server for WordPress
- **phpMyAdmin**: Web-based MySQL administration tool
- **Persistent Data**: Database data persists across container restarts
- **Network Isolation**: All services communicate through a dedicated Docker network

## 📋 Prerequisites

- Docker
- Docker Compose

## 🛠️ Services

### 1. WordPress (`wordpress`)
- **Image**: `wordpress:latest`
- **Port**: `8080` (host) → `80` (container)
- **Volume**: Current directory mounted to `/var/www/html`
- **Database**: Connects to MySQL database

### 2. MySQL Database (`db`)
- **Image**: `mysql:5.7`
- **Port**: Internal only (3306)
- **Volume**: `db_data` for persistent storage
- **Credentials**:
  - Root Password: `password`
  - Database: `wordpress`
  - User: `wordpress`
  - Password: `wordpres` (note: typo in docker-compose.yaml)

### 3. phpMyAdmin (`phpmyadmin`)
- **Image**: `phpmyadmin/phpmyadmin`
- **Port**: Internal only
- **Purpose**: Database administration interface

## 🚀 Quick Start

1. **Clone or download this project**
   ```bash
   git clone <repository-url>
   cd docker-wordpress
   ```

2. **Start the services**
   ```bash
   docker-compose up -d
   ```

3. **Access WordPress**
   - Open your browser and go to: `http://localhost:8080`
   - Follow the WordPress installation wizard

4. **Access phpMyAdmin** (optional)
   - phpMyAdmin is available internally but not exposed to host
   - To access it, you can either:
     - Add port mapping in docker-compose.yaml: `"8081:80"`
     - Or use: `docker-compose exec phpmyadmin bash`

## 📁 Project Structure

```
docker-wordpress/
├── docker-compose.yaml    # Docker Compose configuration
├── README.md             # This file
└── [WordPress files]     # WordPress files will be created here
```

## ⚙️ Configuration

### Environment Variables

The following environment variables are configured:

**Database (`db`)**:
- `MYSQL_ROOT_PASSWORD`: `password`
- `MYSQL_DATABASE`: `wordpress`
- `MYSQL_USER`: `wordpress`
- `MYSQL_PASSWORD`: `wordpres`

**WordPress (`wordpress`)**:
- `WORDPRESS_DB_HOST`: `db:3306`
- `WORDPRESS_DB_USER`: `wordpress`
- `WORDPRESS_DB_PASSWORD`: `wordpres`

### Volumes

- `db_data`: Persistent MySQL data storage
- `./:/var/www/html`: Current directory mounted to WordPress root

### Networks

- `wpNetwork`: Custom network for inter-service communication

## 🛠️ Management Commands

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
# All services
docker-compose logs

# Specific service
docker-compose logs wordpress
docker-compose logs db
docker-compose logs phpmyadmin
```

### Restart Services
```bash
docker-compose restart
```

### Remove Everything (including volumes)
```bash
docker-compose down -v
```

## 🔧 Troubleshooting

### Common Issues

1. **Port 8080 already in use**
   - Change the port mapping in `docker-compose.yaml`:
     ```yaml
     ports:
       - "8081:80"  # Use 8081 instead of 8080
     ```

2. **Database connection issues**
   - Check if the database password matches in both `db` and `wordpress` services
   - Note: There's a typo in the current configuration (`wordpres` instead of `wordpress`)

3. **Permission issues with WordPress files**
   - The current directory is mounted as a volume, ensure proper permissions

### Reset Everything

To completely reset the environment:

```bash
# Stop and remove containers, networks, and volumes
docker-compose down -v

# Remove WordPress files (if any)
rm -rf wp-*

# Start fresh
docker-compose up -d
```

## 🔒 Security Notes

⚠️ **Important**: This setup is for development purposes only!

- Default passwords are used for simplicity
- Database is accessible from the host network
- Consider changing default credentials for production use
- The database password has a typo (`wordpres` instead of `wordpress`)

## 📝 Notes

- WordPress files will be created in the current directory
- Database data persists in the `db_data` volume
- All services restart automatically if the Docker daemon restarts
- phpMyAdmin is not exposed to the host by default

## 🤝 Contributing

Feel free to submit issues and enhancement requests!

## 📄 License

This project is open source and available under the [MIT License](LICENSE).

## 🌐 Connect With Me

Stay connected and follow my journey:

- **GitHub**: [@ahmmedsabbirbd](https://github.com/ahmmedsabbirbd)
- **LinkedIn**: [Sabbir Ahmmed](https://linkedin.com/in/ahmmedsabbirbd)
- **Twitter**: [@ahmmedsabbirbd](https://twitter.com/ahmmedsabbirbd)
- **Instagram**: [@ahmmedsabbirbd](https://instagram.com/ahmmedsabbirbd)
- **Facebook**: [Sabbir Ahmmed](https://facebook.com/ahmmedsabbirbd)
- **YouTube**: [Your Channel](https://youtube.com/@ahmmedsabbirbd)
- **Portfolio**: [yourwebsite.com](https://ahmmedsabbirbd.github.io/)
- **Email**: your.email@example.com

---

⭐ **If this project helped you, please give it a star!**

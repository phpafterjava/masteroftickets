# MasterOfTickets

A web application for comparing ticket prices for concerts, shows, and events in real-time.

## 🎯 Objective

MasterOfTickets helps users find the best ticket deals by comparing prices from various official and secondary ticketing platforms.

## 🛠️ Tech Stack

- **Backend**: Symfony [VERSION_TO_BE_DETERMINED] (PHP 8.2+)
- **Frontend**: Vue.js [LATEST_VERSION] (with Vite for build)
- **Infrastructure**: Docker & Docker Compose
- **Database**: PostgreSQL 15 (user: postgres, password: postgres)
- **Cache**: Redis [VERSION_TO_BE_DETERMINED]
- **API**: RESTful [WITH/WITHOUT API Platform - TO BE DECIDED]

## 🐳 Docker Installation

### Prerequisites
- Docker Engine [MINIMUM_VERSION]+
- Docker Compose V2+
- Git

### Installation Steps

1. **Clone the repository**
```bash
git clone [REPOSITORY_URL]
cd masteroftickets
```

2. **Copy environment configuration files**
```bash
cp .env.example .env
cp docker-compose.override.example.yml docker-compose.override.yml
```

3. **Build and start containers**
```bash
docker compose up --build -d
```

4. **Install PHP dependencies**
```bash
docker compose exec php composer install
```

5. **Install JavaScript dependencies**
```bash
docker compose exec node npm install
```

6. **Run database migrations**
```bash
docker compose exec php php bin/console doctrine:migrations:migrate
```

7. **Load test data (optional)**
```bash
docker compose exec php php bin/console doctrine:fixtures:load
```

8. **Compile frontend assets**
```bash
docker compose exec node npm run dev
```

> **Note**: Ensure Docker Desktop is running before executing these commands.

## 🚀 Usage

The application will be accessible at:
- **Frontend**: http://localhost:[FRONTEND_PORT]
- **Backend API**: http://localhost:[BACKEND_PORT]
- **phpMyAdmin** (for DB management): http://localhost:[PHPMYADMIN_PORT]
- **MailHog** (for email testing): http://localhost:[MAILHOG_PORT]

## 📁 Project Structure

```
masteroftickets/
├── infra/                   # Docker configuration
│   ├── php/                 # PHP/Symfony Dockerfile
│   │   └── Dockerfile
│   ├── node/                # Node/Vue Dockerfile
│   │   └── Dockerfile
│   └── nginx/               # Nginx configuration
│       └── conf.d/
│           └── default.conf
├── backend/                 # Symfony application
│   ├── config/              # Symfony configuration
│   ├── src/                 # PHP source code
│   │   ├── Controller/      # API controllers
│   │   ├── Entity/          # Doctrine entities
│   │   ├── Repository/      # Doctrine repositories
│   │   └── Service/         # Business services
│   ├── templates/           # Twig templates (if used)
│   ├── translations/        # Translation files
│   └── var/                 # Cache, logs, etc.
├── frontend/                # Vue.js application
│   ├── public/              # Static assets
│   ├── src/                 # Vue source code
│   │   ├── assets/          # Images, styles, etc.
│   │   ├── components/      # Reusable Vue components
│   │   ├── composables/     # Composable functions
│   │   ├── pages/           # Application pages
│   │   ├── router/          # Routing configuration
│   │   ├── store/           # Global state (Pinia)
│   │   └── utils/           # Utility functions
│   ├── tests/               # Unit and integration tests
│   └── vite.config.js       # Vite configuration
├── docker-compose.yml       # Main Docker Compose configuration
├── docker-compose.override.yml # Development configuration (not to be committed)
├── .env                     # Environment variables
├── README.md                # This file
└── ...                      # Other configuration files
```

## 🔧 Configuration

### Environment Variables (.env)

Copy `.env.example` to `.env` and adjust values:

```env
###> symfony/framework ###
APP_ENV=[dev/prod]
APP_SECRET=[GENERATED_TOKEN]
TRUSTED_PROXIES=[IP_ADDRESSES]
TRUSTED_HOSTS=[REGEX_PATTERN]
###< symfony/framework ###

###> doctrine/doctrine-bundle ###
DATABASE_URL="postgresql://postgres:postgres@db:5432/masteroftickets?serverVersion=15&charset=utf8"
###< doctrine/doctrine-bundle ###

###> predis/predis-client ###
REDIS_URL="redis://[HOST]:[PORT]"
###< predis/predis-client ###

### Custom variables ###
APP_FRONTEND_URL=[FRONTEND_URL]
API_BASE_URL=[BACKEND_URL]
```

### Exposed Ports

| Service | Port | Description |
|---------|------|-------------|
| Nginx (Backend) | [PORT_TO_BE_DETERMINED] | Symfony API |
| Vue Dev Server | [PORT_TO_BE_DETERMINED] | Vite development server |
| PostgreSQL | 5432 | Database |
| Redis | [PORT_TO_BE_DETERMINED] | Cache |
| phpMyAdmin | [PORT_TO_BE_DETERMINED] | Database interface |
| MailHog | [PORT_TO_BE_DETERMINED] | Email capture |

## 🧪 Testing

### Backend (PHPUnit)
```bash
docker compose exec php php bin/phpunit
```

### Frontend (Vitest)
```bash
docker compose exec node npm run test
```

### End-to-End Tests ([CYRESS/PLAYWRIGHT - TO BE SELECTED])
```bash
docker compose exec node npm run test:e2e
```

## 📦 Production Deployment

For production deployment:

```bash
# Use production compose file
docker compose -f docker-compose.yml -f docker-compose.prod.yml up --build -d

# Build production assets
docker compose exec node npm run build
```

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

### Coding Conventions

- **PHP**: PSR-[STANDARD_NUMBER] with [TOOL_NAME]
- **JavaScript/Vue**: ESLint with [CONFIG_NAME] + Prettier
- **Commit messages**: [CONVENTIONAL_COMMITS/OTHER_FORMAT]

## 🐛 Bug Reports

Please use the [GitHub Issues]([ISSUES_URL]) system to report bugs or request features.

## 📄 License

This project is licensed under the [LICENSE_TYPE] License - see the [LICENSE_FILE] file for details.

## 🙏 Acknowledgments

- [SYMFONY_VERSION] for the robust PHP framework
- [VUE_VERSION] for the reactive frontend
- [DOCKER_VERSION] for simplified containerization
- All ticketing platforms whose data we aggregate (via their public APIs)

---

*Developed with ❤️ for event lovers who want to save on tickets!*
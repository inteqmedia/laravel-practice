# 🚀 Laravel DevOps Setup (Docker + Nginx + PHP-FPM)

## 🧱 Stack Used
- PHP 8.3 (Laravel compatible)
- Nginx (reverse proxy)
- Laravel (inside container)
- Docker Compose (orchestration)
- SQLite (initial testing)

---

## ⚙️ Setup Flow

### 1. Infrastructure Setup
- Created docker-compose.yml at project root
- Defined two services:
  - laravel-app (PHP-FPM)
  - laravel-nginx (web server)

---

### 2. Laravel Container Setup
- Built Laravel inside Docker container
- Installed dependencies using Composer
- Mounted application into `/var/www`

---

### 3. Nginx Setup
- Configured reverse proxy
- Root path: `/var/www/public`
- PHP requests forwarded to `laravel-app:9000`

---

### 4. Common Issues Fixed

#### ❌ PHP Version Error
- Fixed mismatch (8.2 → 8.3)

#### ❌ Composer Platform Errors
- Installed missing PHP extensions (xml, dom, curl, mbstring)

#### ❌ Docker COPY Path Issues
- Fixed incorrect `../src` usage
- Standardized build context to project root

#### ❌ Nginx Mount Error
- Fixed missing `default.conf`
- Ensured correct file binding in docker-compose

#### ❌ SQLite Missing File
- Created `/database/database.sqlite`
- Updated `.env` database path

#### ❌ Database Migration Errors
- Ran `php artisan migrate`

#### ❌ Permission Errors
- Fixed storage and bootstrap permissions
```bash
chmod -R 777 storage bootstrap/cache

php artisan key:generate

Note: no need to run any commands manually example php artisan, docker compose up, only one command is enough that is ansible command
Errors: path mismatch, reverse-proxy port not mentioned, mainly laravel-react nginx.conf.j2 (inside roles) make sure you check logs of reverse-proxy container to know more about the error
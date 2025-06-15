# Docker Base Images Collection

A collection of ready-to-use Docker base images for various development environments and services.

## 🚀 Quick Start

1. Clone this repository:
```bash
git clone https://github.com/jerryagenyi/docker-base-images.git
```

2. Navigate to your project directory and reference these base images in your `docker-compose.yaml`:
```yaml
services:
  myapp:
    build:
      context: ../docker-base-images/python-base  # Relative path to base image
      dockerfile: Dockerfile
```

## 📦 Available Base Images

### Development Environments

#### 🐍 Python Base
- Base image: `python:3.10`
- Pre-installed packages: pytest, requests, python-dotenv, flask
- Automatically installs project-specific requirements.txt
- Common ports: 8000 (Flask/Django), 8888 (Jupyter)

#### 📦 Node.js Base
- Base image: `node:18`
- Automatically installs package.json dependencies
- Default port: 3000

### Data Science & ML

#### 🐍 Miniconda
- Base image: `continuumio/miniconda3`
- Support for environment.yml configuration
- Ideal for data science projects

#### 🔥 PyTorch
- Base image: `pytorch/pytorch:latest`
- Includes numpy, pandas, scikit-learn
- GPU support ready (configurable)

### Web Servers

#### 🌐 Nginx
- Base image: `nginx:latest`
- Port: 80
- Configurable through default.conf

#### 🟢 Caddy
- Base image: `caddy:latest`
- Ports: 80, 443
- Automatic HTTPS
- Volume support for data and config

### Database

#### 🐘 PostgreSQL
- Base image: `postgres:latest`
- Port: 5432
- Configurable through environment variables
- Persistent volume support

### Testing

#### 🌐 Selenium
- Base image: `selenium/standalone-chrome`
- Ready for browser testing
- Python test script support

## 🔧 Usage

### Directory Structure
```
your-projects/
├── docker-base-images/          # This repository
│   ├── python-base/
│   ├── node-base/
│   ├── miniconda/
│   └── ...
│
└── your-project/               # Your actual project
    ├── src/
    ├── requirements.txt
    └── docker-compose.yaml     # References base images
```

### Example Usage

1. **Python Web Application**
```yaml
# your-project/docker-compose.yaml
services:
  webapp:
    build:
      context: ../docker-base-images/python-base
      dockerfile: Dockerfile
    volumes:
      - ./:/app
    ports:
      - "8000:8000"
```

2. **AI Development Environment**
```yaml
services:
  ml-environment:
    build:
      context: ../docker-base-images/pytorch
      dockerfile: Dockerfile
    volumes:
      - ./:/app
    deploy:
      resources:
        reservations:
          devices:
            - driver: nvidia
              count: all
              capabilities: [gpu]
```

### Common Ports Reference

| Service    | Port | Usage                    |
|------------|------|--------------------------|
| Python     | 8000 | Flask/Django/FastAPI     |
| Python     | 8888 | Jupyter Notebooks        |
| Node.js    | 3000 | Express/Next.js          |
| PostgreSQL | 5432 | Database                 |
| Nginx      | 80   | HTTP                     |
| Caddy      | 80   | HTTP                     |
| Caddy      | 443  | HTTPS                   |

## 🔄 Updating Base Images

To update the base images to their latest versions:

```bash
docker-compose build --no-cache
```

## 📝 Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

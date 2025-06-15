# Allow Python version to be configured at build time
ARG PYTHON_VERSION=3.10
FROM python:${PYTHON_VERSION}

WORKDIR /app

# Install common packages that most Python projects need
RUN pip install --no-cache-dir \
    pytest \
    requests \
    python-dotenv \
    flask

# requirements.txt from the project will be mounted at runtime
CMD ["python", "app.py"]
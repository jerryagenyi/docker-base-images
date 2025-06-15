ARG PYTHON_VERSION=3.10
ARG BASE_IMAGE=python:${PYTHON_VERSION}-slim

FROM ${BASE_IMAGE}

LABEL maintainer="Jerry Agenyi"
LABEL description="Hardware-agnostic ML/DL base image"

# System dependencies
RUN apt-get update && apt-get install -y \
    build-essential \
    git \
    curl \
    && rm -rf /var/lib/apt/lists/*

# Install common ML/DL packages without PyTorch
RUN pip install --no-cache-dir \
    numpy \
    pandas \
    scikit-learn \
    matplotlib \
    seaborn \
    jupyter \
    tensorboard \
    opencv-python-headless \
    albumentations

# Install development tools
RUN pip install --no-cache-dir \
    pytest \
    black \
    isort \
    jupyter-lab

# Create non-root user
RUN useradd -m -s /bin/bash ml-user && \
    mkdir -p /app && \
    chown ml-user:ml-user /app

# Set up working directory
WORKDIR /app

# Switch to non-root user
USER ml-user

# Environment variables for better Python behavior
ENV PYTHONUNBUFFERED=1 \
    PYTHONDONTWRITEBYTECODE=1 \
    PIP_NO_CACHE_DIR=1

# Script to install additional requirements (including PyTorch)
COPY --chown=ml-user:ml-user <<-"EOT" /app/entrypoint.sh
#!/bin/bash
if [ -f requirements.txt ]; then
    pip install --user -r requirements.txt
fi
exec "$@"
EOT

RUN chmod +x /app/entrypoint.sh

ENTRYPOINT ["/app/entrypoint.sh"]
CMD ["python", "-m", "jupyter", "lab", "--ip=0.0.0.0", "--allow-root", "--no-browser"]
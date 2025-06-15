FROM pytorch/pytorch:latest
WORKDIR /app

# Install common ML/DL packages
RUN pip install --no-cache-dir \
    numpy \
    pandas \
    scikit-learn \
    matplotlib \
    seaborn \
    jupyter \
    tensorboard \
    torchvision \
    torchaudio \
    transformers \
    opencv-python-headless \
    albumentations

# Install development tools
RUN pip install --no-cache-dir \
    pytest \
    black \
    isort \
    jupyter-lab

# Script to install additional requirements
COPY <<-"EOT" /app/entrypoint.sh
#!/bin/bash
if [ -f requirements.txt ]; then
    pip install -r requirements.txt
fi
exec "$@"
EOT

RUN chmod +x /app/entrypoint.sh

ENTRYPOINT ["/app/entrypoint.sh"]
CMD ["python", "train.py"]
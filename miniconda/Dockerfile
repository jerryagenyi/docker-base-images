FROM continuumio/miniconda3
WORKDIR /app

# Create a default environment with common data science packages
RUN conda create -n base_env python=3.10 \
    numpy \
    pandas \
    matplotlib \
    seaborn \
    scikit-learn \
    jupyter \
    ipykernel \
    && conda clean -afy

# Copy environment setup script
COPY <<-"EOT" /app/setup-env.sh
#!/bin/bash
if [ -f environment.yml ]; then
    # If environment.yml exists, create new environment
    conda env create -f environment.yml
    ENV_NAME=$(head -n 1 environment.yml | cut -d' ' -f2)
else
    # Use base environment
    ENV_NAME=base_env
fi
exec conda run --no-capture-output -n $ENV_NAME "$@"
EOT

RUN chmod +x /app/setup-env.sh

ENTRYPOINT ["/app/setup-env.sh"]
CMD ["python", "app.py"]
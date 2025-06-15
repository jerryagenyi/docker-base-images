FROM continuumio/miniconda3
WORKDIR /app
COPY environment.yml .
RUN conda env create -f environment.yml
ENTRYPOINT ["conda", "run", "--no-capture-output", "-n", "myenv"]
CMD ["python", "app.py"]
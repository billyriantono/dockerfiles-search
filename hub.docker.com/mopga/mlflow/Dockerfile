FROM continuumio/miniconda3

RUN apt-get update && apt-get install -y curl git && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

RUN mkdir -p /mlflow/store && \
    mkdir -p /mlflow/artifacts && \
    mkdir -p /mlflow/github

RUN pip install mlflow[extras] && \
    git clone https://github.com/mlflow/mlflow.git /mlflow/github

RUN pip install mlflow==1.1.0

ENV MLFLOW_TRACKING_URI=http://localhost:5000
CMD mlflow server \
    --backend-store-uri file://mlflow/store \
    --default-artifact-root file://mlflow/artifacts \
    --host 0.0.0.0

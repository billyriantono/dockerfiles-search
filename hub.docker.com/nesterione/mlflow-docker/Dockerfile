FROM python:3.7.0-stretch

ENV MLFLOW_SERVER_HOST 0.0.0.0

ENV BACKEND_STORE_URI /mlruns

ENV DEFAULT_ARTIFACT_ROOT /mlruns

WORKDIR /

COPY . /

RUN apt-get update

RUN pip install -r req.txt

RUN mkdir /mlruns

EXPOSE 5000 

CMD mlflow server --backend-store-uri ${BACKEND_STORE_URI} --default-artifact-root ${DEFAULT_ARTIFACT_ROOT} --host ${MLFLOW_SERVER_HOST}

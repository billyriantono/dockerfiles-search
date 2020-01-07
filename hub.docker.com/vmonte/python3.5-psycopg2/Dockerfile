FROM python:3.5-slim

RUN apt-get update \
    && apt-get install -y libpq-dev python3-dev build-essential

ENV BASE_PROJECT_FOLDER /home/dev/

RUN mkdir -p ${BASE_PROJECT_FOLDER}
RUN mkdir -p ${BASE_PROJECT_FOLDER}/project
RUN mkdir -p /var/log/

EXPOSE 8000

WORKDIR ${BASE_PROJECT_FOLDER}/project

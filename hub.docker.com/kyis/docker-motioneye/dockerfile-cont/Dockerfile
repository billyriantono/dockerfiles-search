FROM openjdk:8

ENV TZ="Asia/Hong_Kong"
ENV LANG C.UTF-8

RUN sh -c 'touch /app.jar' \
 && apt-get update && apt-get upgrade -y \
 && apt-get install python python-pip tar -y \
 && pip install --upgrade pip awscli 

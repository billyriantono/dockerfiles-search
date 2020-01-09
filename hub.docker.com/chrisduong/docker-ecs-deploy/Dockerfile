FROM python:2.7-alpine

LABEL version="1.0"  maintainer="Chris Duong <chrisduong83@gmail.com>"

RUN pip install boto3

WORKDIR /root/dev

ADD ecs_deploy.py .

CMD ["python", "ecs_deploy.py"]

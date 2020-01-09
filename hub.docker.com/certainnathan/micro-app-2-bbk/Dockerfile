FROM ubuntu:latest
MAINTAINER Nathan Coulson "nathancoulson@gmail.com"
RUN apt-get update -y
RUN apt-get install -y python-pip python-dev build-essential
ADD . /app_2
WORKDIR /app_2
RUN pip install -r requirements.txt
ENTRYPOINT ["python"]
CMD ["app2.py"]
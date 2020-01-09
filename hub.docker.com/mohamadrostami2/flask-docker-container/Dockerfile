FROM ubuntu

LABEL MAINTAINER="mohamadrezarostami2@gmail.com"

RUN apt update -y
RUN apt install -y -q python3
RUN apt install -y -q python3-pip
RUN pip3 install flask

COPY . /app
WORKDIR /app

ENV FLASK_APP=app.py
ENV FLASK_ENV=development
ENV FLASK_DEBUG=1

CMD ["python3","app.py"]

FROM ubuntu:18.10
LABEL maintainer "Sergio Sánchez Vallés <serindio@gmail.com>"

RUN apt update -y && apt upgrade -y && apt install imagemagick -y
RUN apt install -y python3-pip python3-dev \
  && cd /usr/local/bin \
  && ln -s /usr/bin/python3 python \
  && pip3 install --upgrade pip
WORKDIR /usr/src/app

COPY requirements.txt ./
RUN pip3 install --no-cache-dir -r requirements.txt

COPY . .

CMD [ "python", "./distortbot.py" ]


FROM ubuntu:trusty
MAINTAINER dj80hd "werwath@gmail.com"
RUN apt-get update -y
RUN apt-get install -y python-pip \
python-dev \
build-essential \
git \
curl \
python-virtualenv

WORKDIR /app
RUN cd /app & git clone https://github.com/dj80hd/SimpleFlask.git
RUN cd SimpleFlask && pip install -r requirements.txt
EXPOSE 5000
WORKDIR /app/SimpleFlask
COPY ./entrypoint.sh /app/SimpleFlask/
RUN pip install -r requirements.txt
CMD ["./entrypoint.sh"]

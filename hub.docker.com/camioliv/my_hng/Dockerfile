FROM python:3.6
MAINTAINER Tom Dryer <tomdryer.com@gmail.com>

RUN useradd --create-home hangups
USER hangups
WORKDIR /home/hangups

COPY hangups ./hangups
COPY setup.py README.rst ./
RUN pip install --user .
RUN mkdir -p .cache/hangups .config/hangups

VOLUME ["/home/hangups/.config/hangups", "/home/hangups/.cache/hangups"]
ENTRYPOINT [".local/bin/hangups"]

ENV http_proxy http://camila.oliveira:agrotis1005@192.168.0.221:3128 
ENV https_proxy http://camila.oliveira:agrotis1005@192.168.0.221:3128
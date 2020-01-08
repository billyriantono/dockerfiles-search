FROM debian:buster

RUN printf "deb http://deb.debian.org/debian buster-backports main" >> /etc/apt/sources.list

RUN apt-get update -qq -y && \
    apt-get install -qq -y xvfb golang git && \
    apt-get -t buster-backports install -y qgis python3-qgis

VOLUME "/cache"
EXPOSE 5000

ENV PYTHONPATH="/usr/lib/python3/dist-packages/"
ENV DISPLAY ":99"
ENV APP /app
ENV SWEREF_CACHE_FOLDER /cache

RUN mkdir $APP
WORKDIR $APP

COPY ./requirements.txt .
RUN pip3 install -r requirements.txt

COPY . .

CMD "./start-prod.sh"

FROM python:2

MAINTAINER mail@nasourso.com

RUN mkdir /data

VOLUME /data

RUN mkdir /app

WORKDIR /app

ADD image.txt /app

ADD run.sh /app

ADD https://raw.githubusercontent.com/C0D3D3V/Moodle-Downloader/master/src/moodleCrawler.py /app

RUN chmod +x run.sh && apt-get update && apt-get install python-beautifulsoup -y && pip install beautifulsoup4 && easy_install lxml && pip install colorama && pip install termcolor && apt-get clean

CMD ["./run.sh"]


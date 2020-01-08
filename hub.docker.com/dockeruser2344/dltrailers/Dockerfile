FROM linuxserver/tautulli:latest

RUN pip install tmdbsimple==2.2.0 &&\
    pip install youtube-dl==2019.4.24 &&\
    pip install unidecode==1.1.0

ADD https://raw.githubusercontent.com/airship-david/Trailer-Downloader/master/download.py /scripts/download.py

RUN chmod +x /scripts/download.py &&\
    mkdir /scripts/downloads &&\
    chmod 777 /scripts/download.py &&\
    chmod 666 /scripts/downloads

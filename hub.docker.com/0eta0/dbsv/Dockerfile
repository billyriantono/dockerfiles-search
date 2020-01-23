FROM python:3

WORKDIR /dbsv

RUN apt-get update
RUN apt-get -y install libev-dev openssl busybox-static

COPY ./requirements.txt ./requirements.txt
COPY ./package ./package
COPY ./main.py ./main.py
COPY ./uwsgi.ini ./uwsgi.ini
COPY ./ecdsa.sh ./ecdsa.sh
COPY ./start.sh ./start.sh
COPY ./crontab /var/spool/cron/crontabs/root

RUN pip install --upgrade pip
RUN pip install --no-cache-dir -r requirements.txt
RUN chmod 700 -R ./

EXPOSE 8008

CMD ["./start.sh" ] 

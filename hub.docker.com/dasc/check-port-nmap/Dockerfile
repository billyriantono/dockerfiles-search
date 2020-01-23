FROM python:3

ADD src/*.py /

RUN pip install Flask nmap flask-restful flask-jsonpify sqlalchemy

CMD [ "python", "./check-port-nmap.py" ]

EXPOSE 5021/tcp

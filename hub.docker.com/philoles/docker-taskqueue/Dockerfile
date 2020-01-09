FROM python:3.6

# copy data

RUN mkdir -p /usr/src/taskqueue
COPY data/src.tar /usr/src/taskqueue/
WORKDIR /usr/src/taskqueue
RUN tar -xf src.tar
RUN pip install -r requirements.txt

COPY data/docker-entrypoint.sh /usr/local/bin/docker-entrypoint.sh
RUN chmod +x /usr/local/bin/docker-entrypoint.sh
ENTRYPOINT ["/usr/local/bin/docker-entrypoint.sh"]

CMD ["celery", "-A", "qworker", "worker", "-l", "info"]

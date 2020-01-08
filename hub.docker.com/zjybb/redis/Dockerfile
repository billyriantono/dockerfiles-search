FROM redis:5.0.6

COPY master.conf /redis-master/redis.conf
COPY slave.conf /redis-slave/redis.conf
COPY run.sh /run.sh

RUN chmod a+x /run.sh

VOLUME /data

CMD [ "/run.sh" ]

ENTRYPOINT [ "bash", "-c" ]
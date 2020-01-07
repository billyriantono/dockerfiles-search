FROM openshine/spark-worker-base:latest
MAINTAINER Roberto Majadas <roberto.majadas@openshine.com>

COPY start.sh /usr/local/bin/

# Create directory where data will be mounted on all workers
ENV DATA_DIR /data
RUN mkdir -p $DATA_DIR

EXPOSE 8081/tcp

CMD ["start.sh"]

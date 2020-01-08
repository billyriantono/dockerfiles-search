FROM sos3k/hadoop-spark
MAINTAINER Radoslaw Wojciechowski <radoslaw.wojciechowski@gmail.com>

ADD spark-worker-entrypoint.sh /spark-worker-entrypoint.sh
RUN chmod a+x /spark-worker-entrypoint.sh

ENTRYPOINT ["/spark-worker-entrypoint.sh"]

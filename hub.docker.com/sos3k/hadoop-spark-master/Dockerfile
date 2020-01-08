FROM sos3k/hadoop-spark
MAINTAINER Radoslaw Wojciechowski <radoslaw.wojciechowski@gmail.com>

ADD spark-master-entrypoint.sh /spark-master-entrypoint.sh
RUN chmod a+x /spark-master-entrypoint.sh

ENTRYPOINT ["/spark-master-entrypoint.sh"]

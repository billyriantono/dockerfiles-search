FROM shuaicj/spark:2.1.1
MAINTAINER shuaicj <shuaicj@gmail.com>

ADD start-spark-master.sh /sbin/

EXPOSE 6066 7077 8080

ENTRYPOINT ["/sbin/start-spark-master.sh"]

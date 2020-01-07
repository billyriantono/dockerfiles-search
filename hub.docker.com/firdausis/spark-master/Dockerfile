FROM smduarte/spark-master

MAINTAINER Firdaus Ismail Sholeh (firdaus_is@yahoo.com)

ADD spark-defaults.conf /conf/spark-default.conf
# Set environment variables.
ENV SPARK_CONF_DIR /conf

EXPOSE 7001 7002 7003 7004 7005 7006 7077 6066 4040 6066 7077 8080
    
CMD /usr/spark/bin/spark-class org.apache.spark.deploy.master.Master -h master

ADD FrequentRoutes.jar /root/FrequentRoutes.jar
# Set environment variables.
ENV HOME /root

# Define working directory.
WORKDIR /root

ENTRYPOINT ["java", "-Djava.security.egd=file:/dev/urandom"]

# Define default command.
# CMD ["-jar", "/root/FrequentRoutes.jar", "/usr/spark", "lovelymachine1.cloudapp.net:9092", "taxi"]
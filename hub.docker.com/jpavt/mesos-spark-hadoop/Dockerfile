FROM mesosphere/spark:1.0.4-2.0.1

WORKDIR /opt/spark/dist

ENV SPARK_SHUFFLE_OPTS "-Dspark.shuffle.service.enabled=true"

ENV SPARK_PRINT_LAUNCH_COMMAND "true"

ENV SPARK_LOCAL_DIRS "/tmp"

ENTRYPOINT ["./bin/spark-class", "org.apache.spark.deploy.mesos.MesosExternalShuffleService"]



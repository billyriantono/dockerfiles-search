FROM jupyter/pyspark-notebook
USER root
RUN wget https://dev.mysql.com/get/Downloads/Connector-J/mysql-connector-java_8.0.11-1ubuntu16.04_all.deb
RUN dpkg -i mysql-connector-java_8.0.11-1ubuntu16.04_all.deb
RUN cp /usr/share/java/mysql-connector-java-8.0.11.jar /usr/local/spark/jars/


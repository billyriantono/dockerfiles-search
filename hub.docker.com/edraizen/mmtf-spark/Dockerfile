FROM quay.io/ucsc_cgl/spark-and-maven

RUN apt-get update && apt-get install -y git

WORKDIR /opt
RUN git clone https://github.com/sbl-sdsc/mmtf-spark.git
ENV PATH=/opt/apache-maven-3.3.9/bin:$PATH
ENV JAVA_HOME=""
ENV SPARK_HOME=/opt/apache-spark

WORKDIR /opt/mmtf-spark
#Skipping tests in not ideal, but it requires the full and reduced mmtfs to be present
RUN mvn install -DskipTests

WORKDIR /opt
RUN mkdir chemcomp
ENV PDB_DIR=/opt/chemcomp
ENV PDB_CACHE_DIR=/opt/chemcomp

COPY wrapper.sh /opt/mmtf-spark

RUN mkdir /data
WORKDIR /data
ENV MMTF_FULL=/data/full
ENV MMTF_REDUCED=/data/reduced

ENTRYPOINT ["sh", "/opt/mmtf-spark/wrapper.sh"]

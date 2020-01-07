FROM jupyter/all-spark-notebook:814ef10d64fb

LABEL maintainer="lbarrientos@opensistemas.com" \
      org.label-schema.vcs-ref=$VCS_REF \
      org.label-schema.build-date=$BUILD_DATE \
      org.label-schema.vcs-url="git@github.com:leonardobarrientosc/jupyter-notebooks-image.git" \
      org.label-schema.docker.dockerfile="/Dockerfile"

ENV SPARK_CONF_DIR /home/jovyan/conf/spark
ENV HADOOP_CONF_DIR /home/jovyan/conf/hadoop
ENV OPENVPN_CONF_DIR /home/jovyan/conf/openvpn
ENV JAVA_HOME /usr/lib/jvm/java-8-openjdk-amd64

USER root

RUN apt-get update && apt-get install --yes \
    openssh-client \
    git \
    libssl-dev \
    gnupg2 \
    vim \ 
    unixodbc-dev \
    g++ \
    libpq-dev \
 && rm -rf /var/lib/apt/lists/*

RUN curl -s https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
RUN curl -s https://packages.microsoft.com/config/ubuntu/18.04/prod.list | tee -a /etc/apt/sources.list.d/mssql-release.list

RUN apt-get update && ACCEPT_EULA=Y  apt-get install --yes \
    msodbcsql17 \
 && rm -rf /var/lib/apt/lists/*

RUN curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add -
RUN echo "deb https://apt.kubernetes.io/ kubernetes-xenial main" | tee -a /etc/apt/sources.list.d/kubernetes.list

RUN apt-get update && apt-get install --yes kubectl 

RUN curl http://central.maven.org/maven2/com/amazonaws/aws-java-sdk/1.7.4/aws-java-sdk-1.7.4.jar -o /usr/local/spark/jars/aws-java-sdk-1.7.4.jar
RUN curl http://central.maven.org/maven2/org/apache/hadoop/hadoop-aws/2.7.7/hadoop-aws-2.7.7.jar -o /usr/local/spark/jars/hadoop-aws-2.7.7.jar
#RUN curl http://maven.twttr.com/com/hadoop/gplcompression/hadoop-lzo/0.4.15/hadoop-lzo-0.4.15.jar -o /usr/local/spark/jars/hadoop-lzo-0.4.15.jar
RUN curl http://central.maven.org/maven2/org/xerial/snappy/snappy-java/1.1.7.2/snappy-java-1.1.7.2.jar -o /usr/local/spark/jars/snappy-java-1.1.7.2.jar


USER $NB_USER
RUN conda install pyarrow fastparquet tensorflow awscli psycopg2 pymongo s3fs scipy scikit-learn requests python-dotenv pyodbc pandas numpy matplotlib seaborn 
RUN conda install -c damianavila82 rise

RUN pip install nbgitpuller && \
    jupyter serverextension enable --py nbgitpuller --sys-prefix
# Uncomment the line below to make nbgitpuller default to start up in JupyterLab
#ENV NBGITPULLER_APP=lab
RUN jupyter-nbextension install rise --py --sys-prefix
RUN jupyter-nbextension enable rise --py --sys-prefix
FROM debian:8

# install basic packages
RUN apt-get update --fix-missing && \
  apt-get -y upgrade && \
  apt-get install -y curl git man bzip2 ca-certificates unzip vim wget && \
  apt-get install -y software-properties-common  

# install java
RUN echo "deb http://ppa.launchpad.net/webupd8team/java/ubuntu xenial main" | tee /etc/apt/sources.list.d/webupd8team-java.list && \
  echo "deb-src http://ppa.launchpad.net/webupd8team/java/ubuntu xenial main" | tee -a /etc/apt/sources.list.d/webupd8team-java.list && \
  apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys EEA14886 && \
  apt-get update -y && \
  apt-get upgrade -y && \
  echo debconf shared/accepted-oracle-license-v1-1 select true | debconf-set-selections && \
  echo debconf shared/accepted-oracle-license-v1-1 seen true | debconf-set-selections && \
  apt-get install -y oracle-java8-installer -f

WORKDIR /home

# install spark
RUN wget --quiet https://archive.apache.org/dist/spark/spark-2.2.0/spark-2.2.0-bin-hadoop2.7.tgz && \
    tar -zxvf spark-2.2.0-bin-hadoop2.7.tgz && \
    mv spark-2.2.0-bin-hadoop2.7 /usr/local/spark && \
    rm -f spark-2.2.0-bin-hadoop2.7.tgz

# set env vars
ENV PATH /usr/local/spark/bin:$PATH
ENV SPARK_HOME=/usr/local/spark 
ENV PYTHONPATH=$SPARK_HOME/python/:$PYTHONPATH
ENV PYSPARK_PYTHON=/usr/bin/python3

# install pip3 and python libs
RUN apt-get install -y python3-pip && \
  pip3 install findspark py4j && \
  python3 -m pip install --upgrade pip && \
  python3 -m pip install jupyter && \
  pip3 install numpy

# set env vars
ENV PYSPARK_DRIVER_PYTHON=jupyter
ENV PYSPARK_DRIVER_PYTHON_OPTS="notebook"

CMD ["bash"]

FROM ubuntu:18.04

MAINTAINER Mathijs van Westendorp <mvwestendorp@gmail.com>

ENV ENABLE_INIT_DAEMON true
ENV INIT_DAEMON_BASE_URI http://identifier/init-daemon
ENV INIT_DAEMON_STEP spark_master_init

ENV SPARK_VERSION=2.4.4
ENV HADOOP_VERSION=2.7

COPY /wait-for-step.sh /
COPY /execute-step.sh /
COPY /finish-step.sh /

ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update && apt-get upgrade -y
RUN apt-get install -y openjdk-8-jre wget python3-pip r-base\

      && chmod +x *.sh \
      && wget https://archive.apache.org/dist/spark/spark-${SPARK_VERSION}/spark-${SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz \
      && tar -xvzf spark-${SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz \
      && mv spark-${SPARK_VERSION}-bin-hadoop${HADOOP_VERSION} spark \
      && rm spark-${SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz

#Give permission to execute scripts
RUN chmod +x /wait-for-step.sh && chmod +x /execute-step.sh && chmod +x /finish-step.sh
RUN pip3 install tensorflow plotly plotly_express
RUN R -e "install.packages(c('knitr', 'ggplot2', 'devtools', 'mplot', 'googleVis', 'sqldf', 'glmnet', 'pROC', 'data.table', 'caret', 'wordcloud'), repos = 'http://cran.us.r-project.org')"

# Fix the value of PYTHONHASHSEED
# Note: this is needed when you use Python 3.3 or greater
ENV PYTHONHASHSEED 1

FROM bde2020/spark-base:2.2.0-hadoop2.7

MAINTAINER Erika Pauwels <erika.pauwels@tenforce.com>
MAINTAINER Gezim Sejdiu <g.sejdiu@gmail.com>

COPY master.sh /

RUN cd /home \
	  && wget https://bootstrap.pypa.io/get-pip.py \
      && python get-pip.py \
      && export SPARK_HOME=/spark \
      && apt-get update \
      && apt-get install -y build-essential python-dev \
      && pip install -q jupyter \
      && pip install https://dist.apache.org/repos/dist/dev/incubator/toree/0.2.0-incubating-rc2/toree-pip/toree-0.2.0.tar.gz \
      && jupyter toree install --spark_home=$SPARK_HOME --kernel_name="Spark Scala" \
	  && jupyter toree install --spark_home=$SPARK_HOME --interpreters=PySpark --kernel_name="Spark Python" \
      && pip install jupyter-spark \
	  && jupyter serverextension enable --py jupyter_spark \
	  && jupyter nbextension install --py jupyter_spark \
	  && jupyter nbextension enable --py jupyter_spark \
	  && jupyter nbextension enable --py widgetsnbextension

ENV SPARK_MASTER_PORT 7077
ENV SPARK_MASTER_WEBUI_PORT 8080
ENV SPARK_MASTER_JUPYTER_PORT 8888
ENV SPARK_MASTER_LOG /spark/logs

EXPOSE 8080 7077 6066 8888
 
CMD ["/bin/bash", "/master.sh"]
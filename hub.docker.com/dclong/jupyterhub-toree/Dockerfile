FROM dclong/jupyterhub-jdk

ARG spark=spark-2.4.1
ARG spark_hdp=$spark-bin-hadoop2.7

RUN apt-get update \
    && apt-get install -y scala \
    && wget http://us.mirrors.quenda.co/apache/spark/$spark/$spark_hdp.tgz -O /$spark_hdp.tgz \
    && tar -zxvf /$spark_hdp.tgz -C /opt/ \
    && rm /$spark_hdp.tgz

RUN pip3 install toree \
    && jupyter toree install --spark_home=/opt/$spark_hdp/

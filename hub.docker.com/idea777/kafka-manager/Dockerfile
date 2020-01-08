FROM reiniergs/centos7-jdk-node8-browsers

USER root
ADD https://github.com/yahoo/kafka-manager/archive/2.0.0.2.tar.gz /mnt/

RUN ls -tlsh  /mnt
RUN cd /mnt/ &&  tar -xvf 2.0.0.2.tar.gz
RUN  ls -t --full /mnt/

RUN cd  /mnt/kafka-manager-2.0.0.2/ && ./sbt clean dist

CMD ["sleep", "36000"]

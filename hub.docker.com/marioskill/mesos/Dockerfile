				#############################################################
				# Archivo Dockerfile para ejecutar apache MESOS             #
				# Basado en una imagen de Ubuntu                            #
				#############################################################

# Establece la imagen de base a utilizar para Ubuntu
FROM ubuntu:16.04

# Establece el autor (maintainer) del archivo (tu nombre - el autor del archivo)
MAINTAINER Mario <100292688@alumnos.uc3m.es>

RUN apt-get update && \
apt-get upgrade -y && \
apt-get install -y tar wget git curl zip && \
apt-get install -y openjdk-8-jdk && \
apt-cache search maven && \
apt-get install -y maven && \
apt-get install -y autoconf libtool && \
apt-get -y install build-essential python-dev python-six python-virtualenv libcurl4-nss-dev libsasl2-dev libsasl2-modules maven libapr1-dev libsvn-dev zlib1g-dev iputils-ping && \
apt-get clean

# 1 Instalamos MESOS

ENV MESOS_v 1.4.1
ENV MESOS /usr/local/src/mesos/$MESOS_v/

RUN mkdir -p $MESOS
RUN wget http://www.apache.org/dist/mesos/$MESOS_v/mesos-$MESOS_v.tar.gz
RUN tar -zxf mesos-$MESOS_v.tar.gz
RUN mv mesos-$MESOS_v/* $MESOS

WORKDIR $MESOS
RUN ./bootstrap
RUN mkdir build
WORKDIR $MESOS/build
RUN ../configure 
RUN make -j 2 V=0
ENV MESOS_SYSTEMD_ENABLE_SUPPORT false
RUN make check; exit 0
RUN make install
RUN ldconfig
RUN mkdir /var/lib/mesos
RUN mkdir /etc/mesos/
RUN mkdir /etc/mesos-master/
RUN mkdir /etc/mesos-slave/
WORKDIR /


RUN rm mesos-$MESOS_v.tar.gz

EXPOSE 5050

RUN apt-get update

RUN apt-get install -y \
    apt-transport-https \
    ca-certificates \
    software-properties-common
RUN curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add -
RUN apt-key fingerprint 0EBFCD88
RUN add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
RUN apt-get update
RUN apt-get install -y docker-ce

ENTRYPOINT ["/usr/local/src/mesos/1.4.1/build/bin/mesos-master.sh"]
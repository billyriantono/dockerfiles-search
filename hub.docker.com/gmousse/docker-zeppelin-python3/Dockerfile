FROM maven:3.3.3-jdk-7

MAINTAINER Guillaume Mousnier <mousnier.guillaume@gmail.com>

RUN  \
  export DEBIAN_FRONTEND=noninteractive && \
  sed -i 's/# \(.*multiverse$\)/\1/g' /etc/apt/sources.list && \
  apt-get update && \
  apt-get -y upgrade && \
  apt-get install -y git npm python3 python3-pip python3-numpy python3-pandas python3-scipy

RUN git clone https://github.com/apache/incubator-zeppelin.git /zeppelin

WORKDIR /zeppelin

RUN mvn clean package -Pspark-1.6 -Ppyspark -Dhadoop.version=2.6.0 -Phadoop-2.6 -DskipTests

COPY interpreter.json conf/

COPY zeppelin-env.sh conf/

COPY requirements.pip ./

RUN pip3 install --upgrade pip

RUN pip3 install -r requirements.pip

EXPOSE 8080

CMD ["bin/zeppelin.sh", "start"]

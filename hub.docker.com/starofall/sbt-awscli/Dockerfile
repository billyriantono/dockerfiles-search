FROM openjdk:8
RUN apt-get update
RUN DEBIAN_FRONTEND=noninteractive apt-get install -qy python-pip apt-transport-https
RUN pip install awscli
RUN echo "deb https://dl.bintray.com/sbt/debian /" | tee -a /etc/apt/sources.list.d/sbt.list
RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 2EE0EA64E40A89B84B2DF73499E82A75642AC823
RUN apt-get update
RUN apt-get install -qy sbt
COPY . /tmp/
RUN (cd /tmp/; sbt exit;)

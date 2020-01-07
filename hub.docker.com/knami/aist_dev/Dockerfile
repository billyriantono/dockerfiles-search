#sudo docker build --network=host -t aist_dev .
#sudo docker run --network=host -it aist_dev /bin/bash
#if you need to connect network, you add option(--network=host)
#https://forums.docker.com/t/docker-dns-broken/61622

#If you want to move docker directory, there is reference.
# http://kazuhito-m.github.io/tech/2016/12/01/move-docker

FROM openjdk:8-jre AS java

FROM continuumio/miniconda3

#javaをひっぱってくる
COPY --from=java /usr/local/openjdk-8 /usr/local/openjdk-8
ENV JAVA_HOME /usr/local/openjdk-8
ENV PATH $PATH:$JAVA_HOME:$JAVA_HOME/bin

WORKDIR /root
COPY requirements.txt ./
COPY ./lib/SocialForceBaseMultiagentSimulater-0.jar /usr/local/openjdk-8/lib/ext/
COPY ./DockerRoot/ ./
COPY . ./src
RUN pip install --no-cache-dir -r requirements.txt
ENV PYTHONPATH $PYTHONPATH:/root/src

#CMD [ "python", "./hello_docker.py" ]


FROM debian:latest

RUN apt-get update
RUN apt-get upgrade -y
RUN apt-get install python3 -y
RUN apt-get install python3-pip -y
RUN apt-get install python3-dev -y
RUN apt-get install default-libmysqlclient-dev -y
RUN apt-get install curl -y
RUN python3 --version
RUN pip3 --version
RUN pip3 install apache-airflow[all]
RUN airflow version
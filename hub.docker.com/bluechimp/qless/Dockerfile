
FROM ubuntu:14.04

RUN sudo apt-get update

RUN sudo apt-get install -y build-essential ruby1.9.3
RUN sudo gem1.9.1 install qless thin --no-ri --no-rdoc

EXPOSE 5678:5678

ADD run.sh /run.sh
CMD sudo sh /run.sh
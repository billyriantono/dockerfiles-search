FROM ubuntu:12.04
MAINTAINER 	Kai Davenport <kaiyadavenport@gmail.com>

RUN apt-get update -q

RUN apt-get install -y rlwrap wget git curl software-properties-common python python-software-properties g++ make
RUN wget -qO /usr/local/bin/nave https://raw.github.com/isaacs/nave/master/nave.sh
RUN chmod a+x /usr/local/bin/nave
RUN nave usemain 0.10.29 || nave usemain 0.10.29

ENTRYPOINT ["/usr/local/bin/node"]
CMD [""]
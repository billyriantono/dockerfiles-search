FROM mechatoni/trusty-java7
MAINTAINER Ikuo Matsumura <makiczar@gmail.com>

WORKDIR /opt/
RUN apt-get update && apt-get -y upgrade
RUN apt-get install -y git vim maven
RUN git clone https://github.com/Graphity/graphity-server.git
RUN cd graphity-server && mvn install

WORKDIR /

CMD ["/bin/bash"]

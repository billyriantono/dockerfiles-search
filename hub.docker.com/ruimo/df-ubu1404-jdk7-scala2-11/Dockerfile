FROM ruimo/df-ubu1404-jdk7
MAINTAINER Shisei Hanai<ruimo.uno@gmail.com>

RUN apt-get install -y wget httpie
RUN cd /tmp && wget http://downloads.typesafe.com/scala/2.11.2/scala-2.11.2.tgz
RUN cd /tmp && tar xf scala-2.11.2.tgz
RUN mv /tmp/scala-2.11.2 /opt/
RUN rm /opt/scala-2.11.2/bin/*.bat
RUN cd /opt/scala-2.11.2/bin && for i in *; do ln -s /opt/scala-2.11.2/bin/$i /usr/local/bin/$i; done

CMD ["/bin/bash"]

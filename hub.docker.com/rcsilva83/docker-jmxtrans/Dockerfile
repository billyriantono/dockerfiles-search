FROM java:8u72-jdk

MAINTAINER fvigotti

RUN echo "debconf debconf/frontend select noninteractive" | debconf-set-selections
RUN wget http://central.maven.org/maven2/org/jmxtrans/jmxtrans/254/jmxtrans-254.deb
RUN dpkg -i jmxtrans-254.deb


ADD run-jmxtrans.sh /usr/bin/run-jmxtrans.sh
RUN chmod +x /usr/bin/run-jmxtrans.sh

# default json confs dir
VOLUME ["/var/lib/jmxtrans"]

# default logs dir
VOLUME ["/var/log/jmxtrans"]

CMD /usr/bin/run-jmxtrans.sh


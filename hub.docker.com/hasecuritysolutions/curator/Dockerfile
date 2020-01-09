FROM ubuntu:18.04

RUN apt-get update && apt-get upgrade -y \
    && apt-get -y install python-pip python2.7 python2.7-dev
RUN pip install elasticsearch-curator \
    && pip install -U elasticsearch-curator
RUN useradd -ms /bin/bash curator
USER elastalert
STOPSIGNAL SIGTERM

CMD /usr/local/bin/curator

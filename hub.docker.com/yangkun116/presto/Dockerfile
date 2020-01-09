FROM kongtrio/kongtrio_centos

LABEL maintainer="yangkun116/presto"

COPY opt.sh /

RUN sh ./opt.sh 

COPY /etc /presto/etc

CMD /bin/bash




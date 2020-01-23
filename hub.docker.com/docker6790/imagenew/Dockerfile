FROM ubuntu
ENV ORA_CLOUD_CLUSTER="ASHB"▒▒
ARG LICENSE_KEY="123-0001-223"
LABEL MAINTAINER vicky.kumar.gupta@oracle.com
COPY sample.sh /code/sample.sh
COPY testfile /code/testfile
RUN chmod +x /code/sample.sh
RUN echo "LICENSE KEY is " $LICENSE_KEY
WORKDIR /code
CMD sh sample.sh testfile

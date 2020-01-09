FROM ubuntu
LABEL MAINTAINER pk
#RUN mkdir /code
ENV ORA_CLOUD_CLUSTER="ASHBURN"
ARG LICENSE_KEY="123-456"
COPY sample.sh /code/sample.sh
COPY testfile /code/testfile
RUN chmod +x /code/sample.sh
RUN echo "License key is "$LICENSE_KEY
WORKDIR /code
#ENTRYPOINT ["sh", "sample.sh"]
CMD sh sample.sh testfile

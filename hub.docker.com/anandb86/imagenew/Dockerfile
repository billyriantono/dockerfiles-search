FROM ubuntu
ENV ORAC_CLOUD_CLUSTER="ASHBURN"
ARG LICENSE_KEY="123-0001-223"
LABEL MAINTAINER anandb86@gmail.com
COPY sample.sh /code/sample.sh
COPY testfile /code/testfile
RUN chmod +x /code/sample.sh
RUN echo "LICENSE KEY IS "$LICENSE_KEY
WORKDIR /code
#ENTRYPOINT ["sh","sample.sh"]
CMD sh sample.sh testfile

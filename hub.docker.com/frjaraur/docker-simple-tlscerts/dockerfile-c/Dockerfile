FROM ubuntu
LABEL MAINTAINER test@test.com
RUN mkdir /code
COPY sample.sh /code/sample.sh
RUN chmod +x /code/sample.sh
RUN cd /code
CMD sh /code/sample.sh

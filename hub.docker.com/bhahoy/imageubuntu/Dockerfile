FROM ubuntu:latest
LABEL MAINTAINER bharath.govindappa@oracle.com
ARG image_variable="local"
ENV ora_port=1521
ENV ora_host=localhost
RUN mkdir /code
COPY sample.sh /code/sample.sh
RUN chmod +x /code/sample.sh
RUN echo "Building an Image BHA"
RUN echo $image_variable
WORKDIR /code
CMD sh /code/sample.sh

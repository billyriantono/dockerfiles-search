ARG VERSION="18.04"
FROM ubuntu:$VERSION
RUN echo "version.." $VERSIION
#First Dockerfile...
LABEL MAINTAINER deep@apps.com
ARG LICENSEKEY="124143"
RUN mkdir /code
COPY sample.sh /code/sample.sh
COPY testfile /code/testfile
RUN chmod +x /code/sample.sh
RUN echo "Image is built at 'date'"
RUN echo "License key is " $LICENSEKEY
#ENTRYPOINT ["sh", "/code/sample.sh"]
#CMD ["/code/testfile"]
CMD echo "Container being built"
CMD env

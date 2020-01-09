ARG version="18.04"
FROM ubuntu:$version
RUN echo "version ..."$version
ARG licenseKey="100...200"
#First Dockerfile ...
LABEL MAINTAINER lakshay@apps.com
RUN mkdir /code
# code holder during image build
COPY sample.sh /code/sample.sh
COPY testfile /code/testfile
RUN chmod +x /code/sample.sh
RUN echo "image is built at `date`"
RUN echo "license key is .."$licenseKey
#ENTRYPOINT ["sh","/code/sample.sh"]
#CMD ["/code/testfile"]
# absolute path for bootstrapper
CMD echo "container being built"
CMD env

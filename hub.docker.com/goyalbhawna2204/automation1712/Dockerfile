ARG version="18.04"

#FROM ubuntu

FROM ubuntu:$version

RUN echo "version ..."$version

# First Dockerfile .. If image is not there it will pull.

ARG LICENSEKEY="100..2000"

LABEL MAINTAINER goyalbhawna22@gmail.com

# Metadata

RUN mkdir /code
#Create the directory to push the code files. This command will be executed only when images will

COPY Sample.sh /code/Sample.sh

COPY testfile /code/testfile
RUN chmod +x /code/Sample.sh
#Giving executable only permissions to the Sample file.

RUN echo "Image is build at `date`"

RUN echo "license key is "$LICENSEKEY

ENTRYPOINT ["sh","/code/Sample.sh"]

#CMD sh /code/Sample.sh /code/testfile

#CMD ["/code/testfile"]

#testfile is input to Sample.sh file.

CMD echo "Container being build"
CMD env

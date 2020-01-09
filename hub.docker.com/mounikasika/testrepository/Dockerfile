FROM ubuntu:16.04
LABEL MAINTAINER Mounika<mounika.sika@oracle.com>
RUN mkdir /code
RUN echo "Image us built..."
COPY Sample.sh /code/Sample.sh
RUN chmod +x /code/Sample.sh
ENTRYPOINT ["sh","/code/Sample.sh"]
CMD ["/etc/hosts"]

FROM ubuntu:16.04
LABEL MAINTAINER udayan.das11@gmail.com
RUN mkdir /code
RUN echo "code directory created"
COPY sample.sh /code/sample.sh
RUN chmod +x /code/sample.sh
ENTRYPOINT ["sh", "/code/sample.sh"]
CMD ["/etc/hosts"]

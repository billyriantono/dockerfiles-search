FROM ubuntu
ENV ORA_CLOUD_CLUSTER="ASHBURN"
ARG LICENSE_KEY="123-0001-223"
LABEL MAINTAINER deepa.l@oracle.com
COPY Sample.sh /codeDee/Sample.sh
COPY testFileDee /codeDee/testFileDee
RUN chmod +x /codeDee/Sample.sh
RUN echo "LICENSE KEY is "$LICENSE_KEY
WORKDIR /codeDee
#CMD sh Sample.sh testFileDee
#ENTRYPOINT ["sh","Sample.sh"]
#CMD ["testFileDee"]
CMD sh Sample.sh testFileDee

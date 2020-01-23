FROM ubuntu
ENV ORA_CLOUD_CLUSTER="ASHBURN"
ARG LICENSE_KEY="123-0001-223"

LABEL MAINTAINER jk@devops.com
COPY Sample.sh /code/Sample.sh
COPY testfile /code/testfile
RUN  chmod +x /code/Sample.sh
RUN echo "LICENAC KEY IS" $LICENSE_KEY
WORKDIR /code
#CMD sh Sample.sh testfile
#To take file as input from cmd
#ENTRYPOINT ["sh","Sample.sh"]
#CMD ["testfile"]
CMD sh Sample.sh testfile

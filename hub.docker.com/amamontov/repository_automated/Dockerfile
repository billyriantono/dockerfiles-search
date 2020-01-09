FROM ubuntu
ARG MESSAGE_ARG='Building message'
ENV message=$MESSAGE_ARG
RUN echo $message
#RUN mkdir /tomcat
#add 'http://www-eu.apache.org/dist/tomcat/tomcat-8/v8.5.16/bin/apache-tomcat-8.5.16.zip' .
#RUN cp apache-tomcat-8.5.16.zip /tomcat
#RUN usr/bin/apt-get update
#RUN usr/bin/apt-get install mc
#RUN unzip /tomcat/apache-tomcat-8.5.16.zip
#RUN rm /tomcat/apache-tomcat-8.5.16.zip
LABEL Author="Alexey Mamontov" Company="Slice"
RUN echo 'Building image ...'
COPY docs/ /docs/
WORKDIR /docs
RUN cat instructions.txt
ENTRYPOINT "/usr/bin/mc"
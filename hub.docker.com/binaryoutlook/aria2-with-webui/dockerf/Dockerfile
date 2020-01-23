FROM java:8-jdk

MAINTAINER Bill Lee, bill@pacificanalytics.com.au

RUN apt-get update && apt-get install unzip

RUN wget http://www.usadellab.org/cms/uploads/supplementary/Trimmomatic/Trimmomatic-0.36.zip -P /opt
RUN unzip /opt/Trimmomatic-0.36.zip -d /opt
RUN mv /opt/Trimmomatic-0.36 /opt/trimmomatic
COPY trimmomatic /opt/trimmomatic

RUN chmod +x /opt/trimmomatic/trimmomatic

ENV PATH="/opt/trimmomatic:${PATH}"

RUN mkdir -p /data
WORKDIR /data

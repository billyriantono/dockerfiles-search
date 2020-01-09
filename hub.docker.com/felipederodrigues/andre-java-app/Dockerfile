FROM ubuntu

RUN apt-get update
RUN apt-get install default-jre default-jdk maven -y

ADD compile.sh ./ 
RUN chmod 755 compile.sh
CMD ["./compile.sh"]

EXPOSE 81

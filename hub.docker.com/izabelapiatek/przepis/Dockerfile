FROM ubuntu:latest AS web100
MAINTAINER izabela.piatek@pollub.edu.pl
RUN ["bin/bash","-c","apt-get update","apt-get install apache2","-y"]
CMD ["bin/bash","-c","systemctl start apache2"]
EXPOSE 8080

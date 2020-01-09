FROM ubuntu
MAINTAINER Mark Fernandes <mark.fernandes@ifr.ac.uk>

# simple Dockerfile to practice docler build & demo automatic builds
# Execute it with 'docker run -it -v <RSE VM dir>/:/home/test/output/ <cont.name> /bin/bash'
ENV APP_USER=guest \
  APP_HOME=/home

USER root

RUN mkdir $APP_HOME/test && cd $APP_HOME/test
WORKDIR $APP_HOME/test 

ADD Welcome.txt /etc/motd
RUN mkdir output scripts
ADD simple.sh scripts/simple.sh
ADD *.txt $APP_HOME/

RUN chmod +x scripts/simple.sh 

EXPOSE 22

VOLUME $APP_HOME/test/output

ENTRYPOINT ["scripts/simple.sh"]
CMD ["/bin/bash"]

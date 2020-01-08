FROM ubuntu:14.04
RUN apt-get update -y
RUN apt-get install -y git-core
ADD ./post-receive /var/repos/post-receive
RUN chmod +x /var/repos/post-receive
ADD ./start /start
RUN chmod +x /start
CMD /start

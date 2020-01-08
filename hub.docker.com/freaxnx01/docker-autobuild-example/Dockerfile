FROM ubuntu
RUN apt-get update
RUN apt-get -y upgrade
RUN apt-get install -y screenfetch
RUN apt-get install -y youtube-dl
ENTRYPOINT ["/usr/bin/youtube-dl", "--version"]

#orig ENTRYPOINT ["/usr/bin/screenfetch"]
#ENTRYPOINT ["/usr/bin/screenfetch", "--version"]
#ENTRYPOINT ["/usr/bin/youtube-dl --version"]
#ENTRYPOINT ["which youtube-dl"]

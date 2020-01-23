FROM docker/whalesay:latest
RUN apt-get -y update && apt-get install -y fortunes
# Port
EXPOSE 80
CMD /usr/games/fortune -a | cowsay
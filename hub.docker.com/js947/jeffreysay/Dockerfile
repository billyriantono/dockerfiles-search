FROM ubuntu:14.04
RUN apt-get update && apt-get install -y cowsay --no-install-recommends
RUN cp /usr/games/cowsay /usr/local/bin/jeffreysay
CMD ["jeffreysay"]

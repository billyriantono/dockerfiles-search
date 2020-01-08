#test
From debian:stable-slim
RUN dpkg --add-architecture i386 && apt-get update && apt-get -y   install lib32z1 lib32ncurses5 libbz2-1.0:i386 lib32gcc1 lib32stdc++6 ca-certificates gdb  &&  rm -rf /var/cache/apk/* && useradd -m -d /home/container container
USER container
ENV  USER container
ENV  HOME /home/container
WORKDIR /home/container

CMD ["/bin/bash"]

FROM linuxconfig/lemp
MAINTAINER Nick Cousins <me@nickcousins.co.uk>
EXPOSE 80

RUN curl -sL https://deb.nodesource.com/setup_8.x | bash -
RUN apt-get update && apt-get install -qy git curl libmcrypt-dev mysql-client zip unzip nodejs php-mailparse ffmpeg

CMD /bin/bash

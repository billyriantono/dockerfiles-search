FROM webdevops/php-apache-dev

MAINTAINER mail@nasourso.com

ENTRYPOINT []

RUN mkdir /api

WORKDIR /api

ADD run.sh /api

RUN chmod +x run.sh

RUN apt-get update && apt-get install git -y && apt-get clean

RUN git clone https://github.com/Seems2Legit/Rainbow-Six-Siege-Player-Stats-API /app

RUN rm /app/config.php

CMD ["./run.sh"]

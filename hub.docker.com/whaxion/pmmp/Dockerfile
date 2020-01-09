FROM php:7

RUN useradd pmmp
RUN mkdir /home/pmmp/
RUN chown -R pmmp /home/pmmp/

RUN apt-get update && apt-get install -y wget

USER pmmp
WORKDIR /home/pmmp/

RUN wget -q -O - https://get.pmmp.io | bash -s -

EXPOSE 19132

ENTRYPOINT bash /home/pmmp/start.sh --no-wizard

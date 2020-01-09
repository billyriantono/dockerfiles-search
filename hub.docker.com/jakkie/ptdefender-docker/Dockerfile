FROM accetto/ubuntu-vnc-xfce

RUN apt-get update && apt-get install -y curl gdebi-core

ARG PTD_VERSION=1.11.3
ENV PTD_VERSION ${PTD_VERSION}

RUN curl -SL https://dl.ptdefender.com/${PTD_VERSION}/PTDefender_${PTD_VERSION}_amd64.deb -o ptdefender.deb

RUN gdebi -n ptdefender.deb \
      && apt-get -f install \
      && dpkg -i ptdefender.deb \
      && rm ptdefender.deb \
      && apt-get -y autoremove

RUN mkdir -p /home/headless/ProfitTrailer && mkdir -p /home/headless/Desktop
RUN ln -sf /opt/PTDefender/ptdefender /home/headless/Desktop/ptdefender

VOLUME ["/home/headless/ProfitTrailer"]

EXPOSE 6901 5901
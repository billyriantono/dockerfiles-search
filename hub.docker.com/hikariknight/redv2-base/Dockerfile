FROM ubuntu:18.04

RUN apt-get update && apt-get install -y \
apt-transport-https \
wget \
curl \
bash-completion \
multiarch-support \
xdg-utils \
nano \
htop \
screen \
python3 \
python3-pip \
python3-wheel \
git \
ffmpeg \
psmisc

RUN pip3 install tweepy markovify

RUN echo \#\!/bin/bash > /usr/local/bin/bot.start && \
echo screen -dmS bot /data/start_red_autorestart.sh >> /usr/local/bin/bot.start && \
chmod +x /usr/local/bin/bot.start

RUN echo \#\!/bin/bash > /usr/local/bin/bot.stop && \
echo killall screen >> /usr/local/bin/bot.stop && \
chmod +x /usr/local/bin/bot.stop

RUN echo \#\!/bin/bash > /usr/local/bin/bot.view && \
echo screen -dr bot >> /usr/local/bin/bot.view && \
chmod +x /usr/local/bin/bot.view

CMD ["/bin/bash"]
FROM haugene/transmission-openvpn

LABEL com.rivierakid.version="0.1.1"

RUN apt-get update && apt-get install -y git cpanminus build-essential libexpat1-dev

RUN apt-get update && apt-get install -y aptitude

RUN cpanm File/Copy/Recursive.pm
RUN cpanm LWP/Simple.pm
RUN cpanm XML/Simple.pm
RUN cpanm TVDB/API.pm
RUN cpanm WWW/TheMovieDB.pm
RUN cpanm JSON/Parse.pm

COPY SortTV1.37.zip /usr/local/src

RUN cd /usr/local/src && unzip SortTV1.37.zip

RUN chmod +x /usr/local/src/sorttv/sorttv.pl

RUN apt-get update && apt-get install -y samba net-tools avahi-daemon

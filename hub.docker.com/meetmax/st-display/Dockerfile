ARG CPANFILE=./docker/st-perl/cpanfile
FROM meetmax/pinto:resin

RUN rm -Rf /home/twst/tools/repo

COPY docker/st-perl/SysInfo.pm /usr/local/lib/site_perl/Forks/Super/

WORKDIR /home/twst/CheckIn/lib
COPY  lib /home/twst/CheckIn/lib

# put script in place
WORKDIR /home/twst/CheckIn/script
COPY script/meeting_scantracker.pl /home/twst/CheckIn/script

WORKDIR /home/twst/log

RUN touch /home/twst/log/error.log

COPY twst_checkin.yml /home/twst/CheckIn/twst_checkin.yml
COPY l4p.conf /home/twst/CheckIn/l4p.conf

CMD ["perl", "/home/twst/CheckIn/script/meeting_scantracker.pl", "-f", "start"]

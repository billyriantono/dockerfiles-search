FROM centos:latest

MAINTAINER Justin Henderson justin@hasecuritysolutions.com

RUN useradd -ms /bin/bash bladerunner
USER bladerunner

STOPSIGNAL SIGTERM

CMD bash -c "while true; do SECRET=CongratulationsYouAreHuman; sleep 1; done"

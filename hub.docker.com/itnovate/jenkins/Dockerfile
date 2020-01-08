FROM jenkins

USER root
RUN apt-get update
RUN apt-get -qqy install ruby nodejs locales vim sudo

RUN echo "en_US.UTF-8 UTF-8" >> /etc/locale.gen
RUN locale-gen
ENV LANG en_US.UTF-8
ENV LC_ALL en_US.UTF-8


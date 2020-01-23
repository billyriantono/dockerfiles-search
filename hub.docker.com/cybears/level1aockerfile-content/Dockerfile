FROM maven:3-jdk-8

# install locales, dos2unix
RUN apt-get clean
RUN apt-get update
RUN apt-get install -y locales
RUN apt-get install -y dos2unix
RUN apt-get clean

# set cs_CZ locale to generate
RUN sed -i '/^# cs_CZ.UTF.* /s/^#//g' /etc/locale.gen

# generate locale
RUN locale-gen cs_CZ.UTF-8

# set environment variables to new locale
ENV LANG "cs_CZ.UTF-8"
ENV LANGUAGE "cs_CZ.UTF-8"
ENV LC_ALL "cs_CZ.UTF-8"

# update locales
RUN update-locale LANG=cs_CZ.utf8
RUN update-locale LC_ALL=cs_CZ.utf8
RUN update-locale LANGUAGE=cs_CZ.utf8

# activate locale
RUN . /etc/default/locale

# set czech timezone
ENV TZ "Europe/Prague"
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# activate ssh-agent
RUN eval `ssh-agent -s`
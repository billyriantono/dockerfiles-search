# Debian
FROM debian:jessie
MAINTAINER JimyRyan

#################################################################################
#################################################################################
#                                                                               #
#             [START :: TIMEZONE, LOCALE, CA CERT & UPDATE / UPGRADE]           #
#                                                                               #
#################################################################################

RUN apt-get update -y \
    && apt-get install -y locales ca-certificates

# Set locale and timezone 
ENV LANGUAGE fr_FR.UTF-8
ENV LANG fr_FR.UTF-8
ENV LC_ALL fr_FR.UTF-8
ENV TZ Europe/Paris

# Change locale and timezone 
RUN set -x \
    && sed -i -e 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/' /etc/locale.gen \
    && sed -i -e 's/# '$LANG' UTF-8/'$LANG' UTF-8/' /etc/locale.gen \
    && locale-gen \
    && update-locale LANG=$LANG \
    && ln -snf /usr/share/zoneinfo/$TZ /etc/localtime \
    && echo $TZ > /etc/timezone

# Update distribution
RUN apt-get update \
    && apt-get upgrade -y

#################################################################################
#                                                                               #
#             [START :: TIMEZONE, LOCALE, CA CERT & UPDATE / UPGRADE]           #
#                                                                               #
#################################################################################
#################################################################################

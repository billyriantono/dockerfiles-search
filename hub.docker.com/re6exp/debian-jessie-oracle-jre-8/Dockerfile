# Oracle JRE 8 for Debian Jessie
#
# URL: https://github.com/re6exp/debian-jessie-oracle-jre-8
#
# Reference:  http://www.duinsoft.nl/packages.php?t=en
#
# Version     0.1
#

FROM re6exp/debian-jessie:latest


RUN \
    echo " Add Oracle JRE 8 repository:"  && \
    echo "deb http://www.duinsoft.nl/pkg debs all" | tee /etc/apt/sources.list.d/duinsoft-jre.list  && \
    apt-key adv --keyserver keys.gnupg.net --recv-keys 5CB26B26  && \
    apt-get update && apt-get upgrade -y


RUN echo " Install Oracle JRE:"  && \
    DEBIAN_FRONTEND=noninteractive  apt-get -o Dpkg::Options::='--force-confnew' -y install update-sun-jre


RUN echo " Clean up:"  && \
    rm -rf /var/cache/update-sun-jre  && \
    apt-get clean  && \
    rm -rf /var/lib/apt/lists/*


# define default command
CMD ["java"]

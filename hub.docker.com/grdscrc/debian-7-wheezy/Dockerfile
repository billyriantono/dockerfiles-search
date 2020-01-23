FROM debian:wheezy

RUN ( \
    echo "deb http://archive.debian.org/debian/ wheezy main contrib non-free" && \
    echo "deb-src http://archive.debian.org/debian/ wheezy main contrib non-free" && \
    echo "deb http://archive.debian.org/debian/ wheezy-backports main contrib non-free" \
    ) > /etc/apt/sources.list

RUN apt-get update && apt-get upgrade -y

# perl-modules dependency
RUN apt-get --yes --force-yes install \
      perl-base=5.14.2-21+deb7u3 \
      tzdata=2016d-0+deb7u1

# libmysql-dev dependency
RUN apt-get --yes --force-yes install \
      libc-bin=2.13-38+deb7u10 \
      libc6=2.13-38+deb7u10

RUN apt-get clean

FROM ubuntu:18.04
RUN apt update
RUN DEBIAN_FRONTEND=noninteractive apt install -y git build-essential libssl-dev libreadline-dev \
                                                  zlib1g-dev libbz2-dev libsqlite3-dev ca-certificates \
                                                  curl wget libtool-bin tzdata file 
                                                  
# I'd like to avoid this but for now... ‾\_('')_/‾
RUN DEBIAN_FRONTEND=noninteractive apt install -y software-properties-common libpq-dev libmysqlclient-dev \
                                                  imagemagick libxml2-dev libxslt-dev libtool-bin libyaml-dev \
                                                  libreadline-dev autoconf pkg-config gettext libglib2.0-dev \
                                                  libyaml-0-2

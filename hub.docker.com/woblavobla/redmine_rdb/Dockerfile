FROM woblavobla/ruby-jemalloc:latest

ENV APP_HOME=/home/redmine_rdb \
    TINI_VERSION=v0.18.0 \
    RAILS_ENV=production \
    RACK_ENV=production

RUN apt-get update && apt-get install -y --no-install-recommends \
        tzdata \
        ca-certificates \
        wget \
        bash \
        bzr \
        git \
        subversion \
        imagemagick \
        openssh-client \
        freetds-dev \
        gcc \
        libmagickcore-dev \
        libmagickwand-dev \
        libpq-dev \
        libsqlite3-dev \
        make \
        patch \
        ntp \
        libsasl2-2 \
        sasl2-bin \
        libsasl2-modules \
        cron \
        libtommath-dev \
        libicu-dev \
        && ln -sf /usr/lib/x86_64-linux-gnu/libtommath.so.1.0.0 /usr/lib/x86_64-linux-gnu/libtommath.so.0 && \
        mkdir /root/fb && cd /root/fb && wget https://sourceforge.net/projects/firebird/files/firebird-linux-amd64/3.0-Release/Firebird-3.0.0.32483-0.amd64.tar.gz/download && \
        tar xzvpf download && cd Firebird* && ./install.sh -silent && \
        echo "DatabaseAccess = Full" >>/opt/firebird/firebird.conf && \
        echo "ServerMode = SuperClassic" >>/opt/firebird/firebird.conf && \
        echo "WireCrypt = Enabled" >>/opt/firebird/firebird.conf && \
        echo "AuthServer = Legacy_Auth, Srp, Win_Sspi " >>/opt/firebird/firebird.conf && \
        echo "UserManager = Legacy_UserManager, Srp" >>/opt/firebird/firebird.conf && \
        rm -rf /root/fb && \
        cd /home && \
        git clone https://github.com/woblavobla/redmine_rdb.git && \
        apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN set -eux; \
    cd $APP_HOME; \
    bundle install; \
    wget https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini -O /tini; \
    chmod +rwx /tini; \
    mkdir /home/tracker_files

ENTRYPOINT ["/tini", "--"]
EXPOSE 3000
WORKDIR $APP_HOME

VOLUME ["/home/tracker_files"]

CMD puma -C config/puma.rb
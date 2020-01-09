FROM sikmi/awseb-deployer-docker:v20180222

# ruby install
RUN curl -O http://ftp.ruby-lang.org/pub/ruby/2.6/ruby-2.6.2.tar.gz && \
        tar -zxvf ruby-2.6.2.tar.gz && \
        cd ruby-2.6.2 && \
        ./configure --disable-install-doc && \
        make && \
        make install && \
        cd .. && \
        rm -r ruby-2.6.2 ruby-2.6.2.tar.gz

RUN gem install bundler

# ECS CLI install
RUN curl -o /usr/local/bin/ecs-cli https://s3.amazonaws.com/amazon-ecs-cli/ecs-cli-linux-amd64-latest
RUN chmod 755 /usr/local/bin/ecs-cli

# node install
RUN printf "deb http://archive.debian.org/debian/ jessie main\ndeb-src http://archive.debian.org/debian/ jessie main\ndeb http://security.debian.org jessie/updates main\ndeb-src http://security.debian.org jessie/updates main" > /etc/apt/sources.list
RUN set -ex \
    && apt-get update \
    && apt-get install -y \
               curl \
               netcat \
               apt-transport-https \
               --no-install-recommends \
    \
    && curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - \
    && echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list \
    && curl -sL https://deb.nodesource.com/setup_10.x | bash - \
    && DEBIAN_FRONTEND=noninteractive apt-get -y install \
         yarn \
    && apt-get clean \
    && rm -rf /var/cache/apt/archives/* /var/lib/apt/lists/*

RUN gem uninstall -ax bundler && gem install -v 1.17.2 bundler

FROM appium/appium
MAINTAINER riet
RUN mv /etc/apt/sources.list /etc/apt/sources.list.bak
ADD sources.list /etc/apt/sources.list
RUN apt-get update && \
    apt-get install -y build-essential  m4 ruby ruby-dev rubygems texinfo libbz2-dev \
                    libcurl4-openssl-dev libexpat-dev libncurses-dev zlib1g-dev \
                    net-tools
RUN rm -f /bin/sh && \
    ln -s /bin/bash /bin/sh && \
    mkdir -p /root/Documents/AutoMobile/cucumber-appium
ADD Gemfile Gemfile.lock /root/Documents/AutoMobile/cucumber-appium/
WORKDIR /root/Documents/AutoMobile/cucumber-appium
RUN gem install -V bundler && \
    bundle install --path /root/.bundle
EXPOSE 4723
RUN ln -s /root/.bundle/ruby/2.3.0/bin/cucumber /usr/local/bin/cucumber
RUN apt-get clean
RUN cp /usr/share/zoneinfo/Asia/Shanghai  /etc/localtime
ADD 51-android.rules /etc/udev/rules.d/51-android.rules
CMD appium

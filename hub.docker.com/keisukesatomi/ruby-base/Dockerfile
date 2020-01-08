FROM keisukesatomi/ubuntu-base:18.04

LABEL maintainer="satomi@fignny.co.jp"

WORKDIR /root

RUN apt update \
&& apt install -y zlib1g-dev build-essential libssl-dev libreadline-dev libyaml-dev

RUN git clone https://github.com/rbenv/rbenv.git ~/.rbenv
RUN git clone https://github.com/rbenv/ruby-build.git ~/.rbenv/plugins/ruby-build

RUN echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bashrc \
&& echo 'eval "$(rbenv init -)"' >> ~/.bashrc \
&& . ~/.bashrc \
&& rbenv install 2.5.1 \
&& rbenv global 2.5.1

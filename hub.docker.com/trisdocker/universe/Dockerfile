FROM swift:5.0-bionic

# Requirements

RUN apt-get update \
 && apt-get install -y wget curl apt-transport-https software-properties-common

# Tarantool

RUN curl http://download.tarantool.org/tarantool/1.10/gpgkey | apt-key add - \
 && echo "deb http://download.tarantool.org/tarantool/1.10/ubuntu/ bionic main" >> /etc/apt/sources.list.d/tarantool_1_10.list \
 && echo "deb-src http://download.tarantool.org/tarantool/1.10/ubuntu/ bionic main" >> /etc/apt/sources.list.d/tarantool_1_10.list

RUN apt-get update \
 && apt-get install -y tarantool tarantool-dev

# Other

## wrk
RUN apt-get update \
 && apt-get install build-essential libssl-dev git -y \
 && git clone https://github.com/wg/wrk.git wrk \
 && cd wrk && make \
 && cp wrk /usr/local/bin \
 && cd .. && rm -rf wrk

## tools
RUN apt-get update \
 && apt-get install -y vim zsh \
 && rm -rf /var/lib/apt/lists/*

## instal oh my zsh
RUN bash -c "$(wget https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)" \
 && sed -i -- 's/robbyrussell/simple/g' /root/.zshrc \
 && sed -i -- 's/  git/  git swiftpm/g' /root/.zshrc

ENTRYPOINT zsh

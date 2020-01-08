FROM bitriseio/docker-bitrise-base:latest
LABEL maintainer="Shawn Turner"

WORKDIR /build

# Install crap
RUN apt-get update && apt-get install -y curl locales aptitude ca-certificates python python-dev \
    python-pip python-virtualenv python-setuptools git automake autoconf libreadline-dev libncurses-dev \
    libssl-dev libyaml-dev libxslt-dev libffi-dev libtool unixodbc-dev unzip vim && \
    rm -rf /var/lib/apt/lists/*

RUN curl -sL https://deb.nodesource.com/setup_6.x | bash -

RUN apt-get update && apt-get install -y nodejs

# set locale
RUN locale-gen en_US.UTF-8
ENV LANG=en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

# Install asdf
RUN git clone https://github.com/asdf-vm/asdf.git ~/.asdf --branch v0.4.1

# Install erlang
RUN $HOME/.asdf/bin/asdf plugin-add erlang https://github.com/asdf-vm/asdf-erlang.git && \
    $HOME/.asdf/bin/asdf install erlang 20.2 && \
    $HOME/.asdf/bin/asdf global erlang 20.2 && \
    rm -rf  /tmp/*

# Install elixir
RUN $HOME/.asdf/bin/asdf plugin-add elixir https://github.com/asdf-vm/asdf-elixir.git && \
    $HOME/.asdf/bin/asdf install elixir 1.6.0 && \
    $HOME/.asdf/bin/asdf global elixir 1.6.0 && \
    rm -rf  /tmp/*

# Make erlang/elixir accessible
RUN echo '. $HOME/.asdf/asdf.sh' >> ~/.bash_profile && \
    echo '. $HOME/.asdf/completions/asdf.bash' >> ~/.bash_profile
ENV PATH=/root/.asdf/bin:/root/.asdf/shims:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

# Install hex and rebar
RUN mix local.hex --force
RUN mix local.rebar --force

# S3 CMD
RUN pip install s3cmd

# # Setup build script
# #ADD scripts/build.sh /usr/local/bin/build.sh
# #RUN chmod +x /usr/local/bin/build.sh

CMD bitrise --version

FROM centos:7

ENV LANG en_US.UTF-8

ENV ELIXIR_VERSION "1.9.1"
ENV ERLANG_VERSION "22.0"
ENV ASDF_VERSION   "v0.5.1"
ENV ASDF_DIR /opt/asdf
ENV PATH "/opt/asdf/bin:/opt/asdf/shims:$PATH"

RUN yum groupinstall -y 'Development Tools' && \
  yum install -y automake autoconf readline-devel openssl-devel ncurses-devel unixODBC-devel libyaml-devel libxslt-devel libffi-devel libtool ca-certificates git unzip which bash && \
  curl --silent --location https://rpm.nodesource.com/setup_11.x | bash - && \
  yum install -y nodejs && \
  npm install -g yarn && \
  git clone https://github.com/asdf-vm/asdf.git /opt/asdf --branch $ASDF_VERSION && \
  asdf plugin-add erlang https://github.com/asdf-vm/asdf-erlang.git && \
  asdf install erlang $ERLANG_VERSION && \
  asdf global  erlang $ERLANG_VERSION && \
  asdf plugin-add elixir https://github.com/asdf-vm/asdf-elixir.git && \
  asdf install elixir $ELIXIR_VERSION && \
  asdf global  elixir $ELIXIR_VERSION && \
  yes | mix local.hex --force && \
  yes | mix local.rebar --force
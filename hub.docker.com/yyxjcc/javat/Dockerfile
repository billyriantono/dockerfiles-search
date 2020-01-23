FROM youyo/erlang:latest
ENV LANG en_US.UTF-8
ENV LC_CTYPE en_US.UTF-8
ENV LC_ALL en_US.UTF-8
ENV ELIXIR_VERSION 1.0.5
WORKDIR /usr/local/src/
RUN wget https://github.com/elixir-lang/elixir/archive/v${ELIXIR_VERSION}.tar.gz
RUN tar xvzf v${ELIXIR_VERSION}.tar.gz
WORKDIR /usr/local/src/elixir-${ELIXIR_VERSION}
RUN make clean test
RUN make install
WORKDIR /
RUN rm -rf /usr/local/src/*
RUN iex -v

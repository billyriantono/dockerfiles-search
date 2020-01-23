FROM elixir:1.7-alpine

RUN \
    apk update && \
    apk --no-cache --update add \
        bash build-base openssh-client git ncurses nodejs procps yarn

ENV TERM=xterm

RUN locale-gen C.UTF-8 || true
ENV LANG=C.UTF-8

RUN mix local.hex --force && \
    mix local.rebar --force

CMD ["/bin/bash"]

FROM adie/debian

MAINTAINER Anton Dieterle <antondie@gmail.com>

RUN wget http://packages.erlang-solutions.com/erlang-solutions_1.0_all.deb \
    && dpkg -i erlang-solutions_1.0_all.deb  \
    && apt-get update -qq \
    && apt-get install -y erlang \
    && rm erlang-solutions_1.0_all.deb \
    && rm -rf /var/lib/apt/lists/*

CMD ["erl"]

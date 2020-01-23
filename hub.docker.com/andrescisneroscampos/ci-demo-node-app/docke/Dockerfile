FROM erlang

RUN    set -x \
    && apt-get update \
    && DEBIAN_FRONTEND=noninteractive apt-get install -y emacs-nox inotify-tools sudo \
    && rm -rf /var/lib/apt/lists \
    && adduser --disabled-password --gecos "" user \
    && echo 'user:pass' | chpasswd \
    && adduser user sudo \
    && adduser user users

USER user
WORKDIR "/project"

RUN    set -x \
    && mkdir -p ~/.config/rebar3/ \
    && echo '{plugins, [rebar3_auto, {rebar3_autotest, "0.1.1"}]}.' > ~/.config/rebar3/rebar.config

ENV ERL_FLAGS="-config app.config"

# TODO: Should I install the erlang docs as well?

CMD ["emacs"]

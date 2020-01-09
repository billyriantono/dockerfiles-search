FROM elixir:latest

ARG FWUP_VERSION=1.3.1

# Install Dependencies
RUN apt-get update -y \
    && apt-get install -y build-essential squashfs-tools \
    ssh-askpass bc m4 unzip cmake python \
    && curl -sSL https://github.com/fhunleth/fwup/releases/download/v${FWUP_VERSION}/fwup_${FWUP_VERSION}_amd64.deb > fwup.deb \
    && dpkg -i fwup.deb \
    && rm fwup.deb

# Install and update local hex repos
RUN mix local.hex --force \
    && mix local.rebar --force \
    && mix archive.install hex nerves_bootstrap --force \
    && mix archive.install hex phx_new --force

ENTRYPOINT [ "bash" ]
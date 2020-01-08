FROM jess/atom

# Declare maintainer
MAINTAINER Leif Madsen <leif@leifmadsen.com>

ENV HOME /home/developer

#Install packages
RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y \
        --allow-downgrades \
        --allow-remove-essential \
        --allow-change-held-packages \
        nodejs nodejs-legacy npm ssh pandoc && \
    rm -r /var/lib/apt/lists/* && \
    useradd --create-home --home-dir $HOME developer && \
    chown -R developer:developer $HOME && \
    apm install language-docker && \
    apm install minimap && \
    apm install atom-beautify && \
    apm install atom-ungit && \
    apm install linter && \
    apm install file-icons && \
    apm install highlight-line && \
    apm install color-picker && \
    apm install auto-indent && \
    apm install linter-docker && \
    apm install rst-preview

USER developer

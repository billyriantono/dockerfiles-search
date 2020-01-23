FROM ubuntu:18.04

RUN apt-get update -qy

# Installing emacs
RUN set -ex \
    apt-get update -qy && \
    apt-get install -yq --no-install-recommends \
    emacs-nox

# Installing latex etc
RUN set -ex \
    apt-get update -qy && \
    apt-get install -yq --no-install-recommends \
    texlive-xetex \
    texlive-generic-extra \
    texlive-science

# installing python (to use the pygments package)
RUN set -ex \
    apt-get update -qy && \
    apt-get install -yq \
    python3-pip

# installing pygments (to export beatiful code blocks)
RUN pip3 install pygments


# installing microsoft fonts
RUN set -ex \
    apt-get update -qy && \
    echo "ttf-mscorefonts-installer	msttcorefonts/accepted-mscorefonts-eula	boolean	true" | debconf-set-selections && \    
    apt-get install -qy ttf-mscorefonts-installer

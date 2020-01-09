FROM python:2.7

ARG UID=1000
ARG GID=1000
ARG USER=${USER:-user}

RUN groupadd -g $GID $USER \
    && useradd -g $USER -u $UID -m $USER

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
            jq \
            texlive-base \
            texlive-binaries \
            texlive-extra-utils \
            texlive-latex-base \
            texlive-latex-extra \
            texlive-latex-recommended \
            texlive-fonts-recommended \
    && apt-get autoremove -y \
    && apt-get clean -y \
    && rm -rf \
            /var/cache/debconf/* \
            /var/lib/apt/lists/* \
            /var/log/* \
            /tmp/* \
            /var/tmp/*

RUN pip install -U pip \
    && pip install \
        yq \
        jsonschema \
        j2cli

ARG BUILDER=/tmp/builder
RUN mkdir -p $BUILDER
COPY . $BUILDER
RUN chown -R $USER:$USER $BUILDER

USER $USER

ARG OUTPUT=$BUILDER/output
RUN mkdir -p $OUTPUT

VOLUME ["$OUTPUT"]

WORKDIR $BUILDER
ENTRYPOINT ["/bin/sh"]

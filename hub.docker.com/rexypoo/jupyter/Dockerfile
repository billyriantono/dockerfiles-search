FROM python:3-stretch AS base

WORKDIR /python

RUN python3 -m venv jupyter \
 && . jupyter/bin/activate \
 && pip install --no-cache-dir jupyter

RUN python3 -m venv virtualenv \
 && . virtualenv/bin/activate \
 && pip install --no-cache-dir virtualenv

# Install python-dev for some packages
RUN apt-get update && apt-get install -yq \
    python-dev \
 && rm -rf /var/lib/apt/lists/*

# Link jupyter and virtualenv to $PATH
RUN ln -s \
    $(pwd)/jupyter/bin/jupyter \
    /usr/local/bin \
 && ln -s \
    $(pwd)/virtualenv/bin/virtualenv \
    /usr/local/bin

FROM base AS drop-privileges
# Create user
ENV SHELL=/bin/bash \
    TEMPLATE=/jupyter/notebooks \
    UID=46323 \
    USER=jupyter
WORKDIR /"$USER"

RUN adduser \
    --disabled-password \
    --gecos "" \
    --home "$(pwd)" \
    --no-create-home \
    --uid "$UID" \
    "$USER" \
 && mkdir -p \
    .local/share/jupyter \
    config \
    kernels \
    notebooks \
    ve \
 && ln -s $(pwd)/config /"$USER"/.jupyter \
 && ln -s $(pwd)/kernels /"$USER"/.local/share/jupyter/ \
 && chown -R "$USER":"$USER" .

COPY sh sh

ADD https://raw.githubusercontent.com/Rexypoo/docker-entrypoint-helper/master/entrypoint-helper.sh /usr/local/bin/entrypoint-helper.sh
RUN chmod u+x /usr/local/bin/entrypoint-helper.sh
ENTRYPOINT ["entrypoint-helper.sh", "jupyter", "notebook"]
CMD ["--ip=0.0.0.0", "--no-browser", "--notebook-dir=/jupyter/notebooks"]
EXPOSE 8888

FROM drop-privileges AS install-tools

RUN apt update && apt install -yq \
    bash \
    man \
    tmux \
    vim \
    zip \
 && rm -rf /var/lib/apt/lists/*

FROM install-tools AS dev
ENTRYPOINT ["/usr/bin/env","bash"]

FROM install-tools AS release

LABEL org.opencontainers.image.url="https://hub.docker.com/r/rexypoo/jupyter" \
      org.opencontainers.image.documentation="https://hub.docker.com/r/rexypoo/jupyter" \
      org.opencontainers.image.source="https://github.com/Rexypoo/docker-jupyter" \
      org.opencontainers.image.version="0.1a" \
      org.opencontainers.image.licenses="MIT" \
      org.opencontainers.image.description="Jupyter on Docker" \
      org.opencontainers.image.title="rexypoo/jupyter" \
      org.label-schema.docker.cmd='mkdir -p "$HOME"/notebooks "$HOME"/.jupyter && \
      docker run -d \
      --name jupyter \
      -p 127.0.0.1:8888:8888 \
      --restart unless-stopped \
      --volume "$HOME"/notebooks:/jupyter/notebooks \
      --volume "$HOME"/.jupyter:/jupyter/config \
      rexypoo/jupyter && \
      docker exec -it \
      --user jupyter \
      jupyter \
      jupyter notebook list' \
      org.label-schema.docker.cmd.devel="docker run -it --entrypoint bash rexypoo/jupyter" \
      org.label-schema.docker.cmd.debug="docker exec -it jupyter bash"

FROM debian:latest

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update -qq && apt-get upgrade -y && \
    apt-get install -yq --no-install-recommends apt-utils && \
    apt-get install -yq --no-install-recommends locales \
      fonts-liberation \
      ca-certificates \
      python3-venv\
      curl \
    && rm -rf /var/lib/apt/lists/*

ENV LANGUAGE 	ru_RU.UTF-8
ENV LC_ALL 	ru_RU.UTF-8
ENV LANG 	ru_RU.UTF-8

RUN echo $LANG UTF-8 > /etc/locale.gen && \
    locale-gen && \
    dpkg-reconfigure locales

ENV TINI_VERSION v0.18.0
add https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /tini
RUN chmod +x /tini
ENTRYPOINT ["/tini", "-g", "--"]

RUN sed -i 's/^#force_color_prompt=yes/force_color_prompt=yes/' /etc/skel/.bashrc && \
    useradd -m -s /bin/bash -N -u 1000 data && \
    ln -snf /bin/bash /bin/sh

USER data
ENV env .dev
WORKDIR /home/data
RUN python3 -m venv $env && \
    source $env/bin/activate && \
    curl https://bootstrap.pypa.io/get-pip.py -o .get-pip.py && \
    python3 .get-pip.py && \
    pip install jupyter

USER root
COPY start.sh /usr/local/bin/
RUN chmod +x /usr/local/bin/start.sh
CMD ["start.sh"]
EXPOSE 8888
USER data


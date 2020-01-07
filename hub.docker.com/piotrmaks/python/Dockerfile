FROM archlinux/base

ADD https://github.com/Yelp/dumb-init/releases/download/v1.2.2/dumb-init_1.2.2_amd64 /usr/bin/dumb-init
RUN chmod +x /usr/bin/dumb-init
ENTRYPOINT ["/usr/bin/dumb-init", "--"]
CMD ["/bin/bash"]

RUN pacman -Syyu --noconfirm \
 && pacman -S --noconfirm \
      python \
      make \
      spatialindex \
 && pacman -Scc --noconfirm \
 && python3 -m ensurepip \
 && pip3 install --no-cache-dir --upgrade pip setuptools \
 && pip3 install --no-cache-dir jupyter networkx osmnx pyyaml geopy

ARG GROUP=1000
ARG USER=1000

RUN groupadd --gid ${GROUP} pay \
 && useradd --uid ${USER} \
            --create-home \
            --gid pay \
            --shell /bin/bash \
            pay

USER pay

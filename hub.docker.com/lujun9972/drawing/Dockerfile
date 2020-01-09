FROM ubuntu:19.10
RUN apt update && apt install -y --no-install-recommends software-properties-common && rm -rf /var/lib/apt/lists/* && rm -rf /var/cache/apk/* && apt-get autoremove
RUN add-apt-repository -y ppa:cartes/drawing && apt update && apt install -y --no-install-recommends drawing && rm -rf /var/lib/apt/lists/* && rm -rf /var/cache/apk/* && apt-get autoremove
# RUN locale-gen zh_CN.UTF-8
# ENV LANG zh_CN.UTF-8
RUN groupadd --gid 1000 user
RUN useradd --home-dir /home/user --gid 1000 --create-home --uid 1000 user
USER user
CMD ["drawing"]

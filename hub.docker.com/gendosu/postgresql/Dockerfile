FROM      postgres:9.6.8

RUN apt-get update \
&&  apt-get install -y --force-yes \
    locales \
&&  apt-get clean \
&&  rm -rf /var/cache/apt/archives/* /var/lib/apt/lists/*

# defaultのlocaleをja_JP.UTF-8にする
#ENV LANG=ja_JP.UTF-8
RUN echo "ja_JP.UTF-8 UTF-8" > /etc/locale.gen
RUN echo "en_US.UTF-8 UTF-8" >> /etc/locale.gen
RUN echo /etc/locale.gen
RUN locale-gen

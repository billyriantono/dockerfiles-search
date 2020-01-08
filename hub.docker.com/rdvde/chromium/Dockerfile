FROM jess/chromium
USER root
RUN usermod -u 1000 chromium \
  && groupmod -g 1000 chromium
RUN apt-get update \
	&& apt-get upgrade -y \
	&& apt-get install -y locales ttf-wqy-zenhei dbus-x11 libx11-xcb1 \
	&& localedef -i zh_TW -c -f UTF-8 -A /usr/share/locale/locale.alias zh_TW.UTF-8 \
	&& apt-get autoremove -y \
	&& apt-get autoclean \
        && apt-get clean \
	&& rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

ENV LC_CTYPE=zh_TW.UTF-8 \
    GTK_IM_MODULE=fcitx \
    QT_IM_MODULE=fcitx \
    XMODIFIERS='@im=fcitx'

USER chromium

ENTRYPOINT [ "/usr/bin/chromium" ]
CMD [ "--no-sandbox", "--incognito", "-user-agent=Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/73.0.3683.75 Safari/537.36" ]


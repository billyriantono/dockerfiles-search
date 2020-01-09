FROM python:3
RUN pip3 install nextcloud_news_updater --install-option="--install-scripts=/usr/bin"
ENTRYPOINT [ "/usr/bin/nextcloud-news-updater" ]
FROM wikimedia/mediawiki:latest
MAINTAINER Kasper Rynning-Tønnesen <kasper@kasperrt.no>

RUN git clone --recursive https://github.com/kasperrt/MediaWiki-OAuth2-Dataporten.git /OAuth2Dataporten
#COPY OAuth2Dataporten/ /OAuth2Dataporten

RUN sed -i '$ d' /entrypoint.sh
RUN echo 'cp -ar /OAuth2Dataporten/ /var/www/html/extensions/OAuth2Dataporten/' >> /entrypoint.sh
RUN echo 'echo "\$wgShowExceptionDetails = true;" >> /var/www/html/LocalSettings.php' >> /entrypoint.sh
RUN echo 'echo "require_once \"\$IP/extensions/OAuth2Dataporten/OAuth2Dataporten.php\";" >> /var/www/html/LocalSettings.php' >> /entrypoint.sh
RUN echo 'php /var/www/html/maintenance/update.php --conf /var/www/html/LocalSettings.php --quick' >> /entrypoint.sh
RUN echo 'exec "$@"' >> /entrypoint.sh

#CMD ["/bin/bash"]
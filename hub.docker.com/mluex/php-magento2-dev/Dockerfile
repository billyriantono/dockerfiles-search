FROM mluex/php-dev:7.2

RUN wget https://raw.githubusercontent.com/mluex/maid/master/maid.sh && \
    chmod +x maid.sh && \
    mv maid.sh /usr/local/bin/maid

RUN npm install -g grunt-cli

# TODO: Add cron job
#ADD crontab /etc/cron.d/magento2-cron
#RUN chmod 0644 /etc/cron.d/magento2-cron \
#    && crontab /etc/cron.d/magento2-cron
#CMD cron -f

WORKDIR /home/wwwroot/

EXPOSE 9000
CMD ["php-fpm"]
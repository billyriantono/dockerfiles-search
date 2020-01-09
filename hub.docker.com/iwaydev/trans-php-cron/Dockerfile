FROM iwaydev/base-php-cron-5.6-prod

WORKDIR /var/www/iway

RUN apt update

# Locales
RUN apt install -y locales \
&& printf 'de_AT.UTF-8 UTF-8\n' >> /etc/locale.gen \
&& printf 'de_BE.UTF-8 UTF-8\n' >> /etc/locale.gen \
&& printf 'de_CH.UTF-8 UTF-8\n' >> /etc/locale.gen \
&& printf 'de_DE.UTF-8 UTF-8\n' >> /etc/locale.gen \
&& printf 'de_LI.UTF-8 UTF-8\n' >> /etc/locale.gen \
&& printf 'de_LU.UTF-8 UTF-8\n' >> /etc/locale.gen \
&& printf 'en_AG.UTF-8 UTF-8\n' >> /etc/locale.gen \
&& printf 'en_AG.UTF-8 UTF-8\n' >> /etc/locale.gen \
&& printf 'en_AU.UTF-8 UTF-8\n' >> /etc/locale.gen \
&& printf 'en_BW.UTF-8 UTF-8\n' >> /etc/locale.gen \
&& printf 'en_CA.UTF-8 UTF-8\n' >> /etc/locale.gen \
&& printf 'en_DK.UTF-8 UTF-8\n' >> /etc/locale.gen \
&& printf 'en_GB.UTF-8 UTF-8\n' >> /etc/locale.gen \
&& printf 'en_HK.UTF-8 UTF-8\n' >> /etc/locale.gen \
&& printf 'en_IE.UTF-8 UTF-8\n' >> /etc/locale.gen \
&& printf 'en_IN.UTF-8 UTF-8\n' >> /etc/locale.gen \
&& printf 'en_IN.UTF-8 UTF-8\n' >> /etc/locale.gen \
&& printf 'en_NG.UTF-8 UTF-8\n' >> /etc/locale.gen \
&& printf 'en_NG.UTF-8 UTF-8\n' >> /etc/locale.gen \
&& printf 'en_NZ.UTF-8 UTF-8\n' >> /etc/locale.gen \
&& printf 'en_PH.UTF-8 UTF-8\n' >> /etc/locale.gen \
&& printf 'en_SG.UTF-8 UTF-8\n' >> /etc/locale.gen \
&& printf 'en_US.UTF-8 UTF-8\n' >> /etc/locale.gen \
&& printf 'en_ZA.UTF-8 UTF-8\n' >> /etc/locale.gen \
&& printf 'en_ZM.UTF-8 UTF-8\n' >> /etc/locale.gen \
&& printf 'en_ZM.UTF-8 UTF-8\n' >> /etc/locale.gen \
&& printf 'en_ZW.UTF-8 UTF-8\n' >> /etc/locale.gen \
&& printf 'ru_RU.UTF-8 UTF-8\n' >> /etc/locale.gen \
&& printf 'ru_UA.UTF-8 UTF-8\n' >> /etc/locale.gen \
&& printf 'zh_CN.UTF-8 UTF-8\n' >> /etc/locale.gen \
&& printf 'zh_HK.UTF-8 UTF-8\n' >> /etc/locale.gen \
&& printf 'zh_SG.UTF-8 UTF-8\n' >> /etc/locale.gen \
&& printf 'zh_TW.UTF-8 UTF-8\n' >> /etc/locale.gen \

# cron
RUN apt-get install -y cron

#cron table
RUN touch /etc/cron.d/crontab
RUN chmod 777 /etc/cron.d/crontab
RUN touch /var/log/cron.log
ENTRYPOINT ["docker/builds/php-cron/docker-entrypoint.sh"]

RUN apt-get autoremove && apt-get clean

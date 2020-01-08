FROM bamos/openface

ADD run.sh /app/run.sh
ADD supervisord.conf /etc/supervisord.conf

RUN add-apt-repository -y ppa:certbot/certbot \
 && add-apt-repository ppa:openjdk-r/ppa \
 && apt-get update \
 && apt-get install -y certbot openjdk-8-jdk-headless nginx supervisor \
 && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
 && rm /etc/nginx/sites-enabled/default \
 && useradd -m app && echo "app:app" | chpasswd && adduser app sudo \
 && chown -R app /app \
 && chgrp adm /var/log && chmod g+w /var/log && chmod g+w /var/log/nginx \
 && chown app /var/log/nginx/* \
 && chgrp adm /var/log/supervisor && chmod g+w /var/log/supervisor \
 && adduser app adm \
 && echo 'app ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers \
 && chmod a+rx /root

ADD nginx.conf /etc/nginx/nginx.conf

USER app
WORKDIR /app

CMD ["./run.sh"]
FROM odoo:9.0

USER root
RUN curl -sL https://deb.nodesource.com/setup_6.x | bash - && apt-get install -y nodejs
RUN pip install supervisor
RUN npm install -g less
RUN mkdir -p /var/log/supervisor /app/ && chown -R 104:107 /app/ /var/log/supervisor
ADD supervisord.conf /etc/supervisor/

ADD package.json docker-entrypoint.sh /app/

WORKDIR /app/
RUN npm install
ADD src/ /app/src/
RUN npm run build

USER odoo

ENV FILE_STORE "/var/lib/odoo/filestore/"
VOLUME ["/var/lib/odoo/filestore"]

ENTRYPOINT ["supervisord", "-n"]

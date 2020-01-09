FROM redash/redash:5.0.1.b4850

USER root

RUN pip install Jinja2==2.10 drest ldap3

COPY . ./
RUN cp /app/client/app/assets/images/db-logos/url.png /app/client/app/assets/images/db-logos/url2.png
RUN npm install && npm run build && rm -rf node_modules
RUN chown -R redash /app

USER redash


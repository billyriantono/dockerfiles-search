FROM kong

WORKDIR /etc/kong

ENV KONG_DATABASE off
ENV KONG_DECLARATIVE_CONFIG /etc/kong/kong.yml
ENV KONG_ADMIN_LISTEN 0.0.0.0:8001

COPY . .
RUN cp kong.conf.default kong.conf

EXPOSE 8000 8001 8443 8444

CMD kong start -c kong.conf

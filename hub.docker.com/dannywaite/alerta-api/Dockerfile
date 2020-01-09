FROM alpine:3.4

RUN  apk --no-cache --update add py-gunicorn python py-pip libffi musl \
  && apk --no-cache --update add --virtual build-dependencies python-dev build-base libffi-dev \
  && pip install alerta-server \
  && apk del build-dependencies

ENV ALERTA_SVR_CONF_FILE /alertad.conf

ENV AUTH_REQUIRED False
ENV ADMIN_USERS not-set
ENV CUSTOMER_VIEWS False
ENV CLIENT_ID not-set
ENV CLIENT_SECRET not-set
ENV ALLOWED_EMAIL_DOMAIN *
ENV CORS_ORIGINS not-set

ADD alertad.conf.sh /alertad.conf.sh

EXPOSE 8000
CMD /alertad.conf.sh && \
    gunicorn \
      --chdir /var/lib alerta.app:app \
      --bind 0.0.0.0:8000 \
      --access-logfile - \
      --error-logfile -

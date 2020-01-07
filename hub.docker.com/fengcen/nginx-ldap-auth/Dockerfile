FROM python:2-alpine

RUN apk --no-cache add openldap-dev \
    && apk --no-cache add --virtual build-dependencies build-base wget \
    && pip install python-ldap \
    && wget https://github.com/nginxinc/nginx-ldap-auth/archive/master.tar.gz -O ldap.tar.gz \
    && tar -zxC /usr/src -f ldap.tar.gz \
    && rm ldap.tar.gz \
    && apk del build-dependencies

EXPOSE 8888

CMD ["python", "/usr/src/nginx-ldap-auth-master/nginx-ldap-auth-daemon.py", "--host", "0.0.0.0"]

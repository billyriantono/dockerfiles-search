FROM bitbucket/hipbucket_base

RUN useradd -U sentry
RUN easy_install -UZ sentry[postgres]
RUN pip install python-memcached redis hiredis nydus psycopg2 django-redis
RUN mkdir /sentry

COPY ./supervisord.conf /etc/supervisor/conf.d/supervisord.conf
COPY ./nginx.conf /etc/nginx/nginx.conf
COPY ./sentry.conf.py /sentry/sentry.conf.py
 
EXPOSE 80

CMD supervisord

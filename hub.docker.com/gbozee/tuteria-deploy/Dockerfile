FROM tuteria/django_app
MAINTAINER Biola Oyeniyi "gbozee@gmail.com"

ENV REFRESHED_AT 2015-01-01


RUN mkdir -p /home/app
COPY ./requirements /home/app/requirements
RUN pip install -r /home/app/requirements/staging2.txt
RUN easy_install -U distribute && pip install -r /home/app/requirements/test.txt
WORKDIR /home/app
VOLUME ["/home/app","/tmp"]
RUN mkdir -p /scripts && chown app /scripts && chgrp app /scripts && mkdir -p /home/app/build/django-annoying
ADD run_server.sh /scripts/ 

RUN chmod +x /scripts/run_server.sh

RUN mkdir -p /var/tuteria && usermod -a -G www-data app && chgrp -R www-data /var/tuteria && chmod -R g+w /var/tuteria && chown app /var/tuteria

VOLUME /var/tuteria

RUN pip install factory_boy && \
	pip install django-debug-toolbar-line-profiler && \
	pip install django-debug-toolbar-template-profiler && \
	pip install pympler

CMD ["/scripts/run_server.sh"]

EXPOSE 8000



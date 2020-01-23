FROM apsl/thumbor

RUN pip install thumbor-cloud-storage

COPY thumbor.conf.tpl /usr/src/app/thumbor.conf.tpl.extended

RUN cat /usr/src/app/thumbor.conf.tpl.extended >> /usr/src/app/thumbor.conf.tpl

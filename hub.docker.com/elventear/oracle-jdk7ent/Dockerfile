FROM apsl/thumbor

COPY . /usr/src/thumbor_cloud_storage

WORKDIR /usr/src/thumbor_cloud_storage
RUN python setup.py bdist_wheel

WORKDIR /usr/src/app

RUN pip install /usr/src/thumbor_cloud_storage/dist/thumbor_cloud_storage-3.0.0-py2.py3-none-any.whl

COPY thumbor.conf.tpl /usr/src/app/thumbor.conf.tpl.extended

RUN cat /usr/src/app/thumbor.conf.tpl.extended >> /usr/src/app/thumbor.conf.tpl

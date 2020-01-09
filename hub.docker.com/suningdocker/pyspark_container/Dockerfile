ARG CODE_VERSION=develop

FROM suningdocker/py_rpc:${CODE_VERSION}

COPY suningclipper_admin/suningclipper_admin/python_container_conda_deps.txt /lib/

RUN echo deb http://ftp.de.debian.org/debian jessie-backports main >> /etc/apt/sources.list \
      && apt-get update --fix-missing \
      && apt-get install -yqq -t jessie-backports openjdk-8-jdk \
      && conda install -y --file /lib/python_container_conda_deps.txt \
      && pip --no-cache-dir install pyspark

COPY containers/python/pyspark_container.py containers/python/pyspark_container_entry.sh /container/

COPY VERSION.txt /lib/

COPY suningclipper_admin/ /lib/suningclipper_admin

RUN pip install /lib/suningclipper_admin

CMD ["/container/pyspark_container_entry.sh"]
FROM centos/python-35-centos7

ENV HOME=/conan

USER root

RUN bash -c 'pip install --no-cache-dir conan'

RUN mkdir -p /var/lib/conan \
 && mkdir -p /conan/.conan_server \
 && chgrp -vR 0 /var/lib/conan /conan \
 && chmod -vR g+rwX /var/lib/conan /conan

COPY server.conf /conan/.conan_server

EXPOSE 9300

USER 1001

CMD ["conan_server"]

FROM fedora:27
ENV PATH=/app/bin:/bin:/usr/bin:/sbin:/usr/sbin
RUN yum -y install python3 python3-virtualenv; yum clean all
RUN python3 -m virtualenv /app
RUN /app/bin/pip install envtpl

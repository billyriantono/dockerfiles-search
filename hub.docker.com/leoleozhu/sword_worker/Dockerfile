FROM python:3.6

ADD 3rd_party/viesus/8.5/viesus*.deb /tmp
RUN dpkg -i /tmp/viesus*.deb
RUN rm -rf /tmp/viesus*.deb

RUN echo "/usr/local/lib64"  > /etc/ld.so.conf.d/viesus.conf && ldconfig

ENV workdir /workdir-sword
RUN mkdir -p ${workdir}
WORKDIR ${workdir}

ADD requirements.txt ${workdir}
RUN pip install -r requirements.txt

ADD sword ${workdir}/sword

ENTRYPOINT ["celery", "-E", "-A", "sword.tasks", "worker"]

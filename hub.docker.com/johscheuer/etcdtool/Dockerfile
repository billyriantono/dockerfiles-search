FROM fedora:27

# TODO create etcdtool user

RUN curl -sLO https://github.com/mickep76/etcdtool/releases/download/3.3.2/etcdtool-3.3-201605022100.x86_64.rpm && \
    dnf install -y etcdtool-3.3-201605022100.x86_64.rpm && \
    rm -f etcdtool-3.3-201605022100.x86_64.rpm && \
    useradd etcdtool

USER etcdtool

ENTRYPOINT [ "/bin/bash", "-c" ]
CMD [ "bash" ]

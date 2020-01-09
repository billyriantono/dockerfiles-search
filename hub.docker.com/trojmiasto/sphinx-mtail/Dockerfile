FROM ubuntu:16.04
LABEL maintainer="Łukasz Górski <l.gorski@trojmiasto.pl>"

COPY mtail /usr/local/bin/mtail
COPY progs/* /etc/mtail/
EXPOSE 3903
ENTRYPOINT ["/usr/local/bin/mtail"]
CMD ["-progs", "/etc/mtail", "-logtostderr", "-logs", "/var/log/sphinxsearch/query.log"]

FROM cznic/knot-resolver

ADD config.docker \
    DigiCertGlobalRootCA.crt \
    /data/

ENTRYPOINT ["/usr/sbin/kresd"]
CMD ["-f","1","-c", "/etc/knot-resolver/kresd.conf"]

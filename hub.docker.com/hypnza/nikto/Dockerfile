FROM hypnza/nmap

RUN apk add --update --no-cache perl-net-ssleay nikto

ENTRYPOINT ["/usr/bin/nikto.pl"]
CMD ["-H"]

FROM akolosov/haproxy-base

ADD haproxy-osrm.cfg /etc/haproxy/configs/osrm.cfg

EXPOSE 5000

# Define entrypoint
CMD ["haproxy", "-f", "/etc/haproxy/haproxy.cfg", "-f", "/etc/haproxy/configs/osrm.cfg"]


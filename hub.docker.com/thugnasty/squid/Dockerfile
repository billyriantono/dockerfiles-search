FROM minimum2scp/squid:latest

# install package to get 'htpasswd' tool
RUN apt install -y apache2-utils

# squid config
COPY squid.conf /etc/squid/squid.conf

# add user/pass for proxy authentication
RUN htpasswd -b -c /etc/squid/passwords hobo derelict

CMD ["/sbin/init"]

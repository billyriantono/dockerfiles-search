FROM codingwell/rpi-raspbian-qemu

MAINTAINER  J.P.C. Oudeman

# Install nginx
RUN [ "cross-build-start" ]
RUN \
echo "deb http://mirrordirector.raspbian.org/raspbian/ stretch main" >> /etc/apt/sources.list.d/mirrordirector.list && \
apt-key adv --fetch-keys http://mirrordirector.raspbian.org/raspbian.public.key && \
echo "Package: * " > /etc/apt/preferences && \
echo "Pin: release n=jessie" >> /etc/apt/preferences && \ 
echo "Pin-Priority: 600" >> /etc/apt/preferences && \
apt-get update && \
apt-get install -y -t stretch nginx && \
\
# forward request and error logs to docker log collector
ln -sf /dev/stdout /var/log/nginx/access.log && \
ln -sf /dev/stderr /var/log/nginx/error.log && \
\
# Cleanup
apt-get clean -y && \
rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN [ "cross-build-end" ]  

CMD ["nginx", "-g", "daemon off;"]

WORKDIR /var/www/html
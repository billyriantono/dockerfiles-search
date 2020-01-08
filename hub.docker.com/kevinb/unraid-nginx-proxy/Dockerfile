FROM nginx

# Install wget and install/updates certificates
#RUN apk add --no-cache --virtual .run-deps \
#    ca-certificates bash wget openssl \
#    && update-ca-certificates

# Set correct environment variables
#ENV DEBIAN_FRONTEND=noninteractive HOME="/root" TERM=xterm LANG=en_US.UTF-8 LANGUAGE=en_US:en LC_ALL=en_US.UTF-8

# Set the locale
#RUN locale-gen en_US.UTF-8

#ENV DOCKER_GEN_VERSION 0.7.4

#RUN wget --quiet https://github.com/jwilder/docker-gen/releases/download/$DOCKER_GEN_VERSION/docker-gen-alpine-linux-amd64-$DOCKER_GEN_VERSION.tar.gz \
# && tar -C /usr/local/bin -xvzf docker-gen-alpine-linux-amd64-$DOCKER_GEN_VERSION.tar.gz \
# && rm /docker-gen-alpine-linux-amd64-$DOCKER_GEN_VERSION.tar.gz

#COPY network_internal.conf /etc/nginx/

#COPY . /app/
#WORKDIR /app/

#ENV DOCKER_HOST unix:///tmp/docker.sock

# Configure user nobody to match unRAID's settings
RUN usermod -u 99 nobody && \
	usermod -g 100 nobody && \
	usermod -d /home nobody && \
	chown -R nobody:users /home

RUN cp /etc/nginx/conf.d/*.conf /home

# Volumes
VOLUME ["/etc/nginx/certs", "/etc/nginx/dhparam", "/etc/nginx/conf.d"]
#VOLUME ["/config"]

RUN chown -R nobody:users /etc/nginx/conf.d && \
  chmod -R 0777 /etc/nginx/conf.d

# Exposed Ports 
# EXPOSE 8080
CMD ["nginx", "-g", "daemon off;"]

# Configure Nginx and apply fix for very long server names
#RUN echo "daemon off;" >> /etc/nginx/nginx.conf \
# && sed -i 's/worker_processes  1/worker_processes  auto/' /etc/nginx/nginx.conf

# Disable SSH
#RUN rm -rf /etc/service/sshd /etc/my_init.d/00_regen_ssh_host_keys.sh
 
# Use baseimage-docker's init system.
#CMD ["/sbin/my_init"]

# Update Image
#RUN apt-get update && apt-get install -y libssl1.0.0 libpcre3 --no-install-recommends && rm -rf /var/lib/apt/lists/*

#RUN apt-add-repository ppa:vbernat/haproxy-1.5 && \
#    apt-get -q update && \
#    apt-get upgrade -qy -o Dpkg::Options::="--force-confold" && \
#    apt-get install -qy haproxy curl wget vim nano vim-haproxy && \
#    apt-get clean && \
#    rm -rf /var/lib/apt/lists/* && \
#    chown -R nobody:users /usr/sbin/haproxy && \
#	chmod -R 0777 /usr/sbin/haproxy

# Add default cnf, we'll move it to the /config volume in init_haproxy.sh
#ADD haproxy.cfg /root/

# Initialize haproxy on boot
#RUN mkdir -p /etc/my_init.d
#ADD init_haproxy.sh /etc/my_init.d/
#RUN chmod +x /etc/my_init.d/init_haproxy.sh

#Start haproxy when container starts
#RUN mkdir -p /etc/service/haproxy
#ADD haproxy.sh /etc/service/haproxy/run
#RUN chmod +x /etc/service/haproxy/run


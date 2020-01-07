FROM debian:latest
MAINTAINER Joel Cressy joel@jtcressy.net
WORKDIR /app
VOLUME /app
# Set locale
RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y locales curl sudo
RUN sed -i -e 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/' /etc/locale.gen && \
    echo 'LANG="en_US.UTF-8"'>/etc/default/locale && \
    dpkg-reconfigure --frontend=noninteractive locales && \
    update-locale LANG=en_US.UTF-8
ENV LANG en_US.UTF-8 
#create user for meteor
RUN mkdir /home/meteor && \
    groupadd -r meteor -g 433 && \
    useradd -u 431 -r -g meteor -d /home/meteor -s /sbin/nologin -c "meteor user" meteor && \
    chown -R meteor:meteor /home/meteor && \
    touch /etc/sudoers && echo '%meteor ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers
#install meteor
USER meteor
RUN curl https://install.meteor.com/ | sh
#ENV PATH /home/meteor/.meteor:$PATH
EXPOSE 3000
COPY ./entrypoint.sh /entrypoint.sh
ENTRYPOINT /entrypoint.sh


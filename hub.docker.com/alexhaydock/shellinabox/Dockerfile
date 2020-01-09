FROM centos:7
LABEL maintainer "Alex Haydock <alex@alexhaydock.co.uk>"

# So here is a fun little project where I put a PHP web shell inside a Docker
# container. I don't use it for any particular purpose, but I imagine it would
# be good for penetration testing on services which allow users to run Docker
# containers in the cloud with otherwise minimal interactivity.

# shellinabox: https://github.com/shellinabox/shellinabox

# Usage: Forward HTTP port 80 to this container and log in as "shell" with the
#        password "bacon". You can 'su root' with the same password.
#        From there, what you do is up to you.

RUN set -xe \
# Install Deps
    && yum install -y git openssl-devel pam-devel zlib-devel autoconf automake libtool make \
# Clone Repo
    && git clone https://github.com/shellinabox/shellinabox.git && cd shellinabox \
# Run autotools & make
    && autoreconf -i \
    && ./configure \
    && make \
# Add a shell user (root is blocked from using shellinabox)
    && adduser shell \
    && echo -e "bacon\nbacon" | passwd shell \
# Change root password so we can elevate with 'su' after logging in as 'shell'
    && echo -e "bacon\nbacon" | passwd root

EXPOSE 80
ENTRYPOINT ["/shellinabox/shellinaboxd", "-t", "--user=0", "--port=80"]

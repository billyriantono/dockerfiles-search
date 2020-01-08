FROM debian:jessie

# Try an APT cache at the build host (assuming default docker bridged network)
RUN echo "Acquire::http::Proxy \"http://172.17.42.1:3142\";" > /etc/apt/apt.conf.d/01proxy
RUN (apt-get update && cd /var/cache/apt/archives/ && apt-get download ruby) || (rm -f /etc/apt/apt.conf.d/01proxy && apt-get update)

# Install Ruby
RUN apt-get update && apt-get install -qy ruby bundler sudo
RUN adduser --disabled-password tester
RUN echo 'tester ALL=(ALL) NOPASSWD:ALL' > /etc/sudoers.d/tester

# Cleanup
RUN rm -f /etc/apt/apt.conf.d/01proxy
RUN apt-get clean

USER tester

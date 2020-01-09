FROM centos:7.7.1908

# add install bash script
ADD build/root/*.sh /root/

# run the install script
RUN ["/bin/bash", "/root/install.sh"]

# set environment variables for user nobody
ENV HOME /home/nobody

# set environment variable for terminal
ENV TERM xterm

# set environment variables for language
ENV LANG en_GB.UTF-8

# run tini to manage graceful exit and zombie reaping
ENTRYPOINT ["/usr/bin/tini", "--"]

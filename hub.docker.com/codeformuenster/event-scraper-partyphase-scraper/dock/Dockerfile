FROM node:8
RUN apt-get update && apt-get install -y openssh-server
RUN mkdir /var/run/sshd
RUN echo 'node:todo' | chpasswd
RUN echo 'AllowUsers node' >> /etc/ssh/sshd_config
RUN chsh -s /usr/local/bin/node node
WORKDIR /home/node
COPY ascii-art.txt .
COPY ascii-art.txt /etc/motd
EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]
RUN cat ascii-art.txt; echo "BUILT SUCCESSFULLY!"; echo

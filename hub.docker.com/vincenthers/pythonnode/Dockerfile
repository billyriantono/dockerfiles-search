FROM ubuntu:wily
RUN apt-get install -y python3.5 curl openssl git
RUN ln -s /usr/bin/python3.5 /usr/bin/python
RUN ln -s /usr/bin/python3.5 /usr/bin/python3
COPY get-pip.py /tmp/
RUN cd /tmp/; python get-pip.py
RUN curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.31.0/install.sh | bash
RUN echo 'source /root/.nvm/nvm.sh' >> /etc/profile
CMD ["/bin/bash", "--login"]

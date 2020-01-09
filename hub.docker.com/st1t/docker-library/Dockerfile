FROM st1t/docker-library:amazonlinux-2

# Set AWS CLI
RUN wget https://bootstrap.pypa.io/get-pip.py \
    && python get-pip.py \
    && pip install awscli \
    && rm -rf /root/.cache get-pip.py

CMD ["/sbin/init"]

FROM mongo

COPY setup.sh /root/setup.sh
COPY mongod.conf /etc/mongod.conf

ENTRYPOINT ["/root/setup.sh"]
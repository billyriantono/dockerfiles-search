FROM ipfs/go-ipfs

COPY start_ipfs.sh /usr/local/bin/start_ipfs
RUN chmod +x /usr/local/bin/start_ipfs

ENTRYPOINT ["/usr/local/bin/start_ipfs"]
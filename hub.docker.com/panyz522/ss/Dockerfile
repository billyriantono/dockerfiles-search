FROM mritd/shadowsocks
ENV pwd=tpdt1234
ENV method=chacha20-ietf-poly1305 
ENV port=7894
EXPOSE 7894
ENTRYPOINT ["/bin/sh", "-c", "/entrypoint.sh -s \"-s 0.0.0.0 -p $port -m $method -k $pwd\""]

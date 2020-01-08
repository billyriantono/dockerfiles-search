from alpine

COPY badvpn-udpgw /usr/bin/badvpn-udpgw
RUN chmod +x /usr/bin/badvpn-udpgw
CMD ["sh", "-c", "/usr/bin/badvpn-udpgw --listen-addr 0.0.0.0:7300"]

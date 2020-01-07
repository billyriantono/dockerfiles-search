FROM busybox:ubuntu-14.04
MAINTAINER william0wang

# Install ngrok
COPY ngrokd /bin/ngrokd
RUN chmod 755 /bin/ngrokd

CMD ngrokd -tunnelAddr="${ngrok_tunnelAddr}" -tlsKey="${ngrok_tlsKey}" -tlsCrt="${ngrok_tlsCrt}" -domain="${ngrok_domain}"

FROM node:8-slim
WORKDIR /opt/glass
COPY . /opt/glass
RUN mkdir logs && chmod u+x ./bin/ -R && chmod u+x *.sh && npm install
#VOLUME /var/lib/dhcp/dhcpd.leases /var/log/dhcp.log /etc/dhcp/dhcpd.conf /opt/glass/config
EXPOSE 3000
ENTRYPOINT ["npm", "start"]

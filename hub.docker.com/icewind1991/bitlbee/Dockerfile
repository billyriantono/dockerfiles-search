FROM fedora:24

RUN dnf -y install 'dnf-command(copr)'; \
	dnf -y copr enable larsks/bitlbee-facebook; \
        dnf -y copr enable mavjs/bitlbee-steam; \
	dnf -y install \
	bitlbee \
	iproute \
	bitlbee-facebook \
	bitlbee-otr \
        bitlbee-steam \
	; dnf clean all

RUN rm -f /etc/bitlbee/bitlbee.conf
COPY bitlbee.conf.in /etc/bitlbee/bitlbee.conf.in

COPY entrypoint.sh /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]

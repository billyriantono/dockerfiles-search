FROM alpine

MAINTAINER wtf

COPY uml.sh /root/
COPY haproxy.cfg /root/

RUN apk update \
    && apk add iptables iproute2 curl haproxy \
	&& curl -SL https://github.com/dapao9999/uml/raw/master/alpine_bbr_ss_swap.img.tar.gz \
	| tar -xzC /root \
	&& curl -SL https://github.com/dapao9999/uml/raw/master/vmlinux_4.10.1.tar.gz \
	| tar -xzC /root \
	&& chmod +x /root/vmlinux_4.10.1 \
	            /root/alpine_bbr_ss_swap.img \
				/root/uml.sh
	
CMD /root/uml.sh

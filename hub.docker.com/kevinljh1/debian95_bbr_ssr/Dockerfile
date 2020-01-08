FROM debian:latest
#RUN apt-get update && apt-get install -y python3 python3-pip nodejs
RUN echo "net.core.default_qdisc=fq\nnet.ipv4.tcp_congestion_control=bbr" >> /etc/sysctl.conf
CMD ["sysctl","-p"]

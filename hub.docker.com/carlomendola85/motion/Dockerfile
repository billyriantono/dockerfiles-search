FROM debian:9.5

RUN apt-get update 
RUN apt-get install -y motion
COPY motion.conf /etc/motion/motion.conf

CMD ["motion","-n"]


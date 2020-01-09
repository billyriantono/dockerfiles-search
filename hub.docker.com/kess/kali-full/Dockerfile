# Kali Linux image with "kali-linux-full" metapackages

FROM kalilinux/kali-linux-docker:latest

RUN apt-get update\
	&& apt-get install kali-linux-full -y\
	&& apt-get upgrade -y

CMD ["bash"]

FROM ahayden/debian:latest

RUN apt-get update && apt-get install -y --no-install-recommends \
		nmap neovim git openssh-client openssh-server sudo curl binutils dnsutils iputils-ping\
	&& rm -rf /var/lib/apt/lists/*

RUN adduser --disabled-password user && \
	echo "user ALL=(root) NOPASSWD:ALL" >/etc/sudoers.d/user && \
	chmod 0440 /etc/sudoers.d/user

RUN su - user -c "cd && mkdir -p persist/.ssh && ln -s persist/.ssh . ; \
		mkdir -p persist/src && ln -s persist/src . ; \
		touch persist/.gitconfig && ln -s persist/.gitconfig ."

EXPOSE 22

CMD ["su", "-", "user"]


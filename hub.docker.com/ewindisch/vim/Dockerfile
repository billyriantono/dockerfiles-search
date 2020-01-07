FROM ubuntu:latest
RUN apt-get update; \
	apt-get install -qy vim-full
COPY usergen.sh /var/tmp/
RUN /var/tmp/usergen.sh
ADD vimrc /root/.vimrc
ADD vim /root/.vim

WORKDIR /mnt

ENTRYPOINT ["/usr/bin/vim"]

# without args will show file tree
CMD ["."]

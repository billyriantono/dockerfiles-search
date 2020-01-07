FROM alpine

USER root

ADD . /tmp/

ENV TERM xterm

RUN apk update && \
	apk upgrade && \
	apk add ca-certificates curl bash bash-completion ncurses vim tar ncdu \
	git git-bash-completion mtr wget bzip2 tig htop && \
	bash /tmp/init.sh

VOLUME ["/data","/log"]

CMD ["bash"]
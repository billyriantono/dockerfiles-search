FROM eclipse/stack-base:debian
ENV PATH /home/user/.local/bin:$PATH
RUN sudo apt-get update && \
	curl -sSL https://get.haskellstack.org/ | sh && \
	stack setup
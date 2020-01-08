FROM jamesrwhite/minicron
MAINTAINER Brian Wojtczak 
RUN minicron db setup
EXPOSE 9292
CMD ["minicron", "server", "--debug"]

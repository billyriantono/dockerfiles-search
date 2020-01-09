FROM alpine:3.8 

# docker run -v ~/.ssh/:/root/.ssh/ --rm -p 8080:8080 autossh
# Turn of monitoring
ENV AUTOSSH_PORT 0
#ENV AUTOSSH_DEBUG true
ENV AUTOSSH_LOGFILE /dev/stderr

RUN apk add --no-cache autossh
EXPOSE 58080

#ENTRYPOINT exec autossh -D 0.0.0.0:58080 -N mikael@fr2.kjr.dk -p 56789 true
ENTRYPOINT exec autossh -D 0.0.0.0:58080 -N $SSH_USER@$SSH_HOST -p ${SSH_PORT:-22} true


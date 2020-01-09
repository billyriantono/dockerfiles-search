# References :
# https://
FROM byte13/nodejs-alpine:latest

RUN apk add make libc-dev g++ git python python3 --update


#
# Next line as workaround due to some access errors since NodeJS 8
# https://stackoverflow.com/questions/44633419/no-access-permission-error-with-npm-global-install-on-docker-image
# The problem is because while NPM runs globally installed module scripts as 
# the nobody user, which kinds of makes sense, recent versions of NPM started 
# setting the file permissions for node modules to root. As a result module 
# scripts are no longer allowed to create files and directories in their module.
# A simple workaround, which makes sense in a docker environment, is to set 
# the NPM default global user back to root, like so:

RUN npm -g config set user root

RUN npm install -g openid-connect && \
    npm install -g --unsafe-perm node-red node-red-admin && \
    npm install -g node-red/node-red-auth-twitter && \
    npm install -g node-red/node-red-auth-github && \
    npm install -g node-red-dashboard

# Next line added due to segfault when authenticating to admin WUI
# https://stackoverflow.com/questions/45019750/docker-node-alpine-8-segmentation-fault-core-dumped
#RUN npm rebuild bcrypt --build-from-source

# Remove packages useless at runtime
RUN apk del libc-dev g++ make git

RUN /usr/sbin/addgroup -g 1234 nodered \ 
    && /usr/sbin/adduser -D -H -s /bin/nologin -u 1234 -G nodered nodered \
    && echo "nodered  ALL=(ALL) NOPASSWD: /usr/bin/python" >>/etc/sudoers

RUN if ! [ -d /vol1 ] ; then mkdir /vol1; chown root:nodered /vol1; chmod 770 /vol1; fi
VOLUME /vol1

USER nodered

# Next section to be updated in case image is run as a Swarm service to me monitored
# HEALTCHECK

# Define what to start by defaut when running the container
ENV NRPORT=7777

CMD /usr/bin/node-red -s ${LOCALSETTINGS} -p ${NRPORT} 


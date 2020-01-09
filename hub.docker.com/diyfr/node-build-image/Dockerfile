FROM alpine:3.9
RUN apk --no-cache add --virtual native-deps g++ gcc libgcc libstdc++ linux-headers make python tini nodejs nodejs-npm
# RUN which npm
RUN npm config set user 0 && npm config set unsafe-perm true

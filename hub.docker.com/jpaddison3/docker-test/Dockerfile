FROM node:boron

# Test an install of something, doesn't matter what it is
RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y software-properties-common

WORKDIR /root/project/
ADD . /root/project/

CMD ["node", "hello_world.js"]

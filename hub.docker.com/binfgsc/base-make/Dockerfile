################# BASE IMAGE ######################
FROM binfgsc/base:latest

################## METADATA #######################
LABEL base.image="binfgsc/base:latest"
LABEL about.summary="An image for compiling c++ programs on alpine linux"

################## MAINTAINER #####################
LABEL maintainer.name="William Hargreaves"
LABEL maintainer.email="whargrea@uoguelph.ca"

################# INSTALLATION ####################
# install the needed packages
RUN sudo apk add --no-cache \
    g++ \
    make \
    zlib-dev \
    python-dev \
    libpng-dev \
    freetype-dev \
    git

# # install a port of glibc
# RUN apk --no-cache add ca-certificates && \
#     wget -q -O /etc/apk/keys/sgerrand.rsa.pub https://alpine-pkgs.sgerrand.com/sgerrand.rsa.pub && \
#     wget https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.28-r0/glibc-2.28-r0.apk && \
#     apk add glibc-2.28-r0.apk
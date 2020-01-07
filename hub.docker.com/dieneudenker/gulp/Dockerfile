FROM node:12.3.1-alpine

# Install dependencies needed by some node libraries
RUN apk add --no-cache libtool=2.4.6-r5 
RUN apk add --no-cache automake=1.16.1-r0
RUN apk add --no-cache autoconf=2.69-r2
RUN apk add --no-cache nasm=2.13.03-r0
RUN apk add --no-cache gcc=8.3.0-r0
RUN apk add --no-cache make=4.2.1-r2
RUN apk add --no-cache g++=8.3.0-r0
RUN apk add --no-cache zlib-dev=1.2.11-r1
RUN apk add --no-cache openssh-client=7.9_p1-r5
RUN apk add --no-cache python=2.7.16-r1 python-dev=2.7.16-r1 python3=3.6.8-r2 python3-dev=3.6.8-r2
RUN apk add --no-cache git=2.20.1-r0

# Install bower and gulp
RUN npm install -g gulp@4.0.2 gulp-cli@2.2.0

# Add possibility to have only one ssh agent running, to be
# able to save ssh key passwords to use in multiple sessions
RUN mkdir /synced_ssh_agent
COPY run_ssh_agent.sh /synced_ssh_agent/

# Define working directory
WORKDIR /app
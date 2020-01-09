FROM node:6.11.2
LABEL NAME="MINUTZ-WEB BUILD IMAGE"
LABEL CLI-VERSION="2.3.1"
RUN useradd --user-group --create-home --shell /bin/false app
ENV HOME=/home/app
WORKDIR $HOME
RUN npm install -g @angular/cli \
&& npm install @angular/cli --save \
&& npm install @angular/compiler-cli --save
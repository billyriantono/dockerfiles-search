FROM paperist/alpine-texlive-ja:latest
RUN tlmgr update --self && \
  tlmgr install sourcecodepro ly1 mweights
RUN apk add --no-cache nodejs nodejs-npm git imagemagick
RUN npm install -g @paperist/cli

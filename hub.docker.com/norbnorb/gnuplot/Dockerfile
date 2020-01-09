FROM alpine
RUN apk add --update gnuplot
RUN apk add --update msttcorefonts-installer
RUN update-ms-fonts
RUN apk del msttcorefonts-installer
RUN apk add --update fontconfig 
RUN fc-cache -f
RUN apk del fontconfig
RUN rm -rf /var/cache/apk/*
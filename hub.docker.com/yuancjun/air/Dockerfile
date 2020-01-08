FROM golang:alpine
RUN apk add curl tzdata ca-certificates
RUN curl -fLo /bin/air https://raw.githubusercontent.com/cosmtrek/air/master/bin/linux/air
RUN chmod +x /bin/air

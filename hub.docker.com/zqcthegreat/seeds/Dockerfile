FROM golang:alpine
WORKDIR /go/src/app
COPY . .
RUN chmod a+x /go/src/app/enterpoint.sh
ENTRYPOINT ["/go/src/app/enterpoint.sh"]


#FROM alpine
#COPY seeds /bin/seeds
#RUN chmod 777 /bin/seeds
#ENTRYPOINT ["/bin/seeds"]

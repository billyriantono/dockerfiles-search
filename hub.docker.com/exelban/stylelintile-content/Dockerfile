FROM alpine
MAINTAINER Erica Windisch <erica@iopipe.com>
COPY . /home/iopipe-measure/
RUN apk add nodejs npm bash
RUN npm install -g serverless
ENTRYPOINT [ "/home/iopipe-measure/measure.sh" ]

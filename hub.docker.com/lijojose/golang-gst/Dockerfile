FROM lijojose/ubuntu-gst AS gobuilder

#RUN mkdir /app
WORKDIR /app

# COPY the source code as the last step
COPY . .

# Get dependancies - will also be cached if we won't change mod/sum
RUN go mod download

# Build the binary
RUN GOOS=linux GOARCH=amd64 go build -o /app/bin/tx /app/cmd/transcode/main.go

RUN mkdir /app/lib && ldd /app/bin/tx | grep "=> /" | awk '{print $3}' | xargs -I '{}' cp -v '{}' /app/lib/
RUN ldd /usr/lib/x86_64-linux-gnu/gstreamer-1.0/libgstvideotestsrc.so | grep "=> /" | awk '{print $3}' | xargs -I '{}' cp -v '{}' /app/lib/
RUN ldd /usr/lib/x86_64-linux-gnu/gstreamer-1.0/libgstvideoconvert.so | grep "=> /" | awk '{print $3}' | xargs -I '{}' cp -v '{}' /app/lib/
RUN ldd /usr/lib/x86_64-linux-gnu/gstreamer-1.0/libgstcoreelements.so | grep "=> /" | awk '{print $3}' | xargs -I '{}' cp -v '{}' /app/lib/

FROM ubuntu:18.04

RUN mkdir /app
RUN mkdir /app/bin
RUN mkdir /app/lib
RUN mkdir /app/gstlib

WORKDIR /app

COPY --from=gobuilder /app/bin ./bin/
COPY --from=gobuilder /app/lib ./lib/
COPY --from=gobuilder /usr/lib/x86_64-linux-gnu/gstreamer-1.0/libgstvideotestsrc.so ./gstlib/
COPY --from=gobuilder /usr/lib/x86_64-linux-gnu/gstreamer-1.0/libgstvideoconvert.so ./gstlib/
COPY --from=gobuilder /usr/lib/x86_64-linux-gnu/gstreamer-1.0/libgstcoreelements.so ./gstlib/
COPY --from=gobuilder /usr/bin/gst-inspect-1.0 ./bin/

ENV GST_PLUGIN_PATH "${GST_PLUGIN_PATH}:/app/gstlib/"
RUN ls -alSh 
RUN cp -rf lib/* /usr/lib/

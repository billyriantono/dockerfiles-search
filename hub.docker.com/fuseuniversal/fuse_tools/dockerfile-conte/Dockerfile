# usage: docker run funkypenguin/xmrig-cpu -o miningpool.url:port -u username -p password

FROM          alpine:3.7 as build

# BUILD_DATE and VCS_REF are immaterial, since this is a 2-stage build, but our build
# hook won't work unless we specify the args
ARG BUILD_DATE
ARG VCS_REF

ENV           XMRIG_DIR /xmrig-cpu
ENV           XMRIG_BUILD_DIR $XMRIG_DIR/build

RUN           apk --no-cache add build-base cmake curl git libuv-dev
# Use xmrig v2.4.2
RUN           git clone https://github.com/xmrig/xmrig.git $XMRIG_DIR && cd $XMRIG_DIR && \
 mkdir $XMRIG_BUILD_DIR && cd $XMRIG_BUILD_DIR && \
    cmake .. -DWITH_HTTPD=OFF && make
RUN           mv $XMRIG_BUILD_DIR/xmrig /usr/bin/

FROM          alpine:3.7

# Now we DO need these, for the auto-labeling of the image
ARG BUILD_DATE
ARG VCS_REF

# Good docker practice, plus we get microbadger badges
LABEL org.label-schema.build-date=$BUILD_DATE \
      org.label-schema.vcs-url="https://github.com/funkypenguin/xmrig-cpu-docker.git" \
      org.label-schema.vcs-ref=$VCS_REF \
      org.label-schema.schema-version="2.2-r1"
      
RUN           apk --no-cache add libuv-dev
COPY          --from=build /usr/bin/xmrig /usr/bin/
ENTRYPOINT    ["xmrig"]

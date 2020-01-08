FROM alpine:latest
RUN apk add mesa-gles mesa-egl chromium
RUN mkdir /usr/lib/chromium/swiftshader/ && cp /usr/lib/libGLESv2.so.2 /usr/lib/chromium/swiftshader/libGLESv2.so && cp /usr/lib/libEGL.so.1 /usr/lib/chromium/swiftshader/libEGL.so
WORKDIR /
CMD ["chromium-browser",  "--headless",  "--no-sandbox",  "--disable-gpu",  "--disable-software-rasterizer",  "--user-data-dir=/data", "--remote-debugging-address=0.0.0.0", "--remote-debugging-port=9222"]

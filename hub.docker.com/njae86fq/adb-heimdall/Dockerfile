FROM sorccu/adb as builder

RUN apk update
RUN apk add --no-cache libusb-dev libstdc++
RUN apk add --no-cache g++ make cmake git
RUN git clone https://gitlab.com/BenjaminDobell/Heimdall /Heimdall
WORKDIR /Heimdall
RUN git checkout a2cfdaa5ed3b95c2aa5cfcd754460109c14c37f2
RUN mkdir build
WORKDIR /Heimdall/build
RUN cmake -DCMAKE_BUILD_TYPE=Release -DDISABLE_FRONTEND=1 ..
RUN make


FROM sorccu/adb
RUN apk update
RUN apk add --no-cache libusb-dev libstdc++
COPY --from=builder /Heimdall/build/bin/* /usr/local/bin/

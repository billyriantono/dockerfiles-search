# djaydev/msi_klm:latest

FROM alpine AS builder
RUN apk add git libusb-dev build-base cargo

RUN git clone https://github.com/ruabmbua/msi_klm.git

RUN cd /msi_klm && cargo build --no-default-features --release

FROM alpine
RUN apk add --no-cache libusb libgcc \
    # cleanup
    && rm -rf /var/cache/apk/* /tmp/* /tmp/.[!.]*

COPY --from=builder /msi_klm/target/release/* /usr/local/bin/

CMD msi_klm -m OFF

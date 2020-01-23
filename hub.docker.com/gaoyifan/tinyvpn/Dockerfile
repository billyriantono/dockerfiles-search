FROM alpine:3.7 as builder
RUN apk add --no-cache build-base git linux-headers
RUN git clone --branch 20171125.0 --recurse-submodules https://github.com/wangyu-/tinyFecVPN.git /usr/local/src/tinyFecVPN
WORKDIR /usr/local/src/tinyFecVPN
ADD enable-forward.patch .
RUN git apply enable-forward.patch
RUN make
RUN strip tinyvpn

FROM scratch
COPY --from=builder /usr/local/src/tinyFecVPN/tinyvpn /
ENTRYPOINT ["/tinyvpn"]

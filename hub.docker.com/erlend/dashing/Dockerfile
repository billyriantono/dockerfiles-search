FROM golang
RUN go get -u github.com/technosophos/dashing

FROM scratch
COPY --from=0 /lib/x86_64-linux-gnu/libdl-2.24.so /lib/x86_64-linux-gnu/libdl-2.24.so
COPY --from=0 /lib/x86_64-linux-gnu/libdl.so.2 /lib/x86_64-linux-gnu/libdl.so.2
COPY --from=0 /lib/x86_64-linux-gnu/libpthread.so.0 /lib/x86_64-linux-gnu/libpthread.so.0
COPY --from=0 /lib/x86_64-linux-gnu/libpthread-2.24.so /lib/x86_64-linux-gnu/libpthread-2.24.so
COPY --from=0 /lib/x86_64-linux-gnu/libc.so.6 /lib/x86_64-linux-gnu/libc.so.6
COPY --from=0 /lib/x86_64-linux-gnu/libc-2.24.so /lib/x86_64-linux-gnu/libc-2.24.so
COPY --from=0 /lib64/ld-linux-x86-64.so.2 /lib64/ld-linux-x86-64.so.2
COPY --from=0 /lib/x86_64-linux-gnu/ld-2.24.so /lib/x86_64-linux-gnu/ld-2.24.so
COPY --from=0 /go/bin/dashing /
ENTRYPOINT ["/dashing"]

FROM alpine:3.6
RUN apk add --no-cache gcc libc-dev
COPY hello.c /
RUN gcc --static hello.c -o hello

FROM scratch
COPY --from=0 /hello .
CMD ["/hello"]

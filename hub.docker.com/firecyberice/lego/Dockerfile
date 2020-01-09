FROM scratch

ARG ARCH=amd64
COPY lego-${ARCH} /lego

COPY content /
EXPOSE 80 443
ENTRYPOINT ["/lego"]
CMD ["-h"]

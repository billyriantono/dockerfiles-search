FROM alpine AS base
COPY VERSION .
RUN mkdir context
COPY Setup.sh ./context
ENTRYPOINT ./context/Setup.sh
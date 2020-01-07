FROM hyperledger/fabric-ca:x86_64-1.0.5

FROM ruby:2.5-alpine
RUN apk add --no-cache bash
COPY --from=0 /usr/local/bin/fabric-ca-client /usr/local/bin

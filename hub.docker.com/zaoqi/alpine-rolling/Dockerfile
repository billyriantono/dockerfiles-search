FROM zaoqi/alpine-rolling
RUN apk upgrade --no-cache

FROM scratch
COPY --from=0 / /

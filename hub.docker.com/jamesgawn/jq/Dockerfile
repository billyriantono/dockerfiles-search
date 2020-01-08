FROM stedolan/jq as build

FROM scratch
COPY --from=build /usr/local/bin/jq /bin/jq

ENTRYPOINT ["/bin/jq"]
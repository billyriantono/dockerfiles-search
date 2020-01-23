FROM segment/chamber:2.7.5 as build

FROM datadog/agent:latest

COPY --from=build /chamber /chamber

ENTRYPOINT ["/chamber", "exec", "datadog", "datadog-agent", "--"]
CMD ["/init"]
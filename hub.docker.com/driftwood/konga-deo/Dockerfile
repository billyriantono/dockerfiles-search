FROM segment/chamber:2.7.5 as build

FROM pantsel/konga:next

EXPOSE 1337

COPY --from=build /chamber /chamber

ENTRYPOINT ["/chamber", "exec", "konga", "datadog", "--", "/app/start.sh"]


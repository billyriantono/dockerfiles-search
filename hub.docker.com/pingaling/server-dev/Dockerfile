FROM elixir:1.7 as development

ENV MIX_ENV dev
ENV PORT 4000

RUN mkdir /app
WORKDIR /app
COPY api/mix.exs .
COPY api/mix.lock .
COPY version.txt /app

RUN mix local.hex --force \
 && mix local.rebar --force \
 && mix deps.get

COPY api /app

EXPOSE 4000
CMD mix ecto.migrate && mix phx.server

FROM elixir:1.7 as production-build
ENV MIX_ENV prod
ENV PORT 4000

COPY --from=development /root/.mix /root/.mix
COPY --from=development /app /app
WORKDIR /app

RUN mix release

FROM erlang:21 as production
ENV MIX_ENV prod
ENV PORT 4000
EXPOSE 4000

RUN curl -sL -o /usr/local/bin/shush \
  https://github.com/realestate-com-au/shush/releases/download/v1.3.0/shush_linux_amd64 \
  && chmod +x /usr/local/bin/shush

COPY --from=production-build /app/_build/prod/rel/api /app
COPY version.txt /app

ENTRYPOINT ["/usr/local/bin/shush", "exec", "--"]
CMD /app/bin/api migrate && /app/bin/api foreground

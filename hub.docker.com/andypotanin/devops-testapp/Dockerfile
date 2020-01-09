FROM microsoft/aspnetcore-build
WORKDIR /app

ENV NODE_PORT 8080
ENV HEALTCHECK_HOST "localhost"
ENV SLACK_CHANNEL_URL ""

ADD app /app

EXPOSE 8080

## Check /info every 10s
#HEALTHCHECK --interval=5s --timeout=2s --start-period=5s --retries=2 CMD powershell -Command "./healthcheck.ps1; exit $LASTEXITCODE"


## Check /info every 10s
HEALTHCHECK --interval=10s --timeout=5s --start-period=30s --retries=2 \
  CMD powershell -command try {$response = iwr http://localhost:8080/ping -UseBasicParsing; if ( $response.StatusCode -eq 200) { return 0} else {return 1}; } catch { return 1 }

CMD [ "node", "server.js"]


##  docker build . --tag=testapp
##  docker run --rm testapp node



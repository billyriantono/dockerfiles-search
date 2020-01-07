FROM microsoft/dotnet:latest

LABEL Christian Sakshaug <christian@dx.no>

COPY /entrypoint.sh /
RUN mkdir /app && chmod +x /entrypoint.sh

WORKDIR /app

ENTRYPOINT [ "/entrypoint.sh" ] 
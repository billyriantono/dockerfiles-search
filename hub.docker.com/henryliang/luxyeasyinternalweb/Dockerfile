FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src

# set up node
ENV NODE_VERSION 10.15.1
ENV NODE_DOWNLOAD_SHA ca1dfa9790876409c8d9ecab7b4cdb93e3276cedfc64d56ef1a4ff1778a40214
RUN curl -SL "https://nodejs.org/dist/v${NODE_VERSION}/node-v${NODE_VERSION}-linux-x64.tar.gz" --output nodejs.tar.gz \
    && echo "$NODE_DOWNLOAD_SHA nodejs.tar.gz" | sha256sum -c - \
    && tar -xzf "nodejs.tar.gz" -C /usr/local --strip-components=1 \
    && rm nodejs.tar.gz \
    && ln -s /usr/local/bin/node /usr/local/bin/nodejs

COPY ["luxyeasy.internalweb/luxyeasy.internalweb.csproj", "luxyeasy.internalweb/"]
RUN dotnet restore "luxyeasy.internalweb/luxyeasy.internalweb.csproj"
COPY ./luxyeasy.internalweb ./luxyeasy.internalweb
WORKDIR "/src/luxyeasy.internalweb"
RUN dotnet build "luxyeasy.internalweb.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "luxyeasy.internalweb.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app ./
CMD ["dotnet", "luxyeasy.internalweb.dll"]
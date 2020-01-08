FROM microsoft/dotnet:2.2-sdk-alpine as sdk
COPY . .
RUN dotnet pack ./NuKeeper/NuKeeper.csproj -o "./artifacts"
FROM microsoft/dotnet:2.2-sdk-alpine as runtime
COPY --from=sdk ./NuKeeper/artifacts .
RUN dotnet tool install nukeeper --global --add-source .
ENV PATH="${PATH}:/root/.dotnet/tools"

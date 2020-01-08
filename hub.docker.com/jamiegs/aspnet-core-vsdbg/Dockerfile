
FROM microsoft/dotnet:2.1.0-aspnetcore-runtime-stretch-slim
# Install VSDBG for local run only.
RUN apt-get update \
    && apt-get install -y --no-install-recommends \
    unzip \
    && curl -sSL https://aka.ms/getvsdbgsh | bash /dev/stdin -v latest -l /vsdbg \
    && rm -rf /var/lib/apt/lists/*
FROM mcr.microsoft.com/dotnet/core/sdk:2.1.802-stretch
# .Net Core 2.1, VB 15.5

RUN set -ex; \
    useradd --create-home -u 9999 codewarrior; \
    mkdir /workspace; \
    chown -R codewarrior:codewarrior /workspace; \
    mkdir -p /opt/nuget/packages; \
    mkdir -p /opt/nuget/cache; \
    chmod -R o+rw /opt/nuget;

COPY rootfs/usr/local/bin/vbc /usr/local/bin/vbc
RUN chmod +x /usr/local/bin/vbc

USER codewarrior
ENV USER=codewarrior \
    HOME=/home/codewarrior \
    DOTNET_CLI_TELEMETRY_OPTOUT=1 \
    NUGET_PACKAGES=/opt/nuget/packages \
    NUGET_HTTP_CACHE_PATH=/opt/nuget/cache

COPY --chown=codewarrior:codewarrior rootfs/workspace/vb-run /workspace/vb-run
COPY --chown=codewarrior:codewarrior rootfs/workspace/vb-test /workspace/vb-test

RUN set -ex; \
    cd /workspace/vb-run; \
# get packages
    dotnet restore; \
# Use the following to extract list of references. Need to update `config.rsp` if packages are added.
#   dotnet run --verbosity normal; \
    dotnet build --no-restore; \
    rm -rf bin/Debug/netcoreapp2.1/run.pdb; \
    rm bin/Debug/netcoreapp2.1/run.dll; \
    rm -rf obj; \
    mkdir -p obj/Debug/netcoreapp2.1; \
    vbc @config.rsp Program.vb; \
    dotnet bin/Debug/netcoreapp2.1/run.dll; \
    rm Program.vb bin/Debug/netcoreapp2.1/run.dll;

RUN set -ex; \
    cd /workspace/vb-test; \
# get packages
    dotnet restore; \
# Use the following to extract list of references. Need to update `config.rsp` if packages are added.
#   dotnet run --verbosity normal; \
    dotnet build --no-restore; \
    rm -rf bin/Debug/netcoreapp2.1/test.pdb; \
    rm bin/Debug/netcoreapp2.1/test.dll; \
    rm -rf obj; \
    mkdir -p obj/Debug/netcoreapp2.1; \
    vbc @config.rsp Fixture.vb Program.vb Solution.vb; \
    dotnet bin/Debug/netcoreapp2.1/test.dll; \
    rm Fixture.vb Solution.vb bin/Debug/netcoreapp2.1/test.dll;

WORKDIR /workspace

# This image sets up some optimizations for our use case.
# `dotnet build` is only used during image build to generate some necessary files [0].
#
# - `{name}.deps.json`
#   - For dynamic linking, e.g, `Could not load file or assembly 'nunit.engine.netstandard'`
# - `{name}.runtimeconfig.dev.json`
#   - For specifying where to probe assemblies in `deps.json`.
#   - `An assembly specified in the application dependencies manifest (test.deps.json) was not found`
#   - Maybe `dotnet exec --additionalProbingPath /opt/nuget/packages` will also work
# - `{name}.runtimeconfig.json`
#   - For `A fatal error was encountered. The library 'libhostpolicy.dylib' required`
#
# List of references are extracted and stored in `config.rsp`.
# `config.rsp` must be updated when we add packages.
# When executing user's code, we use the compiler directly with these generated files for speed [4].
#
# References:
# .Net Core:
# [0]: https://natemcmaster.com/blog/2017/12/21/netcore-primitives/
# [1]: https://github.com/dotnet/cli/blob/v2.1.302/Documentation/specs/runtime-configuration-file.md
# [2]: https://github.com/dotnet/cli/blob/v2.1.302/Documentation/specs/corehost.md
# Roslyn:
# [3]: https://github.com/dotnet/roslyn/blob/Visual-Studio-2017-Version-15.7/docs/compilers/CSharp/CommandLine.md
# [4]: https://stackoverflow.com/q/46065777

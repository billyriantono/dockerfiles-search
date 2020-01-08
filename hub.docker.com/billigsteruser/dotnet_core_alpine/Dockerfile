FROM alpine:3.10.3

RUN apk add --no-cache \
	ca-certificates \
	\
	# .NET Core dependencies
	krb5-libs \
	libgcc \
	libintl \
	libssl1.1 \
	libstdc++ \
	zlib \
	icu-libs \
	git

# Disable the invariant mode (set in base image)
RUN apk add --no-cache 

ENV DOTNET_SYSTEM_GLOBALIZATION_INVARIANT=false \
    LC_ALL=en_US.UTF-8 \
    LANG=en_US.UTF-8 \
    DOTNET_CLI_TELEMETRY_OPTOUT=1

# Install .NET Core SDK
ENV DOTNET_SDK_VERSION 3.0.100

RUN wget -O dotnet.tar.gz https://dotnetcli.blob.core.windows.net/dotnet/Sdk/$DOTNET_SDK_VERSION/dotnet-sdk-$DOTNET_SDK_VERSION-linux-musl-x64.tar.gz \
    && dotnet_sha512='b2b42c7e33bdb492c7f25c615cfc57c9ca3222d4492d59829f2d683cb40a3d18d648195d21f4e519fd187f40d69e2977ccc3d993c5aefc5cb0a23cd496f344dc' \
    && echo "$dotnet_sha512  dotnet.tar.gz" | sha512sum -c - \
    && mkdir -p /usr/share/dotnet \
    && tar -C /usr/share/dotnet -xzf dotnet.tar.gz \
    && ln -s /usr/share/dotnet/dotnet /usr/bin/dotnet \
    && rm dotnet.tar.gz


	# Enable correct mode for dotnet watch (only mode supported in a container)
ENV DOTNET_USE_POLLING_FILE_WATCHER=true \
    # Skip extraction of XML docs - generally not useful within an image/container - helps performance
    NUGET_XMLDOC_MODE=skip

RUN mkdir -p /opt/dotnet_test
WORKDIR /opt/dotnet_test

# Trigger first run experience by running arbitrary cmd
	#Display .NET Core information.
RUN dotnet --info && \
	#Display the installed runtimes.       
	dotnet --list-runtimes  && \
	#Display the installed SDKs.  
	dotnet --list-sdks && \
	#Display .NET Core SDK version in use.
	dotnet --version && \
	# test build
	git clone https://github.com/ae2021/dotnet_core_ci_dummy.git . && \
	dotnet build && \
	dotnet run --project hello_world/hello_world.csproj && \
	cd .. && rm -rf dotnet_test

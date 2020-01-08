FROM codercom/code-server:v2 AS builder
RUN sudo apt-get update && \
	sudo apt-get install -y cmake && \
	git clone https://github.com/Samsung/netcoredbg/ ~/netcoredbg/ && \
	mkdir -p ~/netcoredbg/build/ && mkdir -p ~/netcoredbg/bin/ && \
	sudo apt-get install -y clang

WORKDIR /home/coder/netcoredbg/build/
RUN CC=clang CXX=clang++ cmake .. -DCMAKE_INSTALL_PREFIX=/home/coder/netcoredbg/bin && cmake --build . --target install

FROM codercom/code-server:v2
COPY --from=builder /home/coder/netcoredbg/bin/ /opt/netcoredbg/
RUN wget -q https://packages.microsoft.com/config/ubuntu/18.04/packages-microsoft-prod.deb -O packages-microsoft-prod.deb && \
	sudo dpkg -i packages-microsoft-prod.deb && \
	rm packages-microsoft-prod.deb && \
	sudo apt-get update && \
	sudo apt-get install -y --no-install-recommends apt-transport-https && \
	sudo apt-get update && \
	sudo apt-get install -y --no-install-recommends dotnet-sdk-3.0 && \
	sudo rm -rf /var/lib/apt/lists/* && \
	sudo mkdir -p /home/coder/.local/share/NuGet && \
	sudo chown -R coder:coder /home/coder/.local/share/NuGet && \
	sudo ln -s /opt/netcoredbg/netcoredbg /bin/netcoredbg
ENV DOTNET_CLI_TELEMETRY_OPTOUT 1

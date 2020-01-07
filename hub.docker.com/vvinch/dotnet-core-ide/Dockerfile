FROM microsoft/dotnet:sdk

# add a source for nodejs
RUN curl -sL https://deb.nodesource.com/setup_11.x | bash -

# Install required packages
RUN apt-get update && apt-get install -y nodejs wget libunwind8 libxkbfile1 libsecret-1-0 libnotify4 \
    libgconf-2-4 libnss3 libgtk2.0-0 libxss1 libgconf-2-4 libasound2 libxtst6 \
    libcanberra-gtk-dev libgl1-mesa-glx libgl1-mesa-dri \
    midori xdg-utils rsync

# Install visual studio code
RUN wget https://go.microsoft.com/fwlink/?LinkID=760868 -O vscode.deb && \
    dpkg -i vscode.deb; \
    rm vscode.deb && \
    rm -rf /var/lib/apt/lists/*

# Prepare volume for extensions
RUN mkdir /initial-extensions
VOLUME /extensions

# copy startup script
COPY launch.sh /launch.sh
RUN chmod +x /launch.sh

# Create vscode user
RUN useradd -m vscode -s /bin/bash
WORKDIR /dotnet

RUN chown vscode /extensions
RUN chown vscode /initial-extensions


USER vscode

# Install .NET Core plugins pack
RUN code --extensions-dir /initial-extensions --install-extension salbert.awesome-dotnetcore-pack

# Environment variables
ENV DISPLAY=:0.0
ENV VS_OPTIONS=""

CMD [ "/launch.sh" ]

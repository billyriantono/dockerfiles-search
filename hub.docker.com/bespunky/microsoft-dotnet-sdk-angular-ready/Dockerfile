FROM microsoft/dotnet:2.2-sdk

# Simply installing nodejs from apt-get doesn't install npm.
# Register NodeSource as a valid service for apt-get, then install nodejs from there.
RUN curl -sL https://deb.nodesource.com/setup_11.x | bash - \
 && apt-get install -yq nodejs

# Install Angular CLI globaly so 'ng' commands can be executed
RUN npm install -g @angular/cli

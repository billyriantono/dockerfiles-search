FROM microsoft/dotnet:2.1-sdk

# Install Chrome
RUN \
  apt-get update && \
  apt-get install -y wget xvfb && \
  wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb && \
  dpkg -i google-chrome-stable_current_amd64.deb; apt-get -fy install

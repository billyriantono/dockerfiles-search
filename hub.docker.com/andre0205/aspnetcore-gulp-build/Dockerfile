FROM microsoft/aspnetcore-build:2.0

# Install Node 6.X
RUN wget -O - https://deb.nodesource.com/setup_6.x | bash && apt-get install -y nodejs devscripts && apt-get clean

# Install Gulp globally

RUN npm install --global gulp-cli
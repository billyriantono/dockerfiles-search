FROM beevelop/nodejs-python-ruby

# Update packages, then install base ones.
RUN npm install npm -g
RUN apt-get update
RUN apt-get install -y apt-transport-https

# Register Yarn repository: https://yarnpkg.com/en/docs/install#debian-stable.
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -
RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list

# Update again and install Ruby modules.
RUN apt-get update
RUN apt-get install -y locales-all yarn
RUN pip install --upgrade pip
RUN gem install -N jekyll jekyll-relative-links jekyll-sitemap

# Clean up.
RUN apt-get clean
RUN rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# This is a build-only image, so no CMD.

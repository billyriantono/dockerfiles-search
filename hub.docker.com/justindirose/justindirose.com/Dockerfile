###################################################
# JUSTINDIROSE.COM
# justindirose.com config
# An image built off nginx-jekyll with a test site.
###################################################

# Base Image
FROM justindirose/nginx-jekyll

# File Author / Maintainer
MAINTAINER Justin DiRose desk@justindirose.com

# Add virtual host config
COPY nginx/justindirose.com /etc/nginx/sites-available/justindirose.com
RUN ln -s /etc/nginx/sites-available/justindirose.com /etc/nginx/sites-enabled/justindirose.com

# Set up Jekyll
RUN mkdir /srv/jekyll
COPY . /srv/jekyll

# Build Jekyll
WORKDIR /srv/jekyll
RUN bundle install
RUN bundle exec jekyll build --source /srv/jekyll --destination /usr/share/nginx/html

# ENV/EXPOSE
EXPOSE 80

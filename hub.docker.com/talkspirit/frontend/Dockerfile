FROM node:12.14.0-buster

# to build package
RUN echo "\n# Gemfile\nsource \"https://rubygems.org\"\ngem \"fastlane\"" > /home/node/Gemfile && \
    apt-get update && apt-get install -y build-essential debhelper devscripts vim curl && \
    # cypress \
    apt-get install -y xvfb libgtk2.0-0 libnotify-dev libgconf-2-4 libnss3 libxss1 libasound2 && \
    # fastlane \
    apt-get install -y ruby-full && \
    cd /home/node && gem install bundler && bundle update && \
    npm install -g expo-cli --unsafe-perm

ADD entrypoint.sh /entrypoint.sh
RUN chown node.node /entrypoint.sh

ENTRYPOINT ["sh", "/entrypoint.sh"]
CMD ["bash"]

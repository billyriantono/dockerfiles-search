FROM swift:4.2.2

LABEL maintainer "Henry Huang"
MAINTAINER Henry Huang "https://github.com/henry2423"
ENV REFRESHED_AT 2019-02-07

# Important: Credential Key
ENV OauthToken="Put Your OAuth Access Token Here"
ENV OauthBotToken="Put Your Bot User OAuth Access Token Here"
ENV VerficationToken="Put Your App Verification Token Here"
ENV mongoDBURL="Put You MongoDB URL Here (with credential key)"

ENV HOME=/home

ADD ./ $HOME/
RUN cd $HOME/ && swift build -c release

# Expose SlackServer 
EXPOSE 8080

CMD ["/bin/bash", "-c", "/home/.build/release/TeamAssistantBot"]
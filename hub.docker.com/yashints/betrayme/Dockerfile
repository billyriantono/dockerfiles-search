FROM zricethezav/gitleaks

LABEL "name"="BetrayMe"
LABEL "maintainer"="Yaser Adel Mehraban <me@yashints.dev>"
LABEL "version"="1.0.0"

LABEL "com.github.actions.name"="BetrayMe"
LABEL "com.github.actions.description"="Uses gitleaks to scan for any secrets in your code"
LABEL "com.github.actions.icon"="shield"
LABEL "com.github.actions.color"="green"

COPY entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh

ENTRYPOINT ["bash", "/entrypoint.sh"]
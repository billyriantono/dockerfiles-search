FROM sipcapture/homer-webapp:latest

ENV DEBIAN_FRONTEND noninteractive

# Install mysqlnd so we can control the read_timeout
RUN apt update -qq && apt install -y php5-mysqlnd

# Configure the mysqlnd read timeout
RUN sed -r -i.bak 's/^;(mysqlnd.net_read_timeout)\s*=\s*[0-9]+/\1 = 270/' /etc/php5/apache2/php.ini

# Increase the height on the 'DB Nodes' list box
RUN sed -r -i.bak 's/height:61px;(width:100%;.*tr\.name for tr in db_node track)/height:183px;\1/' /var/www/html/js/widgets/quicksearch/quicksearch.html

# Jump to the search page after login
RUN sed -r -i.bak 's|(if\(path == "/login".*)\$location\.path\(homer\.modules\.pages\.routes\.home\);\s*$|\1$location.path(homer.modules.pages.routes.search);|' /var/www/html/js/modules/auth/module.auth.run.js

# Jump to the search page if already logged in
RUN sed -r -i.bak 's/\$urlRouterProvider\.otherwise\(homer\.modules\.pages\.routes\.home\);\s*$/$urlRouterProvider.otherwise(homer.modules.pages.routes.search);/' /var/www/html/js/modules/auth/module.auth.routes.js

# Jump to the search page from the root URL           
RUN sed -r -i.bak 's/\$location\.path\(homer\.modules\.pages\.routes\.home\);\s*$/$location.path(homer.modules.pages.routes.search);/' /var/www/html/js/modules/auth/controllers/loginCtrl.js

# Add persistent volumes
VOLUME ["/var/www/html/store"]

# UI
EXPOSE 80

ENTRYPOINT ["/run.sh"]

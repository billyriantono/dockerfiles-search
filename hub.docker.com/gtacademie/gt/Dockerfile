FROM camptocamp/odoo-project:11.0-2.5.1
MAINTAINER Camptocamp

# Install additional debian packages if needed
RUN set -x; \
         apt-get update \
         && apt-get install -y --no-install-recommends \
         parallel \
         # dependency of website_multi_theme
         ruby-sass \
         && apt-get clean \
         && rm -rf /var/lib/apt/lists/*


ENV ADDONS_PATH="/opt/odoo/local-src, \
/opt/odoo/src/addons, \
/opt/odoo/external-src/account-financial-tools, \
/opt/odoo/external-src/account-financial-reporting, \
/opt/odoo/external-src/server-env, \
/opt/odoo/external-src/bank-payment, \
/opt/odoo/external-src/partner-contact, \
/opt/odoo/external-src/server-ux, \
/opt/odoo/external-src/reporting-engine, \
/opt/odoo/external-src/web, \  
/opt/odoo/external-src/l10n-switzerland, \
/opt/odoo/external-src/website," \

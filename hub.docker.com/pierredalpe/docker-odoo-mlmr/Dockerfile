FROM odoo:8.0 

MAINTAINER Benoît "XtremXpert" Vézina <xtremxpert@xtremxpert.com> 

# L'usager por défaut est odoo, passons donc a l'usager root
USER root 

# Copions les fichiers nécessaires (minimal)
# 1- clé ssh de déploiement
COPY rootfs /

# Variable d'environnement pour utiliser avec le contexte
# ainsi que par ls petit script python envtpl
#ENV 	OPENERP_SERVER='/etc/odoo/openerp-server.conf' \
#	PGHOST='db' \
#        PGUSER='ReivaPGUser' \
#        PGPSWD='ReivaPGPass' \
#        DBADMPASS='R3!v4P4ss' \
#        DBNAME='dbname' \
#        DBFILTER='dbfilter' \
#        VERSION='1.9-github' \
#	ODOO_VERSION='8.0' \
#	ODOO_RELEASE='20161018'

# On commence par installer ce qui manque a Odoo pour rouler 
# Clean Css, l'installateur pip, nodejs et git.  Le fichier
# récupéré avec Curl modifie les depots pour nodejs.
# On va aussi tout mettre à jours
RUN	curl https://www.postgresql.org/media/keys/ACCC4CF8.asc | apt-key add - && \
	apt-get update && \
	curl -sL https://deb.nodesource.com/setup_4.x | bash - && \
	apt-get dist-upgrade -y && \
	apt-get install -y \
		build-essential \
		git \
#		libffi \
		libffi-dev \
                libssl-dev \
		nodejs \
		python-dev && \



# Injection de git.portall.ca dans known_host
# -- on ne peux pas aacepter le certificat
# -- lors du git clone qui suit
	chmod 600 /root/.ssh/id_rsa && \
	chown -R odoo:odoo /etc/odoo && \
	chmod +x /entrypoint.sh && \
	ssh-keyscan git.portall.ca > /root/.ssh/known_hosts
# Ajout par pip de envtpl pour pouvoir l'utilsier pour
# remplacer des valeurs dans les fichiers de config 
# par des variables d'environnement (entrypoint)
RUN	pip install \
		envtpl \
		num2words \
		phonenumbers \
		pysftp \
            	pymysql \
            	soappy && \

# Installation de clean-css via node-js
	npm install -g less less-plugin-clean-css

# En une linge, création de notre dossier de addons et 
# clonage des modules sur le git.  On utilise un autre 
# répetoire que /mnt/extra-addons car il a été déclaré
# comme volume dans l'image d'origin et et tout changements
# fait à partir de l'environnement docker est ignoré 
# après sa déclaration.  Il faur donc aussi modifier 
# le fichier /etc/odoo/openerp-server.conf
# Adding some OCA stuff
# ADDED FOR DEBUGING AND CREATE QUICKER COMPILE BUT BIGGER IMAGES
RUN	mkdir /tmp/OCA /mnt/docker-addons \
	&& cd /tmp/OCA \

# Link to refund to invoice
	&& git clone -b 8.0 https://github.com/OCA/l10n-spain.git  \
	&& mv /tmp/OCA/l10n-spain/account_refund_original  /mnt/docker-addons/ \

# For changing taxes on commun rules
	&& git clone -b 8.0 https://github.com/OCA/account-fiscal-rule.git  \
	&& mv /tmp/OCA/account-fiscal-rule/account_fiscal_position_rule  /mnt/docker-addons/  \
	&& mv /tmp/OCA/account-fiscal-rule/account_fiscal_position_rule_purchase  /mnt/docker-addons/  \
	&& mv /tmp/OCA/account-fiscal-rule/account_fiscal_position_rule_sale  /mnt/docker-addons/  \
	&& mv /tmp/OCA/account-fiscal-rule/account_fiscal_position_rule_stock  /mnt/docker-addons/  \

# RMA Stuff for return
	&& git clone -b 8.0 https://github.com/OCA/rma.git \
	&& mv /tmp/OCA/rma/product_warranty /mnt/docker-addons/ \
	&& mv /tmp/OCA/rma/crm_claim_rma /mnt/docker-addons/ \
	&& mv /tmp/OCA/rma/crm_claim_rma_code /mnt/docker-addons/ \

# Stuff from CRM (dependencies for RMA)
	&& git clone -b 8.0 https://github.com/OCA/crm.git \
	&& mv /tmp/OCA/crm/crm_claim_code /mnt/docker-addons/ \
	&& mv /tmp/OCA/crm/crm_claim_type /mnt/docker-addons/ \

# Some E-commerce add-ons
	&& git clone -b 8.0 https://github.com/OCA/e-commerce.git \
#	&& mv /tmp/OCA/e-commerce/website_sale_require_login /mnt/docker-addons/ \
	&& mv /tmp/OCA/e-commerce/website_sale_suggest_create_account /mnt/docker-addons/ \

# Some Website addons
	&& git clone -b 8.0 https://github.com/OCA/website.git \
	&& mv /tmp/OCA/website/website_menu_by_user_status /mnt/docker-addons/ \
#	&& mv /tmp/OCA/website/website_portal /mnt/docker-addons/ \
#	&& mv /tmp/OCA/website/website_portal_sale /mnt/docker-addons/ \

# To standardize phone number ???
#	&& git clone -b 8.0 http://gitlab.opengest.solutions/OCA/connector-telephony.git \
#	&& mv /tmp/OCA/connector-telephony/base_phone /mnt/docker-addons/ \

# More field for Parnter
	&& git clone -b 8.0 https://github.com/OCA/partner-contact.git \
	&& mv /tmp/OCA/partner-contact/base_location /mnt/docker-addons/ \
	&& mv /tmp/OCA/partner-contact/partner_contact_birthdate /mnt/docker-addons/ \
	&& mv /tmp/OCA/partner-contact/partner_firstname /mnt/docker-addons/ \
	&& mv /tmp/OCA/partner-contact/partner_contact_gender /mnt/docker-addons/ \
	&& mv /tmp/OCA/partner-contact/partner_second_lastname /mnt/docker-addons/ \
	&& mv /tmp/OCA/partner-contact/partner_contact_personal_information_page /mnt/docker-addons/ \

# Some server-tools
	&& git clone -b 8.0 https://github.com/OCA/server-tools.git \
	&& mv /tmp/OCA/server-tools/auditlog /mnt/docker-addons/ \
	&& mv /tmp/OCA/server-tools/auto_backup /mnt/docker-addons/ \
	&& mv /tmp/OCA/server-tools/web_context_tunnel /mnt/docker-addons/ \

# Some change in membership
	&& git clone -b 8.0 https://github.com/OCA/vertical-association.git \
	&& mv /tmp/OCA/vertical-association/membership_extension /mnt/docker-addons/ \
	&& mv /tmp/OCA/vertical-association/membership_variable_period /mnt/docker-addons/ \

# Canada localization
	&& git clone -b 8.0 https://github.com/OCA/l10n-canada.git \
	&& mv /tmp/OCA/l10n-canada/res_partner_attributes_add_BN /mnt/docker-addons/ \
	&& mv /tmp/OCA/l10n-canada/res_partner_attributes_add_NEQ /mnt/docker-addons/ \
	&& mv /tmp/OCA/l10n-canada/res_partner_attributes_add_SIN /mnt/docker-addons/ \
	&& mv /tmp/OCA/l10n-canada/l10n_ca_qc_account_fiscal_position_rule /mnt/docker-addons/  \
	&& mv /tmp/OCA/l10n-canada/l10n_ca_toponyms /mnt/docker-addons/ \

# Add stuff that can not be get on other source from our own Git

	&& cd /mnt/docker-addons \
#        && git clone -b 8.0 git@git.portall.ca:Portall/base_phone.git \
        && git clone -b 8.0 git@git.portall.ca:Portall/checkout_term_and_condition.git \
#        && git clone -b 8.0 git@git.portall.ca:Portall/entrepro_delivery_carrier.git \
#        && git clone -b 8.0 git@git.portall.ca:reiva/membership_reiva.git \
        && git clone -b 8.0 git@git.portall.ca:Portall/odoo_shipping_service_apps.git \
#        && git clone -b 8.0 git@git.portall.ca:Portall/payment_moneris.git \
#        && git clone -b 8.0 git@git.portall.ca:Portall/payment_optimalpayments.git \
        && git clone -b 8.0 git@git.portall.ca:Portall/product_bundle.git \
#        && git clone -b 8.0 git@git.portall.ca:reiva/products_reiva.git \
        && git clone -b 8.0 git@git.portall.ca:reiva/reiva_frontpage.git \
        && git clone -b 8.0 git@git.portall.ca:Portall/sale_automatic_workflow.git \
        && git clone -b 8.0 git@git.portall.ca:Portall/sale_payment_method.git \
        && git clone -b 8.0 git@git.portall.ca:Portall/sale_payment_method_automatic_workflow.git \
        && git clone -b 8.0 git@git.portall.ca:Portall/snippet_latest_posts.git \
        && git clone -b 8.0 git@git.portall.ca:Portall/taxes_reiva.git \
        && git clone -b 8.0 git@git.portall.ca:Portall/theme_common.git \
        && git clone -b 8.0 git@git.portall.ca:Portall/theme_enark.git \
#        && git clone -b 8.0 git@git.portall.ca:reiva/theme_reiva.git \
        && git clone -b 8.0 git@git.portall.ca:reiva/snippet_google_map.git \
        && git clone -b 8.0 git@git.portall.ca:Portall/website_animate.git \
        && git clone -b 8.0 git@git.portall.ca:Portall/website_custom_pricelist.git \
        && git clone -b 8.0 git@git.portall.ca:Portall/website_less.git \
#        && git clone -b 8.0 git@git.portall.ca:Portall/website_sale_available.git \
#        && git clone -b 8.0 git@git.portall.ca:Portall/website_portal_sale.git \
        && git clone -b 8.0 git@git.portall.ca:Portall/website_sale_require_login.git \
        && git clone -b 8.0 git@git.portall.ca:Portall/website_sale_payment_method_automatic_workflow.git \
        && git clone -b 8.0 git@git.portall.ca:Portall/website_webkul_addons.git \
        && git clone -b 8.0 git@git.portall.ca:Portall/website_sale_clear_cart.git \
        && git clone -b 8.0 git@git.portall.ca:Portall/wk_wizard_messages.git \

# Use the odoo config file from the rootfs
	&& mv /etc/odoo/openerp-server.conf /etc/odoo/openerp-server.conf.deb \
	&& mv /etc/odoo/openerp-server.conf.docker /etc/odoo/openerp-server.conf \

# Mount /var/lib/odoo to allow restoring filestore and /mnt/extra-addons for users addons
	&& mkdir -p /mnt/extra-addons \
        && chown -R odoo /mnt/extra-addons /etc/odoo \

# Some clean up
        && apt-get purge -y --auto-remove -o APT::AutoRemove::RecommendsImportant=false -o APT::AutoRemove::SuggestsImportant=false npm \
        && rm -rf /var/lib/apt/lists/* odoo.deb wkhtmltox.deb

USER odoo 

# Declaration des volumes docker-addons & /etc/odoo
# Mais c'est probablement inutile dans le cadre du
# serveur de production puisque 100% de modif devraient
# provenir du docker.  Seul les serveur de Dev en ont besoin
VOLUME ["/mnt/docker-addons", "/etc/odoo", "/var/lib/odoo", "/mnt/extra-addons"]

# Peut être inutile
ENTRYPOINT ["/entrypoint.sh"]
CMD ["openerp-server"]

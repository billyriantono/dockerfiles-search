FROM flexberry/mono-ember as backendAndApp

ENV PROJECT=EmberFlexberry

ARG TAG=1.0.0-beta01-application

RUN	git clone --depth=50 --branch=$TAG https://github.com/akosinsky/FlexberryEmberTestStand.ODataBackend /backend-src && \
	cd /backend-src/$PROJECT ; \
	nuget restore $PROJECT.sln ; \
	msbuild /p:Configuration=Release $PROJECT.sln ; \
	cd /backend-src/ember-app ; \
	echo "#ember init" ; \
	ember init ; \
	echo "#npm install" ; \
	npm install ; \
	echo "#bower install  --allow-root" ; \
	bower install  --allow-root ; \
	echo "#ember install ember-flexberry@2.0.0" ; \
	ember install ember-flexberry@2.0.0 ; \
	echo "#npm install" ; \
	npm install ; \
	echo "#bower install  --allow-root" ; \
	bower install  --allow-root ; \
	echo "#mv app app-save" ; \
	mv app app-save ; \
	echo "#mv public public-save" ; \
	mv public public-save ; \
	echo "#mv tests tests-save" ; \
	mv tests tests-save ; \
	echo "#mv vendor/fonts vendor/fonts-save" ; \
	mv vendor/fonts vendor/fonts-save ; \
	echo "#mv vendor/serviceImages vendor/serviceImages-save" ; \
	mv vendor/serviceImages vendor/serviceImages-save ; \
	echo "#ember generate flexberry-application app --metadata-dir=vendor/flexberry" ; \
	ember generate flexberry-application app --metadata-dir=vendor/flexberry ; \
	cp -rvf app/* app-save/ ; \
	cp -rvf public/* public-save/ ; \
	cp -rvf tests/* tests-save/ ; \
	cp -rvf vendor/fonts/* vendor/fonts-save/ ; \
	cp -rvf vendor/serviceImages/* vendor/serviceImages-save/ ; \
	cp -rvf app-save/* app/ ; \
	cp -rvf public-save/ public/ ; \
	cp -rvf tests-save/* tests/ ; \
	cp -rvf vendor/fonts-save/* vendor/fonts/ ; \
	cp -rvf vendor/serviceImages-save/* vendor/serviceImages/ ; \
	echo "#ember build" ; \
	ember build ; \
	echo done

FROM flexberry/alt.p8-apache2-mono:latest

RUN	rm -r /var/www/vhosts/test

COPY --from=backendAndApp /backend-src/EmberFlexberry/ODataBackend /var/www/vhosts/test
COPY --from=backendAndApp /backend-src/ember-app/dist /var/www/vhosts/test
COPY vhosts.conf /conf

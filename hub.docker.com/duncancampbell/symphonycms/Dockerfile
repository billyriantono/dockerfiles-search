FROM duncancampbell/apache-php-xsl-mysql

RUN apt-get update && apt-get install -y git
RUN git clone git://github.com/symphonycms/symphony-2.git /var/www/html/symphonycms  && chown -R www-data:www-data * 

RUN git clone https://github.com/symphonycms/markdown.git /var/www/html/symphonycms/extensions/markdown
RUN git clone https://github.com/symphonycms/maintenance_mode.git /var/www/html/symphonycms/extensions/maintenance_mode
RUN git clone https://github.com/symphonycms/selectbox_link_field.git /var/www/html/symphonycms/extensions/selectbox_link_field
RUN git clone https://github.com/symphonycms/jit_image_manipulation.git -b 1.x /var/www/html/symphonycms/extensions/jit_image_manipulation
RUN git clone https://github.com/symphonycms/export_ensemble.git /var/www/html/symphonycms/extensions/export_ensemble
RUN git clone https://github.com/symphonycms/debugdevkit.git /var/www/html/symphonycms/extensions/debugdevkit
RUN git clone https://github.com/symphonycms/profiledevkit.git /var/www/html/symphonycms/extensions/profiledevkit
RUN git clone https://github.com/symphonycms/xssfilter.git /var/www/html/symphonycms/extensions/xssfilter
RUN git clone https://github.com/symphonycms/members.git /var/www/html/symphonycms/extensions/members
RUN git clone https://github.com/symphonycms/numberfield.git /var/www/html/symphonycms/extensions/numberfield
RUN git clone https://github.com/symphonists/association_field.git /var/www/html/symphonycms/extensions/association_field
RUN git clone https://github.com/animaux/association_ui_selector_materie.git /var/www/html/symphonycms/extensions/association_ui_selector_materie
RUN git clone https://github.com/animaux/association_ui_editor_materie.git /var/www/html/symphonycms/extensions/association_ui_editor_materie
RUN git clone https://github.com/Solutions-Nitriques/image_preview.git /var/www/html/symphonycms/extensions/image_preview
RUN git clone https://github.com/klaftertief/imagecropper.git /var/www/html/symphonycms/extensions/imagecropper
RUN git clone https://github.com/symphonists/image_index_preview.git /var/www/html/symphonycms/extensions/image_index_preview
RUN git clone https://github.com/symphonists/reflectionfield.git /var/www/html/symphonycms/extensions/reflectionfield
RUN git clone https://github.com/twiro/reflecteduploadfield.git /var/www/html/symphonycms/extensions/reflecteduploadfield
RUN git clone https://github.com/symphonists/richtext_tinymce.git /var/www/html/symphonycms/extensions/richtext_tinymce


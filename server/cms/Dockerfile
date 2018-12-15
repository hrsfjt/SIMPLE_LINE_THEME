FROM php:7-apache

# Init server environments
RUN apt-get update
RUN apt-get install -y curl unzip libpng12-dev libjpeg-dev libfreetype6-dev libjpeg62-turbo-dev libmcrypt-dev
RUN rm -rf /var/lib/apt/lists/*
RUN docker-php-ext-configure gd --with-png-dir=/usr --with-jpeg-dir=/usr
RUN docker-php-ext-install gd mysqli opcache pdo_mysql mbstring iconv mcrypt
RUN a2enmod rewrite expires

# Wordpress Core Files
ENV WORDPRESS_VERSION 4.9.8
RUN curl -o wordpress.tar.gz -fSL "https://ja.wordpress.org/wordpress-${WORDPRESS_VERSION}-ja.tar.gz"
RUN tar -xzf wordpress.tar.gz
RUN rm wordpress.tar.gz
RUN mv /var/www/html/wordpress /var/www/html/cms
RUN chown -R www-data:www-data /var/www/html/cms

ENV BREADCRUMB_NAVXT_VERSION 6.1.0
RUN curl -o breadcrumb-navxt.zip -fSL "https://downloads.wordpress.org/plugin/breadcrumb-navxt.${BREADCRUMB_NAVXT_VERSION}.zip"
RUN unzip breadcrumb-navxt.zip
RUN cp -r breadcrumb-navxt /var/www/html/cms/wp-content/plugins/
RUN rm -rf breadcrumb-navxt/
RUN rm breadcrumb-navxt.zip

ENV AKISMET_ANTI_SPAM_VERSION 4.0.8
RUN curl -o akismet.zip -fSL "https://downloads.wordpress.org/plugin/akismet.${AKISMET_ANTI_SPAM_VERSION}.zip"
RUN unzip akismet.zip
RUN cp -r akismet /var/www/html/cms/wp-content/plugins/
RUN rm -rf akismet/
RUN rm akismet.zip

ENV BACK_WP_UP_VERSION 3.6.0
RUN curl -o backwpup.zip -fSL "https://downloads.wordpress.org/plugin/backwpup.${BACK_WP_UP_VERSION}.zip"
RUN unzip backwpup.zip
RUN cp -r backwpup /var/www/html/cms/wp-content/plugins/
RUN rm -rf backwpup/
RUN rm backwpup.zip

ENV GOOGLE_XML_SITEMAPS_VERSION 4.0.9
RUN curl -o google-sitemap-generator.zip -fSL "https://downloads.wordpress.org/plugin/google-sitemap-generator.${GOOGLE_XML_SITEMAPS_VERSION}.zip"
RUN unzip google-sitemap-generator.zip
RUN cp -r google-sitemap-generator /var/www/html/cms/wp-content/plugins/
RUN rm -rf google-sitemap-generator/
RUN rm google-sitemap-generator.zip

ENV WP_MULTIBYTE_PATCH_VERSION 2.8.1
RUN curl -o wp-multibyte-patch.zip -fSL "https://downloads.wordpress.org/plugin/wp-multibyte-patch.${WP_MULTIBYTE_PATCH_VERSION}.zip"
RUN unzip wp-multibyte-patch.zip
RUN cp -r wp-multibyte-patch /var/www/html/cms/wp-content/plugins/
RUN rm -rf wp-multibyte-patch/
RUN rm wp-multibyte-patch.zip

ENV CONTACT_FORM_VERSION 5.0.4
RUN curl -o contact-form-7.zip -fSL "https://downloads.wordpress.org/plugin/contact-form-7.${CONTACT_FORM_VERSION}.zip"
RUN unzip contact-form-7.zip
RUN cp -r contact-form-7 /var/www/html/cms/wp-content/plugins/
RUN rm -rf contact-form-7/
RUN rm contact-form-7.zip

# Copy index/access files
COPY index.php /var/www/html/index.php
COPY .htaccess /var/www/html/.htaccess

# Change owner
RUN chown www-data. /var/www/html/index.php
RUN chown www-data. /var/www/html/.htaccess

RUN usermod -u 1000 www-data && groupmod -g 1000 www-data
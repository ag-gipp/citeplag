# Image to run Citeplag Frontend in a single docker instance.
# A msql/maria db instance for the pmc oas files is still needed.
FROM php:5.6-fpm
LABEL maintainer="vincent.stange@uni-konstanz.de"

# Expose the port nginx is reachable on
EXPOSE 80

# We want to run php5 fpm plus a nginx to properly use it in a single instance
# Supervisor will execute both services properly
RUN apt-get update && apt-get install -y nginx supervisor curl

# Configure nginx
COPY config/citeplag.conf /etc/nginx/conf.d/default.conf

# Configure PHP-FPM
COPY config/fpm-pool.conf /usr/local/etc/php-fpm.d/www.conf
#COPY config/php.ini /etc/php7/conf.d/zzz_custom.ini

# Configure supervisord
COPY config/supervisord.conf /etc/supervisor/conf.d/supervisord.conf

# Copy frontend files
COPY . /app

# Let supervisord start nginx & php-fpm
CMD ["/usr/bin/supervisord", "-c", "/etc/supervisor/conf.d/supervisord.conf"]
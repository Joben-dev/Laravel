# Use an official PHP image with Composer and Nginx installed
FROM php:8.1-fpm

# Install system dependencies
RUN apt-get update && apt-get install -y \
    libpng-dev \
    libjpeg-dev \
    libfreetype6-dev \
    libonig-dev \
    libxml2-dev \
    zip \
    unzip \
    curl \
    nginx \
    supervisor

# Install PHP extensions
RUN docker-php-ext-install pdo_mysql mbstring exif pcntl bcmath gd

# Install Composer
COPY --from=composer:2.5 /usr/bin/composer /usr/bin/composer

# Set working directory
WORKDIR /var/www/html

# Copy application files
COPY . .

# Set permissions
RUN chown -R www-data:www-data /var/www/html/storage /var/www/html/bootstrap/cache

# Expose port 80 for Nginx
EXPOSE 80

# Create a supervisor configuration file for PHP-FPM and Nginx
RUN echo '[supervisord]\nnodaemon=true\n\n' \
    '[program:php-fpm]\ncommand=/usr/local/sbin/php-fpm\n\n' \
    '[program:nginx]\ncommand=/usr/sbin/nginx -g "daemon off;"\n\n' \
    > /etc/supervisor/supervisord.conf

# Start Supervisor (which runs PHP-FPM and Nginx)
CMD ["supervisord", "-c", "/etc/supervisor/supervisord.conf"]

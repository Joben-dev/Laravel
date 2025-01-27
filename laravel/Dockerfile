FROM php:8.0-fpm

# Install system dependencies
RUN apt-get update && apt-get install -y libpng-dev libjpeg-dev libfreetype6-dev zip git curl

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Set the working directory
WORKDIR /var/www

# Copy project files into the container
COPY . .

# Install PHP dependencies using Composer
RUN composer install

# Expose port 80
EXPOSE 80

# Command to run the app
CMD ["php", "-S", "0.0.0.0:80", "-t", "api"]

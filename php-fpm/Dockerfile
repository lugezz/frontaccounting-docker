FROM php:8.3-fpm

# Update package lists and install required dependencies
RUN apt-get update && apt-get install -y \
    libmemcached-dev \
    pkg-config \
    libssl-dev \
    libxml2-dev \
    libicu-dev \
    libmcrypt-dev \
    default-libmysqlclient-dev \
    && docker-php-ext-install mysqli pdo pdo_mysql

# Install the memcached extension separately
RUN pecl install memcached \
    && docker-php-ext-enable memcached

# Clean up
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

# Set the working directory
WORKDIR /var/www/html

# Copy your application code into the container
COPY . /var/www/html

# Expose port 80 to the outside world
EXPOSE 80

# Start Nginx service
CMD ["nginx", "-g", "daemon off;"]
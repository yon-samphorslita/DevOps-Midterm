FROM jenkins/jenkins:lts

# Set non-interactive mode for apt
ENV DEBIAN_FRONTEND=noninteractive

# Switch to root user to perform apt-get commands
USER root

# Install necessary dependencies and add Sury PHP repository
RUN apt update && \
    apt install -y curl gnupg lsb-release ca-certificates && \
    curl -sSL https://packages.sury.org/php/README.txt | bash -x && \
    apt update && \
    apt install -y php8.4 php8.4-xml php8.4-mbstring php8.4-curl npm php-zip

# Install Composer
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \
    php -r "if (hash_file('sha384', 'composer-setup.php') === 'dac665fdc30fdd8ec78b38b9800061b4150413ff2e3b6f88543c636f7cd84f6db9189d43a81e5503cda447da73c7e5b6') { echo 'Installer verified'.PHP_EOL; } else { echo 'Installer corrupt'.PHP_EOL; unlink('composer-setup.php'); exit(1); }" && \
    php composer-setup.php && \
    php -r "unlink('composer-setup.php');" && \
    mv composer.phar /usr/local/bin/composer

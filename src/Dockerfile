# See here for image contents: https://github.com/microsoft/vscode-dev-containers/tree/v0.191.1/containers/debian/.devcontainer/base.Dockerfile

# [Choice] Debian version: bullseye, buster, stretch
ARG VARIANT="bullseye"
FROM mcr.microsoft.com/vscode/devcontainers/base:0-${VARIANT}

RUN sudo apt -y install lsb-release apt-transport-https ca-certificates \
    && sudo wget -O /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg \
    && echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" | sudo tee /etc/apt/sources.list.d/php.list

RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install --no-install-recommends php8.2 php8.2-bcmath php8.2-bz2 php8.2-intl php8.2-gd php8.2-mbstring php8.2-mysql php8.2-zip php8.2-dom php8.2-yaml php8.2-curl mariadb-server apache2 nodejs npm

# Xdebug.
RUN apt-get install php8.2-xdebug

# Install Composer.
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Install terminus.
RUN mkdir /utilities && composer create-project pantheon-systems/terminus /utilities/terminus \
    && echo -e '\nPATH="/utilities/terminus/bin:$PATH"' >> /home/vscode/.bashrc

# Configure Apache.
RUN echo "Listen 8080" >> /etc/apache2/ports.conf && \
    a2enmod rewrite

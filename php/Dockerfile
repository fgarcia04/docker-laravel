FROM centos:7

MAINTAINER Federico Garcia <fgarcia@urbano.com.ar>

RUN echo "Starting to setup Docker"

RUN echo "Installing Apache"
# Install Apache
RUN yum -y update
RUN yum -y install httpd httpd-tools

COPY localhost.conf /etc/httpd/conf.d/

RUN echo "Install dependencies"
RUN yum install -y wget git glibc gcc make openssl libssl-dev libcurl4-openssl-dev

RUN echo "Installing EPEL Repo"
# Install EPEL Repo
RUN yum -y install https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm \
RUN yum -y install http://rpms.remirepo.net/enterprise/remi-release-7.rpm

RUN echo "Installing PHP7.1 and modules"
# Install PHP
RUN yum install yum-utils
RUN yum-config-manager --enable remi-php71
RUN yum -y install php php-bcmath php-cli php-common php-gd php-intl php-ldap php-mbstring \
    php-mysql php-mssql php-pgsql php-pear php-soap php-xml php-xmlrpc php-pecl php-pdo pmbstringhp-zts php-devel php-mcrypt php-fileinfo php-zip

# Install composer
RUN curl -sS https://getcomposer.org/installer | php
RUN mv composer.phar /usr/local/bin/composer
RUN chmod +x /usr/local/bin/composer

WORKDIR /var/www/html

# Start Apache
EXPOSE 80
CMD ["/usr/sbin/httpd","-D","FOREGROUND"]

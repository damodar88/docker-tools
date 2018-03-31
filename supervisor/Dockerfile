FROM        ubuntu:14.04
MAINTAINER  damodar108 damodar@openmailbox.org

#actualizar sistema
RUN apt-get update -y && apt-get upgrade -yqq


#instalar php
RUN apt-get install -y php5-cli php5 php5-mcrypt php5-curl php5-pgsql

#instalar ssh
RUN apt-get install -y openssh-server supervisor
RUN mkdir -p /var/run/sshd

#add damodar usuario
RUN useradd -d /home/damodar -m -s /bin/bash damodar
RUN echo damodar:damodar | chpasswd
RUN usermod -aG sudo damodar
RUN sed -i 's/PermitRootLogin without-password/PermitRootLogin no/' /etc/ssh/sshd_config

#configuracion supervisor
RUN mkdir -p /var/log/supervisor
COPY ./supervisord.conf /etc/supervisor/supervisord.conf

#configuracion apache
COPY ./config/001-docker.conf /etc/apache2/sites-available/
RUN ln -s /etc/apache2/sites-available/001-docker.conf /etc/apache2/sites-enabled/

#variables de apache 
ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2
ENV APACHE_PID_FILE /var/run/apache2.pid
ENV APACHE_RUN_DIR /var/run/apache2
ENV APACHE_LOCK_DIR /var/lock/apache2
ENV APACHE_SERVERADMIN admin@localhost

EXPOSE 80 22

COPY ./scripts/info.php /var/www/html/info.php
CMD ["/usr/bin/supervisord","-c","/etc/supervisor/supervisord.conf"]




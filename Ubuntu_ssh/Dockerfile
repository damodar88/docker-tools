FROM ubuntu:14.04
#quien es el mantenedor
MAINTAINER Seven Dowideit <SvenDowideit@docker.com>
#actualiza y instala ssh
RUN apt-get update && apt-get install -y openssh-server
#crea carpeta den /var/run/sshd
RUN mkdir /var/run/sshd
#cambia la contraseña por damodar
RUN echo 'root:screencast' | chpasswd
#con el editor set modifica sshd_config darle permiso de conexion a root
RUN sed -i 's/PermitRootLogin without-passwd/PermitRootLogin yes/' /etc/ssh/sshd_config
#
#SSH login fix. Otherwise use is kicked off after login
RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd
#establese un balor para la variable no VISIBLE
ENV NOTVISIBLE "in users profile"
#agrega ese valor a al profile
RUN echo "export VISIBLE=now" >> /etc/profile
#abre el puerto
EXPOSE 22
#ejecutamos cuando se crea el contenedor
CMD ["/usr/sbin/sshd","-D"]

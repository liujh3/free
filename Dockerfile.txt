FROM debian
LABEL maintainer="liujunhao123123@gmail.com"
RUN apt update \
    && apt-get install -y openssh-server \
    &&  mkdir -p /var/run/sshd \
    && mkdir -p /root/.ssh
RUN sed -ri 's/session required pam_loginuid.so/#session required pam_loginuid.so/g' /etc/pam.d/sshd
ADD authorized_keys /root/.ssh/authorized_keys
ADD run.sh /run.sh
RUN chmod 755 /run.sh
EXPOSE 22
CMD ["/run.sh"]


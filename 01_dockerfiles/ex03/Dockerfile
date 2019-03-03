FROM ubuntu:18.04

RUN apt-get update
RUN apt-get upgrade -y
RUN apt-get install -y curl openssh-server tzdata ca-certificates
RUN curl -s https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.deb.sh | bash
RUN apt-get install -y gitlab-ce
RUN echo "letsencrypt['enable'] = false" >> /etc/gitlab/gitlab.rb
RUN echo "nginx['ssl_certificate'] = \"/etc/gitlab/ssl/gitlab.example.com.crt\"" >> /etc/gitlab/gitlab.rb
RUN echo "nginx['ssl_certificate_key'] = \"/etc/gitlab/ssl/gitlab.example.com.key\"" >> /etc/gitlab/gitlab.rb
RUN echo "EXTERNAL_URL='https://gitlab.example.com'" >> /etc/gitlab/gitlab.rb
RUN echo "nginx['redirect_http_to_https'] = true" >> /etc/gitlab/gitlab.rb
RUN openssl req \
	-subj "/C=US/ST=Denial/L=Springfield/O=Dis/CN=www.example.com" \
       -newkey rsa:2048 -nodes -keyout gitlab.example.com.key \
       -x509 -days 365 -out gitlab.example.com.crt
RUN mkdir -p /etc/gitlab/ssl && chmod 700 /etc/gitlab/ssl && cp gitlab.example.com.key gitlab.example.com.crt /etc/gitlab/ssl/

RUN mkdir -p /opt/gitlab/sv/sshd/supervise \
    && mkfifo /opt/gitlab/sv/sshd/supervise/ok \
    && printf "#!/bin/sh\nexec 2>&1\numask 077\nexec /usr/sbin/sshd -D" > /opt/gitlab/sv/sshd/run \
    && chmod a+x /opt/gitlab/sv/sshd/run \
    && ln -s /opt/gitlab/sv/sshd /opt/gitlab/service \
    && mkdir -p /var/run/sshd

CMD (./opt/gitlab/embedded/bin/runsvdir-start &) && EXTERNAL_URL="https://gitlab.example.com" gitlab-ctl reconfigure && gitlab-ctl tail

EXPOSE 80 443 22

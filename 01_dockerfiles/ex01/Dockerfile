from debian

RUN apt-get update
RUN apt-get install -y curl bzip2 locales
RUN mkdir /home/ts3
WORKDIR /home/ts3
RUN curl -sSLo ./ts3.tar.bz2 https://files.teamspeak-services.com/releases/server/3.6.1/teamspeak3-server_linux_amd64-3.6.1.tar.bz2
RUN tar -xvf ts3.tar.bz2
RUN rm -rf ts3.tar.bz2
ENV TS3SERVER_LICENSE accept

CMD ./teamspeak3-server_linux_amd64/ts3server_minimal_runscript.sh

EXPOSE 9987/udp
EXPOSE 10011
EXPOSE 30033

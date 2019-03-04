FROM ubuntu:18.04

RUN apt-get update
RUN apt-get install -y wget
RUN mkdir /home/minecraft && mkdir /home/minecraft/server
WORKDIR /home/minecraft/server
RUN wget https://launcher.mojang.com/v1/objects/3737db93722a9e39eeada7c27e7aca28b144ffa7/server.jar
RUN apt-get install -y openjdk-8-jre-headless screen
RUN echo "eula=true">eula.txt
EXPOSE 25565

CMD java -Xmx1024M -Xms1024M -jar server.jar nogui

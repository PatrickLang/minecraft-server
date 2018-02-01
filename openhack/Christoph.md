You'll find 2 Dockerfiles.


* openhack/1.0/nanoserver/Dockerfile.openjdk - rebuild the openjdk container service on nanoserver. The Dockerfile is full of hacks to get around lack of machine wide privilege of ContainerUser and things missing in nanoserver and powershell core

Make sure you tag the container with: `8u131-jdk-nanoserver-1709`

* nanoserver/Dockerfile.acanthamoeba - it's this is where we need to figure out how to get the G:\ to work again

_When_ this builds, tag it `minecraft-server:nanoserver-1709` 

I also modified 

* openhack/1.0/nanoserver/Dockerfile to inherit `minecraft-server:nanoserver-1709`
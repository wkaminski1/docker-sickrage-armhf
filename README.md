[linuxserverurl]: https://linuxserver.io
[forumurl]: https://forum.linuxserver.io
[ircurl]: https://www.linuxserver.io/irc/
[podcasturl]: https://www.linuxserver.io/podcast/
[appurl]: https://sickrage.github.io/
[hub]: https://hub.docker.com/r/lsioarmhf/sickrage/

[![linuxserver.io](https://raw.githubusercontent.com/linuxserver/docker-templates/master/linuxserver.io/img/linuxserver_medium.png)][linuxserverurl]

The [LinuxServer.io][linuxserverurl] team brings you another container release featuring easy user mapping and community support. Find us for support at:
* [forum.linuxserver.io][forumurl]
* [IRC][ircurl] on freenode at `#linuxserver.io`
* [Podcast][podcasturl] covers everything to do with getting the most from your Linux Server plus a focus on all things Docker and containerisation!

# lsioarmhf/sickrage
[![](https://images.microbadger.com/badges/version/lsioarmhf/sickrage.svg)](https://microbadger.com/images/lsioarmhf/sickrage "Get your own version badge on microbadger.com")[![](https://images.microbadger.com/badges/image/lsioarmhf/sickrage.svg)](http://microbadger.com/images/lsioarmhf/sickrage "Get your own image badge on microbadger.com")[![Docker Pulls](https://img.shields.io/docker/pulls/lsioarmhf/sickrage.svg)][hub][![Docker Stars](https://img.shields.io/docker/stars/lsioarmhf/sickrage.svg)][hub][![Build Status](http://jenkins.linuxserver.io:8080/buildStatus/icon?job=Dockers/LinuxServer.io-armhf/lsioarmhf-sickrage)](http://jenkins.linuxserver.io:8080/job/Dockers/job/LinuxServer.io-armhf/job/lsioarmhf-sickrage/)

Automatic Video Library Manager for TV Shows. It watches for new episodes of your favorite shows, and when they are posted it does its magic. [Sickrage](https://sickrage.github.io/)

[![sickrage](https://raw.githubusercontent.com/linuxserver/docker-templates/master/linuxserver.io/img/sickrage-banner.png)][appurl]

## Usage

```
docker create --name=sickrage \
-v <path to config>:/config \
-v <path to downloads>:/downloads \
-v <path to tv-shows>:/tv \
-e PGID=<gid> -e PUID=<uid>  \
-e TZ=<timezone> \
-p 8081:8081 \
lsioarmhf/sickrage
```

## Parameters

`The parameters are split into two halves, separated by a colon, the left hand side representing the host and the right the container side. 
For example with a port -p external:internal - what this shows is the port mapping from internal to external of the container.
So -p 8080:80 would expose port 80 from inside the container to be accessible from the host's IP on port 8080
http://192.168.x.x:8080 would show you what's running INSIDE the container on port 80.`


* `-p 8081` - the port(s)
* `-v /config` - where sickrage should store config files.
* `-v /downloads` - your downloads folder
* `-v /tv` - your tv-shows folder
* `-e PGID` for GroupID - see below for explanation
* `-e PUID` for UserID - see below for explanation
* `-e TZ` for timezone information, eg Europe/London

It is based on alpine linux with s6 overlay, for shell access whilst the container is running do `docker exec -it sickrage /bin/bash`.

### User / Group Identifiers

Sometimes when using data volumes (`-v` flags) permissions issues can arise between the host OS and the container. We avoid this issue by allowing you to specify the user `PUID` and group `PGID`. Ensure the data volume directory on the host is owned by the same user you specify and it will "just work" ™.

In this instance `PUID=1001` and `PGID=1001`. To find yours use `id user` as below:

```
  $ id <dockeruser>
    uid=1001(dockeruser) gid=1001(dockergroup) groups=1001(dockergroup)
```

## Setting up the application 
`IMPORTANT... THIS IS THE ARMHF VERSION`

Web interface is at `<your ip>:8081` , set paths for downloads, tv-shows to match docker mappings via the webui.


## Info

* To monitor the logs of the container in realtime `docker logs -f sickrage`.

* container version number 

`docker inspect -f '{{ index .Config.Labels "build_version" }}' sickrage`

* image version number

`docker inspect -f '{{ index .Config.Labels "build_version" }}' lsioarmhf/sickrage`

## Versions

+ **07.02.17:** Rebase to alpine 3.5.
+ **14.10.16:** Add version layer information.
+ **30.09.16:** Fix umask.
+ **11.09.16:** Add layer badges to README.
+ **07.09.16:** Initial Release

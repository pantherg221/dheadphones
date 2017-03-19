headphones is an automated music downloader for NZB and Torrent, written in Python. It supports SABnzbd, NZBget, Transmission, µTorrent and Blackhole.

Usage
docker create \
    --name="headphones" \
    -v /path/to/headphones/data:/config \
    -v /path/to/downloads:/downloads \
    -v /path/to/music:/music \
    -e PGID=<gid> -e PUID=<uid> \
    -e TZ=<timezone> \
    -p 8181:8181 \
    linuxserver/headphones
Parameters
The parameters are split into two halves, separated by a colon, the left hand side representing the host and the right the container side. For example with a port -p external:internal - what this shows is the port mapping from internal to external of the container. So -p 8080:80 would expose port 80 from inside the container to be accessible from the host's IP on port 8080 http://192.168.x.x:8080 would show you what's running INSIDE the container on port 80.
-p 8181 - the port(s)
-v /config - Configuration file location
-v /music - Location of music. (i.e. /opt/downloads/music or /var/music)
-v /downloads - Location of downloads folder
-e PGID for for GroupID - see below for explanation - optional
-e PUID for for UserID - see below for explanation - optional
-e TZ for setting timezone information, eg Europe/London
It is based on alpine linux with s6 overlay, for shell access whilst the container is running do docker exec -it headphones /bin/bash.
User / Group Identifiers
Sometimes when using data volumes (-v flags) permissions issues can arise between the host OS and the container. We avoid this issue by allowing you to specify the user PUID and group PGID. Ensure the data volume directory on the host is owned by the same user you specify and it will "just work" ™.
In this instance PUID=1001 and PGID=1001. To find yours use id user as below:
  $ id <dockeruser>
    uid=1001(dockeruser) gid=1001(dockergroup) groups=1001(dockergroup)
Setting up the application
Access WebUI at <your-ip>:8181 and walk through the wizard.
Info
To monitor the logs of the container in realtime docker logs -f headphones.

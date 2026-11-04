
1. Verify the target volume
Make sure /dev/sdb is actually mounted there:

```
df -h /mnt/HC_Volume_102357905
findmnt /mnt/HC_Volume_102357905
```

Also verify that it will be mounted automatically after reboot:
```
cat /etc/fstab
```


This is important: you don't want Docker starting before /dev/sdb is mounted, otherwise Docker could create /mnt/HC_Volume_102357905/docker on your root filesystem.
2. Check how much Docker currently uses
```
sudo du -sh /var/lib/docker
docker system df
```

And make sure the destination has enough free space:

```
df -h /mnt/HC_Volume_102357905
```

3. Stop Docker
This causes downtime for all containers:
```
sudo systemctl stop docker
```

Also stop the Docker socket so something doesn't automatically start Docker again:
```
sudo systemctl stop docker.socket
```

Verify:
```
systemctl status docker
```

There should be no dockerd process running.
4. Create the new Docker directory
```
sudo mkdir -p /mnt/HC_Volume_102357905/docker
```

5. Copy Docker data
Use rsync, preserving permissions, ownership, hard links, ACLs and extended attributes:
```
sudo rsync -aHAXx --numeric-ids --info=progress2 \
    /var/lib/docker/ \
    /mnt/HC_Volume_102357905/docker/
```

Do not delete /var/lib/docker yet.

Compare sizes afterward:
```
sudo du -sh /var/lib/docker
sudo du -sh /mnt/HC_Volume_102357905/docker
```

They should be approximately equal. Small differences from filesystem allocation are normal.
6. Configure Docker's new data-root
Check whether you already have a Docker configuration:
```
sudo cat /etc/docker/daemon.json
```

If it doesn't exist:
sudo mkdir -p /etc/docker
sudo nano /etc/docker/daemon.json
```
sudo mkdir -p /etc/docker
sudo nano /etc/docker/daemon.json
```

Put this in it:
```
{
  "data-root": "/mnt/HC_Volume_102357905/docker"
}
```
If daemon.json already contains settings, don't overwrite them. Add data-root to the existing JSON.

For example, if you currently have:
```
{
  "log-driver": "json-file"
}

```

change it to:
```
{
  "data-root": "/mnt/HC_Volume_102357905/docker",
  "log-driver": "json-file"
}
```



7. Start Docker
```
sudo systemctl start docker
docker info | grep -i "Docker Root Dir"
```

You want:
Docker Root Dir: /mnt/HC_Volume_102357905/docker

Check your containers:
```
docker ps -a
```

And volumes:
```
docker volume ls
```


8. Verify your important containers
Your containers, images, networks and volumes should all still exist.

9. Reboot test before deleting the old Docker data
I strongly recommend a reboot at this point:
```
sudo reboot
```

After reconnecting:
```
findmnt /mnt/HC_Volume_102357905
docker info | grep -i "Docker Root Dir"
docker ps
```

You want to establish that /dev/sdb is mounted and Docker is using it after a normal boot.
10. Only then reclaim the old space
Initially, rename rather than delete the old directory:
```
sudo mv /var/lib/docker /var/lib/docker.old
```
Run your services for a while and verify everything.

Then:
```
sudo du -sh /var/lib/docker.old
```

When you're confident everything is working:
```
sudo rm -rf /var/lib/docker.old
```

Afterward:
```
df -h /
df -h /mnt/HC_Volume_102357905
```

Your /dev/sda1 should have significantly more free space.

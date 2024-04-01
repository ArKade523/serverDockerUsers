# Instructions to mount a cloud storage device as a local directory using Rclone

1. Create the Rclone remote
```bash
rclone config
 > n
 > <enter name>
 > <choose a remote>
 > <Leave blank>
 > <Leave blank>
 > n
 > Choose "no" if on headless machine
 > Run `rclone authorize "remote-name"` on another machine and paste the auth token

```

2. Test to make sure the remote is working
```bash
rclone mount <remote name>:/ /home/<username>/onedrive/ --vfs-cache-mode writes --daemon --allow-other
```

3. Back up the docker container
```bash
sudo docker export container_<username> > <username>.tar
```

4. Stop and remove the docker container
```bash
sudo docker stop <container_name>
sudo docker rm <container_name>
```

5. Run the container again with the volume mounted
```bash
sudo docker run -v /home/<username>/:/home/math/ -d --network=host --name container_<username> math_deb1 tail -f /dev/null
```

6. Copy the .tar file and unzip it
```bash
sudo docker cp <username>_backup.tar container_<username>:/
sudo docker exec container_<username> /bin/bash
  # From inside the container
  sudo tar xf <username>_backup.tar -C /
```

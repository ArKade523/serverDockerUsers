# Server Docker Users

In order for this to work properly, the `docker_shell` file should be copied into `/usr/local/bin/`:
```
sudo cp docker_shell /usr/local/bin/
```

The ssh daemon should also be updated to call the script whenever a user attempts to connect.

These lines should be added to `/etc/ssh/sshd_config`:
```
Match Group docker
	ForceCommand /usr/local/bin/docker_shell
```

This is still a work in progress. Direct questions to [Kade Angell](mailto:kade.angell@icloud.com) 

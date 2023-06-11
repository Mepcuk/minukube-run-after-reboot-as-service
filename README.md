# minukube-run-after-reboot-as-service
Minukube run as service after Linux reboot


Create a file `minikube.service` inside `/etc/systemd/system/` folder;
Change this file in order to use your own User/Group; (Since minikube was initially configured to work in your own user)
After that run the command to update the systemd unit files: # `systemctl reload-daemon`
Now you will be able to enable your newly created systemd service: # `systemctl enable minikube`

```
[Unit]
Description=Kickoff Minikube Cluster
After=docker.service

[Service]
Type=oneshot
ExecStart=/usr/local/bin/minikube start
RemainAfterExit=true
ExecStop=/usr/local/bin/minikube stop
StandardOutput=journal
User=jon
Group=jon

[Install]
WantedBy=multi-user.target
```

+++
title = "Installation d'un service sous Linux"
date = "2024-03-10"
description = "Installation d'un service sous Linux"
tags = []
summary = "Installation d'un service sous Linux"
+++
# Exemple de configuration pour lancer un service sous Linux

```systemd
[Unit]
Description=Mon service server daemon
After=network.target

[Service]
#Type=simple
#Type=exec
Type=forking
EnvironmentFile=/etc/sysconfig/monservice
ExecStart=/usr/sbin/monservice
#Restart= always
User=monuser
KillMode=process
Environment=MON_SERVICE_HOME=/usr/share/monservice
Environment=MON_SERVICE_CONF=/etc/monservice/conf
Environment=LOCAL_JMX=false

[Install]
WantedBy=multi-user.target
```

Ensuite pour l'installer :
```shell
# installer
sudo cp curator/mon-service.service /etc/systemd/system/mon-service.service
sudo systemctl enable mon-service.service
sudo systemctl start mon-service.service
# voir l'état
sudo systemctl status mon-service.service
# voir les logs
journalctl -u mon-service.service
```

Pour la commande pour lancer le processus 
```
#!/bin/bash

nohup java -jar /home/monservice/mon-service-webapp-1.0.0-SNAPSHOT.jar --spring.config.location=/home/monservice/config/application.yml > /dev/null 2>&1 &
```

                    
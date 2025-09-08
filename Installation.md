# IBM App Connect Enterprise (ACE) Installation & Configuration

### 1. Extract & Make Global Installation of ACE - Location `/opt`
```bash
sudo cp /tmp/12.0-ACE-LINUXX64-12.0.11.3.tar.gz /opt
cd /opt
sudo tar -xvf 12.0-ACE-LINUXX64-12.0.11.3.tar.gz
sudo ace-12.0.11.3/ace make registry global accept license
```

## Create ACE Admin user & Add to required Groups & Change ownershift of ACE directories.
```bash
sudo useradd -g mqbrkrs -G mqm aceadm
sudo chown -R aceadm:mqbrkrs /opt/ace-12.0.11.3
sudo chown -R aceadm:mqbrkrs /var/mqsi
```

### Add mqsiprofile to the bashrc & Verify Installation
Add to your `.bashrc` or `.profile`:
```bash
echo "source /opt/ace-12.0.11.3/server/bin/mqsiprofile" >> ~/.bashrc
echo "export ACE_HOME=/opt/ace-12.0.11.3" >> ~/.bashrc
echo "PATH=$PATH:$ACE_HOME" >> ~/.bashrc
ace version
```

### Create Integration Node, Start & Check Status
```bash
mqsicreatebroker NODE01 -s active -i aceadm -a password
mqsistart NODE01
mqsilist NODE01
```

### Create Linux Service to start and stop Integration Node during reboots.
### This can be used for any IntegrationNode by providing as parameter
```bash
sudo vi /etc/systemd/system/ace@.service

[Unit]
Description=ACE integration node %I
After=network.target
Requires=network.target

[Service]
Type=forking
ExecStart=/bin/bash -c 'source /opt/ace-12.0.11.3/server/bin/mqsiprofile && /opt/ace-12.0.11.3/server/bin/mqsistart %I'
ExecStop=/bin/bash -c 'source /opt/ace-12.0.11.3/server/bin/mqsiprofile && /opt/ace-12.0.11.3/server/bin/mqsistop %I'
User=aceadm
Restart=on-abnormal
LimitNOFILE=10240
LimitNPROC=4096
KillMode=mixed
RestartSec=5s
TimeoutStopSec=90s

[Install]
WantedBy=multi-user.target

sudo systemctl daemon-reload
sudo systemctl enable ace@NODE01
```
# IBM App Connect Enterprise (ACE) Installation & Configuration

## Prerequisites
- Linux x64 system
- Sudo privileges
- IBM ACE installation package (e.g., `12.0-ACE-LINUXX64-12.0.11.3.tar.gz`)

## Installation Steps

### 1. Extract & Make Global Installation of ACE - Location `/opt`
```bash
sudo cp /tmp/12.0-ACE-LINUXX64-12.0.11.3.tar.gz /opt
cd /opt
sudo tar -xvf 12.0-ACE-LINUXX64-12.0.11.3.tar.gz
sudo ace-12.0.11.3/ace make registry global accept license
```

## Post-Installation Configuration

### Set Environment Variables
Add to your `.bashrc` or `.profile`:
```bash
export PATH=/opt/ace-12.0.11.3/server/bin:$PATH
export ACE_HOME=/opt/ace-12.0.11.3
```

### Verify Installation
```bash
ace version
```

## Additional Configuration

### Create Integration Node
```bash
mqsicreatebroker <NodeName>
```

### Start Integration Node
```bash
mqsistart <NodeName>
```

### Check Node Status
```bash
mqsilist <NodeName>
```

## References

- [IBM ACE Documentation](https://www.ibm.com/docs/en/app-connect/12.0)
-
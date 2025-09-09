# IBM ACE Integration Node Config File and Overrides File

## Integration Node Config File (`nodeConfig.json`)
- Contains core configuration for an IBM ACE integration node.
- Common fields include:
    - `nodeId`: Unique node identifier.
    - `host`: Node hostname or IP address.
    - `port`: Port for node communication.
    - `environment`: Deployment environment (e.g., dev, test, prod).
    - `logging`: Logging settings (level, format, etc.).
- Example:
    ```json
    {
        "nodeId": "ace-node-01",
        "host": "192.168.1.10",
        "port": 7800,
        "environment": "production",
        "logging": {
            "level": "info"
        }
    }
    ```

## Overrides File (`overrides.json`)
- Used to temporarily or selectively override values from the main config file.
- Useful for environment-specific changes, debugging, or testing.
- Typical overrides:
    - Change logging level.
    - Update host or port for a test environment.
- Example:
    ```json
    {
        "logging": {
            "level": "debug"
        },
        "port": 7900
    }
    ```

## How It Works
- The integration node loads its main config file on startup.
- If an overrides file is present, its values replace those in the main config.
- This allows flexible configuration management without changing the base file.

## Best Practices
- Keep sensitive values (like credentials) secure and out of config files.
- Use overrides for temporary or environment-specific changes.
- Document all config and override
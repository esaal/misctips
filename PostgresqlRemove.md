Copilot, 20241127

To stop the PostgreSQL service and completely remove PostgreSQL before installing a different version, follow these steps:

### 1. Stop the PostgreSQL Service
First, stop the PostgreSQL service to ensure no processes are running:
```bash
sudo systemctl stop postgresql
```

### 2. Disable the PostgreSQL Service
Prevent PostgreSQL from starting automatically on boot:
```bash
sudo systemctl disable postgresql
```

### 3. Remove PostgreSQL Packages
Remove PostgreSQL and its associated packages:
```bash
sudo apt-get --purge remove postgresql postgresql-client postgresql-client-common postgresql-common
```

### 4. Remove PostgreSQL Directories
Delete the PostgreSQL data and configuration directories:
```bash
sudo rm -rf /var/lib/postgresql/
sudo rm -rf /var/log/postgresql/
sudo rm -rf /etc/postgresql/
```

### 5. Remove the PostgreSQL User
If a system user `postgres` was created during installation, remove it:
```bash
sudo deluser postgres
```

### 6. Verify Uninstallation
Check that PostgreSQL has been completely removed:
```bash
psql --version
```
If PostgreSQL is uninstalled successfully, you should see a message like:
```bash
-bash: /usr/bin/psql: No such file or directory
```

These steps will ensure that PostgreSQL is completely removed from your system, allowing you to install a different version cleanly¹(https://www.squash.io/step-by-step-process-to-uninstall-postgresql-on-ubuntu/)²(https://neon.tech/postgresql/postgresql-administration/uninstall-postgresql-ubuntu).

Would you like guidance on installing a new version of PostgreSQL after this?

Source: Conversation with Copilot, 11/27/2024
(1) Step-by-Step Process to Uninstall PostgreSQL on Ubuntu - Squash. https://www.squash.io/step-by-step-process-to-uninstall-postgresql-on-ubuntu/.
(2) How to Uninstall PostgreSQL from Ubuntu - PostgreSQL Tutorial. https://neon.tech/postgresql/postgresql-administration/uninstall-postgresql-ubuntu.

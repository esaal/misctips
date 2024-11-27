Copilot, 20241127

To install and manage multiple versions of PostgreSQL on a Linux system, you have a few options. Here are two common methods:

### Method 1: Using `update-alternatives`
1. **Add the PostgreSQL Repository**:
   ```bash
   sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt/ $(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/pgdg.list'
   wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -
   sudo apt-get update
   ```

2. **Install Multiple PostgreSQL Versions**:
   ```bash
   sudo apt-get install postgresql-12 postgresql-13 postgresql-14
   ```

3. **Set Up Alternatives for `pg_dump`**:
   ```bash
   sudo update-alternatives --install /usr/bin/pg_dump pg_dump /usr/lib/postgresql/12/bin/pg_dump 120
   sudo update-alternatives --install /usr/bin/pg_dump pg_dump /usr/lib/postgresql/13/bin/pg_dump 130
   sudo update-alternatives --install /usr/bin/pg_dump pg_dump /usr/lib/postgresql/14/bin/pg_dump 140
   ```

4. **Switch Between Versions**:
   ```bash
   sudo update-alternatives --config pg_dump
   ```

### Method 2: Using `pgenv`
1. **Install Required Libraries**:
   ```bash
   sudo apt-get install lib32readline8 libreadline-gplv2-dev lib32tinfo6 libc6-i386 libtinfo-dev
   ```

2. **Install `pgenv`**:
   ```bash
   git clone https://github.com/theory/pgenv.git ~/.pgenv
   echo 'export PATH="$HOME/.pgenv/bin:$PATH"' >> ~/.bashrc
   source ~/.bashrc
   ```

3. **Install PostgreSQL Versions**:
   ```bash
   pgenv install 12.0
   pgenv install 13.0
   ```

4. **Switch Between Versions**:
   ```bash
   pgenv use 12.0
   pgenv use 13.0
   ```

Both methods allow you to install and switch between multiple PostgreSQL versions on your Linux system. The `update-alternatives` method is more manual but gives you fine-grained control, while `pgenv` is more automated and user-friendly¹(https://www.shkodenko.com/managing-multiple-postgresql-versions-on-ubuntu-linux-a-guide-to-using-pg_dump-with-different-server-versions/)²(https://www.cyberithub.com/how-to-manage-multiple-postgresql-instances-using-pgenv/).

Would you like more details on either method?

Source: Conversation with Copilot, 11/27/2024
(1) Managing Multiple PostgreSQL Versions on Ubuntu Linux: A ... - Shkodenko. https://www.shkodenko.com/managing-multiple-postgresql-versions-on-ubuntu-linux-a-guide-to-using-pg_dump-with-different-server-versions/.
(2) How to manage multiple PostgreSQL Instances Using pgenv. https://www.cyberithub.com/how-to-manage-multiple-postgresql-instances-using-pgenv/.
(3) github.com. https://github.com/yewton/yewton.net/tree/a40629581f7ba39b96d9dba4f17172b9e18beabe/content%2Fpost%2F2016-09-03_153406%2Findex.md.
(4) github.com. https://github.com/dry-dock/u14pls/tree/b5d524765e344c82641eb63c4df9710606b61107/version%2Fpostgres_9_4.sh.
(5) github.com. https://github.com/AntoineSavage/utils/tree/8f0e9cf566659084a12209da0aced9d1dcbfab31/install_postgres.sh.

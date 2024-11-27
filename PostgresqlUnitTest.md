Copilot, 20241127

To set up pgTAP to follow the PostgreSQL version managed by `pgenv` or `pg_dump`, you can follow these steps:

### Using `pgenv`

1. **Install pgTAP**:
   ```bash
   git clone https://github.com/theory/pgtap.git
   cd pgtap
   make && sudo make install
   ```

2. **Install PostgreSQL Versions with `pgenv`**:
   ```bash
   pgenv install 12.0
   pgenv install 13.0
   ```

3. **Switch PostgreSQL Version**:
   ```bash
   pgenv use 12.0
   ```

4. **Create pgTAP Extension in the Database**:
   ```sql
   CREATE EXTENSION pgtap;
   ```

5. **Run pgTAP Tests**:
   ```bash
   pg_prove -d your_database_name path/to/your/test.sql
   ```

### Using `pg_dump` and `update-alternatives`

1. **Install Multiple PostgreSQL Versions**:
   ```bash
   sudo apt-get install postgresql-12 postgresql-13
   ```

2. **Set Up Alternatives for `pg_dump`**:
   ```bash
   sudo update-alternatives --install /usr/bin/pg_dump pg_dump /usr/lib/postgresql/12/bin/pg_dump 120
   sudo update-alternatives --install /usr/bin/pg_dump pg_dump /usr/lib/postgresql/13/bin/pg_dump 130
   ```

3. **Switch Between Versions**:
   ```bash
   sudo update-alternatives --config pg_dump
   ```

4. **Install pgTAP**:
   ```bash
   git clone https://github.com/theory/pgtap.git
   cd pgtap
   make && sudo make install
   ```

5. **Create pgTAP Extension in the Database**:
   ```sql
   CREATE EXTENSION pgtap;
   ```

6. **Run pgTAP Tests**:
   ```bash
   pg_prove -d your_database_name path/to/your/test.sql
   ```

By following these steps, you can ensure that pgTAP is set up to follow the PostgreSQL version you are currently using with `pgenv` or `pg_dump`¹(https://www.endpointdev.com/blog/2023/04/pgtap-for-database-unit-tests/)²(https://pgtap.org/documentation.html).

Would you like more details on any of these steps?

Source: Conversation with Copilot, 11/27/2024
(1) How To Set Up pgTAP for Writing PostgreSQL Database Unit Tests. https://www.endpointdev.com/blog/2023/04/pgtap-for-database-unit-tests/.
(2) pgTAP: Documentation. https://pgtap.org/documentation.html.

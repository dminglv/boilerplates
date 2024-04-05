# FreeRADIUS with PostgreSQL

FreeRADIUS is an open-source implementation of RADIUS, an IETF protocol for AAA (Authorisation, Authentication, and Accounting). More information can be found on the FreeRADIUS website, where you can find the whole documentation as well as a quick start guide to quick start your RADIUS server.

## Installation Process

Follow these steps to set up FreeRADIUS with PostgreSQL using Docker:

1. **Install Docker**: Ensure Docker is installed on your system.

2. **Configure PostgreSQL**:
    - Create a user and a database named `radius`.
    - Utilize the `schema.sql` file to establish the database structure. ([actual PostgreSQL schema](https://github.com/FreeRADIUS/freeradius-server/blob/master/raddb/mods-config/sql/main/postgresql/schema.sql))

3. **Add new user for connection**:
   - Add a user `demo` with password `12345` to the table `radcheck` for an example:
     ```sql
     INSERT INTO radcheck VALUES (1, 'demo', 'Cleartext-Password', ':=', '12345');
      ```

4. **Database Connection Configuration**:
    - Navigate to the `raddb/mods-available/sql` file.
    - Update the database connection settings as follows:
      ```
      server = "192.0.2.3"
      port = 5432
      login = "radius"
      password = "changeme"
      ```

5. **Client Settings**:
    - Define the allowed list of clients in `raddb/clients.conf` by adjusting the following lines:
      ```
      client client_example {
          ipaddr = 192.0.2.0/24  # Change the client IP/domain
          secret = changeme123  # Change the client secret
          shortname = example  # Client name for logs
      }
      ```

6. **Build Docker Image**:
    - Use the following command to build the Docker image:
      ```shell
      docker build -t my-radius .
      ```

7. **Run Docker Image**:
    - Execute the Docker image with:
      ```shell
      docker run --rm -d --name my-radius -p 1812-1813:1812-1813/udp my-radius
      ```
8. **Configure a firewall on the server to allow UDP traffic on ports `1812` and `1813`**.
9. **Set up a connection to the Radius server from the client by using its IP address and port number `1812` and secret in file `clients.conf`**.

---

***Ensure to replace placeholder values like IP addresses, login credentials, and client secrets with your specific configurations.***


For more resources and templates, check out the [boilerplates GitHub repository](https://github.com/dminglv/boilerplates).
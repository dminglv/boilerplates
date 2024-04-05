# strongSwan with Radius and LetsEncrypt

strongSwan is free, open-source, and the most widely-used IPsec-based virtual private network implementation, allowing you to create an encrypted secure tunnel between two or more remote networks.

strongSwan uses the IKEv2 protocol, which allows for direct IPSec tunneling between the server and the client. strongSwan stands for Strong Secure WAN and supports both versions of automatic keying exchange in IPsec VPN, IKE V1 and V2.

## Installation Process

1.  **Install Ansible**: Ensure Ansible is installed on your system locally.
2. Rent a VPS with Ubuntu 22.04 LTS
3. Configure the connection to the server in order to install strongSwan in the `inventory.ini`:
   ```ini
   [vpn_servers]
   127.0.0.01 ansible_user=root ansible_ssh_pass=password
   ```
4. Use a subdomain for each VPN server. Add an A DNS record that points to your server.
5. Configure the installation configuration in the config file `config_env.yml`
6. Run the installation by using the following command:
   ```shell
   ansible-playbook -i inventory.ini all-install.yml
   ```

Ensure to replace placeholder values like IP addresses, login credentials, and client secrets with your specific configurations.

For more resources and templates, check out the [boilerplates GitHub repository](https://github.com/dminglv/boilerplates).
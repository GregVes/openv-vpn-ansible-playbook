# OpenVPN Ansible playbook

A playbook to manage a PKI for OpenVPN

```sh
ansible-playbook -i inventory.yml playbook.yml --extra-vars="host=<host-ip> host_user=<host-user> private_key=<ssh-private-key-location>"
```
## What does this playbook do?

NOTE: for commodity, we create the whole PKI on the same server. You should rather have dedicated CA (validating and signing certs) and the vpn (run openvpn) servers

This playbook creates the PKI allowing clients to tunnel their traffic to an OpenVPN server (see `inventory.yml`). When a client referenced in `clients` list is not registered on the VPN server, it is automatically created. 

* install easyrsa `3.0.8` in a dedicated `easyrsa_home`dir
* init the PKI
* generate `ca.crt` and `ca.key`
* generate `server.key` and `server.req`
* sign `server.req` and create `server.crt`
* generated pre-shared `ta.key`
* template `server.conf` and `client.base.conf`
* (optional) if ufw is installed, allow traffic through `openvpn_port`, set `DEFAULT_FORWARD_POLICY` and IP masquerading
* start openvpn server systemd service
* generate `<client>.req` and `<client>.key` for non already existing clients
* sign `<client>.req`  create `<client>.cert` for non already existing clients
* generate client config files
* copy client config files to localhost's `openvpn_client_configs_dest`

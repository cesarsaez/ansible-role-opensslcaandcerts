# Ansible role for OpenSSL CA 

The goal of this Ansible role is to build an OpenSSL Certification Authority and create and sign certificates in order to ease testing of services that require SSL.

The role is build assuming the following scenario:

- Create a root CA in 1 given node from the inventory
- Distribute and make trust the CA in the nodes from the inventory.
- Create a SSL certificate with the given Common Name and Subject Alternatives names.
- Distribute the SSL certificates to a given path in all the nodes form the directory.

## Usage

Create your playbook and adapt the variables
```
- hosts: servers
    become: yes

    roles:
    - role: opensslcaandcerts
      ca_server: myserver01
      ca_subject: "NINJAROCKESTARS-CA"
      ca_organization_name: "ACME INTERNATIONAL"
      cert_cn: "myservice.example.com"
      cert_subject_alt_names:
        - server01.example.com
        - server02.example.com
        - myservice.example.com
      cert_org: "ACME Solutions"
      cert_country: "ES"
      cert_ou: "IT LABS"
      cert_expirydate: 20221215100000Z
      myapp_service_account: myfooapp 
```
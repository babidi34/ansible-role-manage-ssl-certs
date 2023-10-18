Rôle Ansible: manage_ssl_certs
=========

This Ansible role is designed to set up SSL certificates for various applications by copying the necessary certificates from the Let's Encrypt live directory to the desired destination directory. It also ensures that the specified users have the appropriate permissions to access the certificates.

Requirements
------------

Ansible version 2.9 or higher.

Role Variables
--------------

Variable Name	Default Value	Description
ssl_certs_dir	/etc/ssl/certs	Directory where SSL certificates (.pem files) will be stored.
ssl_private_key_dir	/etc/ssl/private	Directory where the private keys for the SSL certificates will be stored.
domain_name	example.com	The domain name associated with the SSL certificate.
ssl_cert_path	{{ ssl_certs_dir }}/cert.pem	Destination path for the SSL certificate.
ssl_key_path	{{ ssl_private_key_dir }}/privkey.pem	Destination path for the private key.
ssl_ca_path	{{ ssl_certs_dir }}/chain.pem	Destination path for the certificate authority (CA) chain.
db_user	root	User that will own the SSL certificates and private keys.
ssl_users	[ "{{ db_user }}" ]	List of users that need to be added to the ssl-cert group for access to the certificates.


Dependencies
------------

None.

Example Playbook
----------------

- hosts: servers
  roles:
    - role: ssl_cert_setup
      vars:
        domain_name: 'mywebsite.com'
        ssl_users:
          - 'www-data'
          - 'mysql'


License
-------

MIT

Author Information
------------------

Feel free to modify or add any additional information that might be relevant to your specific use case!

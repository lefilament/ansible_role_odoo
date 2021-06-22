odoo
=========

This role deploys Odoo with Nginx. This role is not maintained anymore, use docker_odoo instead.

Requirements
------------

None

Role Variables
--------------

Variables from default directory :
* URLs
  * odoo_url: URL on which Nginx will be listening for serving Odoo
  * www_site: OPTIONAL : you can define whether you also want to authorize the same above URL with www. in front with the following variable (needs to be set to true)
  * odoo_url2: OPTIONAL : you can define a second URL to access you Odoo instance (which can also be combined with the above www_site)
* odoo_master_pass: Odoo Master Password (required for operations on database from Web interface)
* odoo_version: Odoo version to be deployed (defaults to 10.0)
* odoo_bin_name: Odoo executable (defaults to odoo-bin which is in use since version 10.0)
* default_maintenance_email: e-mail used to generate Let's Encrypt SSL certificate
* Custom modules to be added to Odoo sources:
  * custom_modules_base_url: Where to fetch custom modules from (defaults to https://sources.le-filament.com/lefilament)
  * odoo_custom_modules: list of custom modules to be fetched from previous URL
  * odoo_custom_modules_oca: list of dict (repo, list of modules) Odoo modules to be retrieved from OCA (https://github.com/OCA)
* Banking variables - for Odoo automatic retrieval of statements (based on https://woob.tech/)
* Backups (for backups to be deployed, host needs to be in maintenance_contract group) :
  * swift parameters for 2 object storage instances where backups should be pushed daily
  * odoo_backup_pass : Passphrase for encryption of backups

Variables from vars directory :
* odoo_user: User to be created on server for Odoo (odoo)
* odoo_home: Home diretory for Odoo user - this is where Odoo sources will be installed (/opt/odoo)
* odoo_port: Odoo internal port exposed to Nginx (8069)
* odoo_config_name: Odoo service to be deployed on server - to be used with systemctl commands (odoo-server)


Dependencies
------------

This role needs the following collections :
 * community.general
 * community.postgresql


Example Playbook
----------------

    - hosts: odoo_server
      become: true
      roles:
      - { role: odoo, tags: odoo }
      vars:
      - { odoo_url: "odoo.example.org" }
      - { odoo_master_pass: "odooMasterPasswordToBeModified" }
      - { odoo_version: "10.0" }
      - { default_maintenance_email: "maintenance@example.org" }


License
-------

AGPL-3

Author Information
------------------

Le Filament (https://le-filament.com)

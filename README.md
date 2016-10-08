Apigee Fetch Files
=========

This is a helper role that is used to download a set of files from an arbitrary set of remote servers. 
This role is typically used to download logs, configuration files and system files for examination and assessment of
server state. 

Requirements
------------

This role expects a collection that defines the directory and file name pattern to search. This role uses the linux 
find command so any directory naming convention and file naming pattern useful with find can be provided.  
 
The installation of Apigee OPDK requires root access. Credentials must also be supplied to override the empty placeholders
provided here. It is recommended that credentials be consolidated into a single credentials.yml file that can be stored 
separately. It is assumed that files containing credentials are stored in the ~/.apigee folder. 


Role Variables
--------------

Default values for variables are provided by the role apigee-opdk-setup-default-settings.

This role expects a collection of key value pairs consisting of directory and file names which will be passed into the 
`find` command. The expected key attributes are `dir:` and `name:` such that the defining a collection for apigee logs 
assigned to the `apigee_log_files` would look like this:
 
    apigee_log_files:
      - { dir: '{{ opdk_installer_path }}/', name: '*.log' }
      - { dir: '{{ opdk_installer_path }}/var/log/', name: '*.log' }
      
The name of variable to reference your collection of key value pairs.

    fetch_files: '{{ apigee_log_files }}'


Dependencies
------------

This role depends on the following roles:

* apigee-opdk-setup-default-settings

Example Playbook
----------------

      - hosts: planet
        vars:
          apigee_log_files:
            - { dir: '{{ opdk_installer_path }}/', name: '*.log' }
            - { dir: '{{ opdk_installer_path }}/var/log/', name: '*.log' }
        roles:
        - { role: fetch-files, fetch_files: '{{ apigee_log_files }}' }         

License
-------

Apache License Version 2.0, January 2004

Author Information
------------------

Carlos Frias
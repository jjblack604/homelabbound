Role Name
=========

Docker Trove Datastores

This role facilitates the setup and management of Docker-based Trove datastores, ensuring Docker registry authentication, image building, tagging, and pushing to a specified Docker registry.

Use at your own risk.

I realize that many users deploy with tags such as 1.1.0, whereas this role uses database version as tag. I may add some login in the future to accomodate that.

Ideally place this behind a proxy :).

Requirements
------------

Configuration of variable overrides.

Role Variables
--------------

    trove_docker_repository: URL of the Docker registry. This can be an IP address and port (192.168.1.100:5000) or a domain (registry.example.com).

    trove_registry_name: The namespace within the Docker registry for storing datastore images (e.g., trove-datastores).

    trove_containers: List of datastore configurations, each item should define:
        datastore_name: Name of the datastore (mariadb, mysql, postgresql).
        version: Version of the datastore.
        os: Operating system for the datastore image (currently supports ubuntu).
        os_version: Version of the OS.

    trove_repo_destination_directory, trove_build_directory, trove_docker_build_logs: Paths for the cloned Trove repository, image build directory, and build logs.

    trove_image_maintainer: Maintainer contact email.

    trove_docker_htpasswd_path, trove_docker_htpasswd_user, trove_docker_htpasswd_passwd: Configuration for Docker registry authentication.

    trove_docker_config: Docker daemon configuration, including insecure-registries and dns settings.

    trove_docker_external_port_map, trove_docker_internal_port_map: Port mappings for accessing the Docker registry.

Dependencies
------------

No external dependencies. This role is designed to manage all its requirements internally.

Example Playbook
----------------

    - hosts: docker_servers
      vars:
        trove_docker_repository: "registry.example.com"
        trove_registry_name: "trove-datastores"
        trove_docker_htpasswd_user: "admin"
        trove_docker_htpasswd_passwd: "secure_password"
        trove_containers:
          - datastore_name: "mariadb"
            version: "10.4"
            os: "ubuntu"
            os_version: "20.04"
      roles:
        - { role: docker_trove_datastores }

License
-------

GPLv3

Author Information
------------------

James Black - OpenStack Infrastructure Engineer<br>
@hamburgler IRC<br>
https://www.homelabbound.com
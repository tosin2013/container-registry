Container Registry
=========

This role will install a container registry using podman. This role will also sync the registry with Openshift for a disconnected install.

Requirements
------------
The role swygue-redhat-subscription is required by this role to subscribe the system.
```
ansible-galaxy install git+https://github.com/Qubinode/swygue-redhat-subscription.git
```

The following collections are required for the deployment
```
ansible-galaxy collection install community.general
ansible-galaxy collection install community.crypto
ansible-galaxy collection install ansible.posix
ansible-galaxy collection install containers.podman
```

Role Variables
--------------



Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: username.rolename, x: 42 }

Test Registry
-------
**Login to registry**
```
podman login ${HOSTNAME}:5000
```

**Push image to registry** 
```
podman pull registry.access.redhat.com/ubi8/ubi:latest
podman tag registry.access.redhat.com/ubi8/ubi:latest ${HOSTNAME}:5000/ubi8/ubi:latest
podman push  ${HOSTNAME}:5000/ubi8/ubi:latest
```

**Verifiy image exists**
```
curl -u registryuser:registryuserpassword  --connect-timeout 15  https://${HOSTNAME}:5000/v2/_catalog
```

License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).

### Ansible playbooks for deployment of EnMasse to OCP

Enmasse version: 0.16.0-rc4

#### Prerequisites

* Add the path to the Openshift `oc` client in `playbooks/group_vars/all.yml`.
* Build the `enmasse-keycloak-client` project with Maven, and copy the `enmasse-keycloak-client.jar` JAR archive into `roles/openshift_enmasse/files/enmasse_keycloak_client`
* Log into the OpenShift cluster with the `oc` client

#### Usage

* Install EnMasse to OpenShift (singletenant)

    ```
    $ ansible-playbook playbooks/enmasse.yml
    ```

* Create a brokered address space

    ```
    $ ansible-playbook playbooks/enmasse.yml -e create_address_space=true
    ````

* Create a standard address space

    ```
    $ ansible-playbook playbooks/enmasse.yml -e create_address_space=true \
    -e address_space_type=standard
    ```

* Create addresses

    ```
    $ ansible-playbook playbooks/enmasse.yml -e create_address=true
    ```

* Create additional addresses

    ```
    $ ansible-playbook playbooks/enmasse.yml -e create_address=true \ 
    -e address_names='[{"name":"queue1","type":"queue","plan":"standard"},{"name":"queue2","type":"queue","plan":"standard"}]'
    ```

### ToDo

* support for multitenant installation
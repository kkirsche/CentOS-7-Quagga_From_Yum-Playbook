# Quagga Playbook

This installs the following items from source:

* Gawk 4.1.1
* Texinfo 5.2
* Quagga 0.99.24.1

This playbook is designed and has been tested on:

* CentOS 7 Minimal Installation with Development Tools


## Running the playbook

1. Edit the `hosts` file to contain a list of hosts which you would like to run this playbook on. __Note:__ only one host per line!
2. Ensure your public SSH key is on each host, we will be assuming you are using SSH keys, not passwords! To add your SSH key to a fresh CentOS 7 installation, execute the following command, replacing the `username` and `ipaddress` with the ones of the host.
```shell
cat ~/.ssh/id_rsa.pub | ssh username@ipaddress 'mkdir -p ~/.ssh/; touch ~/.ssh/authorized_keys; cat >> .ssh/authorized_keys'
```
3. Run the playbook:
```shell
ansible-playbook -i hosts quagga.yml -t gawk,texinfo,quagga,configure
```


## Those versions are outdated!

At the time of creating this playbook, all the above versions are the most recent versions available. It is possible though that they will be outdated in the future and you may want these updated. This is simple thanks to the variables used in this project.

#### Updating Dependencies

Here we will show you how to update a dependency or quagga. We will use gawk as an example. The only difference between these is the package name, version, and location of the tarball.

Dependenant source code will be in:

* Quagga: `./roles/quagga/files/quagga-0.99.24.1.tar.gz`
* Gawk: `./roles/dependencies/files/gawk-4.1.1.tar.gz`
* Texinfo: `./roles/dependencies/files/texinfo-5.2.tar.gz`

__Gawk Example:__

1. Clone the project
2. Open `./vars/default.yml`
3. Change the value of `gawk_version` to the new version in the `package-version` (example: `gawk-4.1.1`) format.
4. Replace `./roles/dependencies/files/gawk-4.1.1.tar.gz` with a `.tar.gz` of the version you would like to use in `./roles/dependencies/files/package-version.tar.gz` format.
5. Run the playbook

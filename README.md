# jenkins-test-kitchen-ansible

An Ansible role that deploys Jenkins CI with a job that runs Test Kitchen to test an Ansible role from GitHub.

### 1. Start a Vagrant Virtual Machine

```
$ cd vagrant
$ vagrant up
```

### 2. Fetch the IP Address of the Virtual Machine

First, connect to your virtual machine:

```
$ cd vagrant
$ vagrant ssh
```

Identify the IP address through which the virtual machine is accessible from outside via `ifconfig`. In this example, we assume the IP address to be `192.168.0.66`. `exit` the virtual machine again.

### 3. Enter the IP Address of the Virtual Machine into Ansible's `hosts` file

```
$ echo 192.168.0.66 > hosts
```

### 4. Run the Ansible Playbook to provision the Virtual Machine

```
$ ansible-playbook -i hosts playbook.yml
```

When asked for a password, enter `vagrant`.


After successful provisioning, Jenkins can be accessed via `192.168.0.66:8080` in your browser. Jenkins comes readily configured with a project called `MyCoolApp`. When you build the project, [Test Kitchen](http://kitchen.ci) will execute [Serverspec](http://serverspec.org) tests against an Ansible role and present its colorized results in the Jenkins Build's Console Output.

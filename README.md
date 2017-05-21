# Configuring Jenkins using Ansible

## Objectives

* Using ansible, automatically configure a server running jenkins, abiding by the following constraints:

  - Setup necessary runtime packages automatically.
  - Be able to setup jenkins configuration files automatically.
  - Be able to automatically setup a job to build [this repo.](https://github.com/CSC-326/JSPDemo)

## Description

The playbook to setup Jenkins can be found [here](https://github.com/gms298/Configuring-Jenkins-using-Ansible/tree/master/Playbook%20files).

The tree structure of the playbook is as follows: 

```
- main.yml                    # The main YML file which gets executed by ansible-playbook
- roles/
	- jenkins/
		- files/
			- jenkins-ci.org.key
		- templates/
			- build.xml.j2
		- vars/
			- main.yml
		- tasks/
			- main.yml
			- dependencies.yml
			- jenkins.yml
			- jobs.yml
```

Run `ansible-playbook -i inventory main.yml -s` to automatically start executing the role `jenkins` which will in turn execute all the task files in order.

The file [dependencies.yml](https://github.com/gms298/Configuring-Jenkins-using-Ansible/blob/master/Playbook%20files/roles/jenkins/tasks/dependencies.yml) installs the necessary runtime packages and dependencies required by Jenkins automatically. 

The file [jenkins.yml](https://github.com/gms298/Configuring-Jenkins-using-Ansible/blob/master/Playbook%20files/roles/jenkins/tasks/jenkins.yml) will install Jenkins, Jenkins CLI as well as the `git plugin` required by Jenkins to build the JSPDemo Project. It also **configures Jenkins** automatically by disabling security by appropriately modifying the config.xml file used by Jenkins.

The file [jobs.yml](https://github.com/gms298/Configuring-Jenkins-using-Ansible/blob/master/Playbook%20files/roles/jenkins/tasks/jobs.yml) will actually use a template to create a job in jenkins as well as build that job.

## Screencast

[Click here](https://www.youtube.com/watch?v=753-g3cD_ts) to view the screencast video.
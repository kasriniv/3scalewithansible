# Creating 3scale artifacts in a CI-CD pipeline using Ansible

This repo is to provide ansible scripts to create all 3scale artifacts needed to provision a service in 3scale.
They can be invoked as-is or a via a jenkins-ansible plugin.
The ansible playbooks here are divided into:
1. Create a new 3scale service
2. Update a new 3scale service

(These will be merged later)

The ansible playbook 'addnewservice.yml' creates a new 3scale service using the parameters defined in newservicedetails.yml.
The service id generated from this call is required to be set in updateservicedetails.yml.
Update service uses the updateservicedetails.yml to do the following :
- set the backend url
- set the production endpoint
- set the staging endpoint
- get the metricid for the default metric 'Hits'
- create a mapping rule for the verb+pattern combination defined in updateservicedetails.yml
- create an application plan : a required contract for a 3scale proxied service to be tested.
- create an application : required so a key can be used to test the 3scale proxied endpoint
- test the 3scale proxied endpoint 


How to run
---------
To run ansible playbook to create a service
Step 0: set the properties you want in newservicedetails.yml 
Step 1: ansible-playbook addnewservice.yml
Step 2: get service id from the debug output of Step 1 and edit updateservicedetails.yml
Step 3: ansible-playbook updateservice.yml

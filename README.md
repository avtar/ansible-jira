# JIRA Ansible Role

This role is meant to be used with external playbooks to build and test JIRA Docker images. When invoked it will provision a Docker image with all of JIRA's requirements with the exception of a database server. A Supervisor configuration file is prepared as part of the image build. No context path is configured to JIRA will only be reachable using http://yourdomain.com/ and not http://yourdomain.com/jira 

A separate deployment related playbook accepts PostgreSQL database information as environment variables and is meant to be executed when starting a container using the previously built Docker image.

The image should be tested by launching a container and verifying that the expected HTTP status code is returned while searching the result of a GET request for a specified string.


## Role variables

    jira_groupname: jira
    jira_username: jira

The user account and group that will own application directories. Supervisor will also start the application process using this account.

    jira_install_dir: /opt/jira

The directory where the JIRA distribution is extracted.

    jira_home_dir: /opt/jira-home

The directory where critical JIRA data is stored. Unless a temporary container is launched to test a newly built image this directory should be provided to a production container as a volume.


## Environment variables

    jira_version

The version of JIRA being installed.

    jira_db_name
    jira_db_username
    jira_db_password
    DB_SERVICE_ADDRESS

The PostgreSQL database, user name, password, and IP address.

    jira_tcp_port

The TCP port that JIRA should used to serve requests.

    jira_test_http_endpoint

The HTTP endpoint that the test playbook should attempt to reach. '/' is a safe default.

    jira_test_http_status_code

The HTTP status code to expect to confirm JIRA is working. '200' is a safe default.

    jira_test_string

A string that the test playbook should search for to confirm that JIRA has been deployed properly. 

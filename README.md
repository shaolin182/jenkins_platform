This project aims to build a jenkins environment through docker containers.
This environment will be compose of 2 nodes : 
* a Jenkins master
* a Jenkins slave

Jenkins slave can run docker containers by reusing unix socket that docker daemon is listening from host

Plugins from jenkins_master/plugins.txt will be automatically installed

# Installation


    # Add secrets files in jenkins-master/secret folder
    echo "Default_Jenkins_User_to_change" > ./jenkins_master/secrets/JENKINS_USER
    echo "Default_Jenkins_password_to_change" > ./jenkins_master/secrets/JENKINS_PASSWORD

    # Build and run containers
    docker-compose up -d --build --force-recreate

# TODO
Add a volume for persisting jenkins configurations
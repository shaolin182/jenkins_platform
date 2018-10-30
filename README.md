This project aims to build a jenkins environment through docker containers.
This environment will be compose of 2 nodes : 
* a Jenkins master
* a Jenkins slave

Jenkins slave can run docker containers by reusing unix socket that docker daemon is listening from host

Plugins from jenkins_master/plugins.txt will be automatically installed

# Installation


    # Add secrets files in jenkins-master/secret folder
    echo -n "Default_Jenkins_User_to_change" > ./jenkins_master/secrets/JENKINS_USER
    echo -n "Default_Jenkins_password_to_change" > ./jenkins_master/secrets/JENKINS_PASSWORD

    # On windows env, export that variable fof handling path
    export COMPOSE_CONVERT_WINDOWS_PATHS=1

    # Build and run containers
    docker-compose up -d --build

# Jenkins plugins
In order to get a list of all installed plugins, you can run those commands


    JENKINS_HOST=username:password@myhost.com:port
    curl -sSL "http://$JENKINS_HOST/pluginManager/api/xml?depth=1&xpath=/*/*/shortName|/*/*/version&wrapper=plugins" | perl -pe 's/.*?<shortName>([\w-]+).*?<version>([^<]+)()(<\/\w+>)+/\1 \2\n/g'|sed 's/ /:/'
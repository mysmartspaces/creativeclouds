# [Free GitLab local server using docker compose](https://github.com/igecloudsdev/gitlab-server/blob/main/README.md#free-gitlab-local-server-using-docker-compose)

**GitLab** is a web-based platform used to host Git repositories. This tool supports software development using the Continuous Delivery(CD) and Continuous Integration(CI) processes

This repo contains a docker compose script to set up and self-host a local instance of GitLab server. It’s an alternative to GitHub able to run locally for free and is very easy to set up. The script was tested on Linux and Windows but should work on any platform able to run Docker. Feel free to clone or fork .


There are some of the features or benefits that comes with gitlab


* Easy integration with Jenkins, Docker, Slack, Kubernetes, JIRA, LDAP e.t.c
* Code Quality (Code Climate)
* On-premise or cloud-based installations
* Development Analytics
* Performance monitoring
* Rich API
* Integration with IDEs like Eclipse, Visual Studio, Koding, and IntelliJ
* Issue management, bug tracking, and boards
* Repository mirroring and high availability (HA)
* Hosting static websites (GitLab Pages)
* ChatOp tool (Mattermost)
* Code Review functionality and Review Apps tool
* Service Desk (ticketing system)



# [Follow these steps to set up GitLab locally](https://github.com/igecloudsdev/gitlab-server/blob/main/README.md#follow-these-steps-to-set-up-gitlab-locally)

Check out the repo:

```
$ git clone https://github.com/PhiCygni/gitlab-free-local-server-using-docker-compose.git
```

Get the local hostname of the machine you want to run GitLab on:

```
$ hostname
```

Modify the `.env` file with a text editor and change the `localhost` value to your local hostname. For example:

```
GITLAB_HOSTNAME=mydesktop
```

Build the container and start it:

```
$ docker-compose up
```

While it's building and starting up open another terminal to the same directory and run the command:

```
$ docker-compose ps
```

This command will report on the current state of the container. Wait until the **`State`** column reports the container to be **`Up (health: healthy)`** and not  **`Up (health: starting)`** . This might take about **5 minutes so be patient!** This is how we know the building of the container is completed and is ready to be used.

Now retrieve the newly created GitLab root password:

```
Linux: $ sudo cat ./config/initial_root_password

Windows: $ type .\config\initial_root_password
```

Example output:

```
Password: zsFHw3SpgwSTal1+Ufiurw4DaghDIcKlVy+MUctmxwE=
```

**Make sure to write this root password down somewhere because GitLab will delete it in time!**

One can now access the GitLab UI using URL `http://MY_HOSTNAME:7080/`. For instance if the hostname is `mydesktop` then the URL is [http://mydesktop:7080](http://mydesktop:7080/). The username is `root` and we just found the password in the step above. Log in as `root` to get started.

Note: URL [http://localhost:7080/](http://localhost:7080/) will also work to access the server, but the local hostname will be required if one wants to access the server from another computers on the local LAN.

# [Configuring your GitLab server after it is set up](https://github.com/igecloudsdev/gitlab-server/blob/main/README.md#configuring-your-gitlab-server-after-it-is-set-up)

Your GitLab container is now running and you can access the UI. Now do the following to start using it:

1. Log in with the root account and for security reasons make a new user with admin rights and use it for everyday admin tasks. The root account should only be used when needed. It should also the noted the root account can only be used using localhost access and remote access is not allowed. Therefore creating another admin user is recommended.
2. Configure your firewall to open up port `TCP 7080` if access to other LAN computers is required.

# [Using GitLab with a SSL certificate](https://github.com/igecloudsdev/gitlab-server/blob/main/README.md#using-gitlab-with-a-ssl-certificate)

It should be noted my script design currently does not make of the SSL HTTPS capability of GitLab and uses only the non-encrypted HTTP protocol. This was intentional to keep install steps to a minimum and simplify things as much as possible. In my opinion using HTTP only is not the end of the world given that the recommended use case of my script is for a private local network.

However, it is very possible to generate a SSL certificate for GitLab so that HTTPS can be used instead of just HTTP. One can generate a Certificate Authority and then add it to all the client computers requiring a verified HTTPS connection to the GitLab server. I will expand this repo to incorporate the addition of verified HTTPS access if I see there is enough interest.

# [Steps to completely remove the GitLab container](https://github.com/igecloudsdev/gitlab-server/blob/main/README.md#steps-to-completely-remove-the-gitlab-container)

**Note! The following steps will completely remove the GitLab container and all its repos!**

You will only want to do this if you want to do fresh install for some reason or just don't need the container anymore. If that's the case do the following to remove the container, repos and its config files:

```
Linux: $ ./script-docker-compose-down-remove-everything.sh

Windows: $ script-docker-compose-down-remove-everything.bat
```

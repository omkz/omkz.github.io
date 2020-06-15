---
published: true
title: Install Rabbit Mq On Ubuntu 18.04
layout: post
categories: misc
tags: [rabbitmq, backend]
---

Copy the following script and save it in your server as rabbit.sh:

```bash
#!/bin/sh
## If sudo is not available on the system,
## uncomment the line below to install it
# apt-get install -y sudo
sudo apt-get update -y
## Install prerequisites
sudo apt-get install curl gnupg -y
## Install RabbitMQ signing key
curl -fsSL https://github.com/rabbitmq/signing-keys/releases/download/2.0/rabbitmq-release-signing-key.asc | sudo apt-key add -
## Install apt HTTPS transport
sudo apt-get install apt-transport-https
## Add Bintray repositories that provision latest RabbitMQ and Erlang 21.x releases
sudo tee /etc/apt/sources.list.d/bintray.rabbitmq.list <<EOF
## Installs the latest Erlang 22.x release.
## Change component to "erlang-21.x" to install the latest 21.x version.
## "bionic" as distribution name should work for any later Ubuntu or Debian release.
## See the release to distribution mapping table in RabbitMQ doc guides to learn more.
deb https://dl.bintray.com/rabbitmq-erlang/debian bionic erlang
deb https://dl.bintray.com/rabbitmq/debian bionic main
EOF
## Update package indices
sudo apt-get update -y
## Install rabbitmq-server and its dependencies
sudo apt-get install rabbitmq-server -y --fix-missing
```
Run the script:
```
sh rabbit.sh
```

Check RabbitMQ Server Status.
```
sudo systemctl status rabbitmq-server.service
```

If RabbitMQ is not running, then start service with this command:
```
sudo systemctl start rabbitmq-server.service
```

Enable RabbitMQ service on system boot.
```
sudo systemctl enable rabbitmq-server
```

Let us see how we can enable the ‘Installation Management Console’ plugin. But before we do that, let us take a look at all the RabbitMQ plugins that are available.
```
sudo rabbitmq-plugins list
```
Now enable the RabbitMQ Management plugin
```
sudo rabbitmq-plugins enable rabbitmq_management
```

We can access the Management console using the default guest user. But we need to create and add a new Admin user to access Management console.

Here we create a user with username ‘admin’ and password is also ‘admin’. But I would recommend using a strong password for security.
```
sudo rabbitmqctl add_user admin admin
```

Now we tag our user ‘admin’, which we created in the steps above, as ‘administrator’
```
sudo  rabbitmqctl set_user_tags admin administrator
```

Now we are ready to restart RabbitMQ service
```
sudo systemctl restart rabbitmq-server.service
```

Management UI access
The Management Console can be accessed using either of these URLs:

```bash 
http://localhost:15672

```

![Screenshot from 2020-05-15 19-20-17](https://user-images.githubusercontent.com/444807/82049781-26bdc380-96e1-11ea-9649-ed2dbfb5939d.png)

Ref:
- https://medium.com/@danielmontoyahd/installing-rabbitmq-on-ubuntu-18-04-190af686be90
- https://www.fosslinux.com/6339/how-to-install-rabbitmq-server-on-ubuntu-18-04-lts.htm
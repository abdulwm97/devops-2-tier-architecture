![image](https://user-images.githubusercontent.com/80905254/122024703-94df2900-cdc0-11eb-963b-f65f06e3bd4e.png)


## Provision file downloading and installing nginx and nodejs to the app instance
```
#!/bin/bash
sudo apt-get update -y

sudo apt-get upgrade -y

sudo  apt-get install nginx -y

sudo systemctl enable nginx

sudo apt-get install nodejs -y

sudo apt-get install npm-y

sudo apt-get install python-software-properties

curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash

sudo apt-get install nodejs -y

sudo npm install pm2 -g

npm install 
```

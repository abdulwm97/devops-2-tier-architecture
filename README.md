![image](https://user-images.githubusercontent.com/80905254/122024703-94df2900-cdc0-11eb-963b-f65f06e3bd4e.png)

## Replace default with this for reverse proxy (the ip is the ip of the app)
```
server {
	listen 80;

	server_name _;

	location / {
		proxy_pass http://192.168.10.100:3000;
		proxy_http_version 1.1;
		proxy_set_header Upgrade $http_upgrade;
		proxy_set_header Connection 'upgrade';
		proxy_set_header Host $host;
		proxy_cache_bypass $http_upgrade;
	}
}
```
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

## To install mongodb on database instance
```
# be careful of these keys, they will go out of date
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv D68FA50FEA312927
echo "deb https://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/3.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.2.list



sudo apt-get update -y
sudo apt-get upgrade -y



# sudo apt-get install mongodb-org=3.2.20 -y
sudo apt-get install -y mongodb-org=3.2.20 mongodb-org-server=3.2.20 mongodb-org-shell=3.2.20 mongodb-org-mongos=3.2.20 mongodb-org-tools=3.2.20



# remoe the default .conf and replace with our configuration
sudo rm /etc/mongod.conf
```

## Replace mongod file at cd /etc/ with following
```
# mongod.conf

# for documentation of all options, see:
#   http://docs.mongodb.org/manual/reference/configuration-options/

# Where and how to store data.
storage:
  dbPath: /var/lib/mongodb
  journal:
    enabled: true
#  engine:
#  mmapv1:
#  wiredTiger:

# where to write logging data.
systemLog:
  destination: file
  logAppend: true
  path: /var/log/mongodb/mongod.log

# network interfaces
net:
  port: 27017
  bindIp: 0.0.0.0


#processManagement:

#security:

#operationProfiling:

#replication:

#sharding:

## Enterprise-Only Options:

#auditLog:

#snmp:
```

## Then restart and enable mongod
```
sudo systemctl restart mongod
sudo systemctl enable mongod
```

## In the app instance do the following
`export DB_HOST=mongodb://192.168.10.150:27017/posts` - This sets up the environment variable for DB_HOST
Seeding maybe required so go to the seeds folder and `node seed.js`.
Now `npm start`


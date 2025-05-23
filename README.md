# MongoDB-database-Node.js-Express-REST-API
MongoDB database  &amp; Node.js/Express REST API on Ubuntu 24 Servers


Mongo db


# MongoDB Deployment on Ubuntu 24

This guide outlines the steps to deploy a MongoDB database on an Ubuntu 24 server.

1. Update System Packages

```bash
sudo apt update
```

2. Import MongoDB GPG Key and Add Repository

```bash
wget -nc https://www.mongodb.org/static/pgp/server-6.0.asc
cat server-6.0.asc | gpg --dearmor | sudo tee /etc/apt/keyrings/mongodb.gpg >/dev/null 
sudo sh -c 'echo "deb [ arch=amd64,arm64 signed-by=/etc/apt/keyrings/mongodb.gpg] https://repo.mongodb.org/apt/ubuntu jammy/mongodb-org/6.0 multiverse" >> /etc/apt/sources.list.d/mongo.list'
```

3. Install MongoDB

```bash
sudo apt update
sudo apt install mongodb-org -y
```

4. Start MongoDB Service

```bash
sudo systemctl start mongod
```

5. Create a User with Password

Access the MongoDB shell:

```bash
mongosh
```

Execute the following commands in the MongoDB shell:

```javascript
use recipe
db.createUser({
  user: "admin",
  pwd: "12345",
  roles: [ { role: "readWrite", db: "recipe" } ]
})
exit

```
6. Verify Installation (Optional)

Check the status of the MongoDB service:

```bash
sudo systemctl status mongod
```




USE THIS 


# Deploy a Node.js/Express REST API on Ubuntu 24

This guide outlines the steps to deploy a Node.js/Express REST API on an Ubuntu 24 server.

1. Update System Packages

```bash
sudo apt update
```

2. Install Node.js

```bash
curl -sL https://deb.nodesource.com/setup_18.x | sudo bash -
sudo apt install nodejs -y
```

3. Install Yarn (Optional)

```bash
sudo npm install -g yarn
```

4. Clone the Project

```bash
git clone https://github.com/GerromeSieger/RecipeApp-Node.git
cd RecipeApp-Node
```

5. Install Dependencies

Using npm:

```bash
npm install
```

Or using Yarn:

```bash
yarn install
```

6. Set Up Environment File

```bash
cp .envEXAMPLE .env
```

Edit .env file to configure your database and other settings

7. Run the Application

Using npm:

```bash
npm run start
```

Or using Yarn:

```bash
yarn start
```

8. Verify Deployment

Open a web browser and navigate to http://publicip:5000/docs to access the swagger documentation.

Alternative Deployment Strategy (Using Systemd)

9. Set Up as a Systemd Service

Create a service file:

```bash
sudo nano /etc/systemd/system/nodejs-api.service
```

Add the following content (adjust paths as necessary):

```ini
[Unit]
Description=Node.js API
After=network.target

[Service]
User=root
WorkingDirectory=/root/RecipeApp-Node
ExecStart=/usr/bin/yarn start
Restart=always

[Install]
WantedBy=multi-user.target

```

10. Reload Daemon, Start and Enable nodejs-api Service

```bash
sudo systemctl daemon-reload
sudo systemctl start nodejs-api
sudo systemctl enable nodejs-api
sudo systemctl status nodejs-api
```

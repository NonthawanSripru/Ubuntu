# Ubuntu
## 1. Install the **Installation on Ubuntu** package with :

```sh
sudo apt-get update

```
 <p align="center"><img src="nginx/1.JPG" width=500></p>

```sh
sudo apt-get install nginx 
```
<p align="center"><img src="nginx/2-installnginx.JPG" width=500></p>

## 2. Setting Up a Node.js Server
2.1 Create a simple Node.js server. We’ll start by initiating a project and installing the Express package:
```sh
mkdir node-demo && cd node-demo
```


```sh
npm init -y
```
<p align="center"><img src="nginx/3.JPG" width=500></p>

```sh
npm i express
```
 
 
2.2 Create a file called server.js, with the following contents:
 <p align="center"><img src="nginx/4.JPG" width=500></p>
 
```sh
const express = require('express')
```

```sh
const app = express()
```

```sh
const port = 3000
```

```sh
app.get('/', (req, res) => res.send('Hello World!'))
```


```sh
app.listen(port, () => console.log(`Example app listening on port ${port}!`))
```

 <p align="center"><img src="nginx/6.JPG" width=500></p>
 
2.3 You can start the server by running 'node server.js'

```sh
node server.js
```
 <p align="center"><img src="nginx/7.JPG" width=500></p>
 
## 3. Configuring NGINX
	3.1 open up the NGINX default site config file
```sh
sudo nano /etc/nginx/sites-available/default
```
3.2 If you want, you can go directly to the directory and open up the config file with your favorite text editor. As you scroll down, you’ll find a server block. It looks something like this:

 
```sh
server {
  listen       80;
  server_name  localhost;

  ....
  more config goes here
}
```

3.3 Next, we’ll configure the server block to suit our needs. We want to configure NGINX to pass all requests through to our Node.js server. Replace the above server block with a new block as shown below:


 <p align="center"><img src="nginx/8.JPG" width=500></p>
 
```sh
server {
  listen       80;
  server_name  localhost;

  location / {
    proxy_pass http://localhost:3000;
    proxy_http_version 1.1;
    proxy_set_header Upgrade $http_upgrade;
    proxy_set_header Connection 'upgrade';
    proxy_set_header Host $host;
    proxy_cache_bypass $http_upgrade;
  }
```

3.4 save the file and type the following to restart NGINX
<p align="center"><img src="nginx/9.JPG" width=500></p>

```sh
sudo service nginx restart
```

<p align="center"><img src="nginx/10.JPG" width=500></p>

```sh
node server.js
```


## successfully installed You will see the word Hello world.

<p align="center"><img src="nginx/11.JPG" width=500></p>


 



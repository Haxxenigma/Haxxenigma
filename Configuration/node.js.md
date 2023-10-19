# [Node.js](https://nodejs.org/ru)

### Install Node.js & npm:

```shell
apt install nodejs
apt install npm
```

### Initialize project:

```shell
mkdir mywebserver
cd mywebserver

npm init
```

### Create 'public' folder:

```
mywebserver/
├── public/
│   ├── index.html
│   ├── style.css
│   └── script.js
└── index.js
```

### Start project:

```shell
node index.js
```

<br>

### index.js *with http:*

```javascript
const http = require('http');
const fs = require('fs');
const path = require('path');

const hostname = '127.0.0.1';
const port = 80;

const server = http.createServer((req, res) => {
    let filePath = path.join(__dirname, 'public', req.url === '/' ? 'index.html' : req.url);

    fs.readFile(filePath, (err, data) => {
        if (err) {
            res.writeHead(404);
            res.end('Not Found');
            return;
        }

        res.writeHead(200);
        res.end(data);
    });
});

server.listen(port, hostname, () => {
    console.log(`Server is running at http://${hostname}:${port}/`);
});
```

<br>

### index.js *with express:*

```javascript
const express = require('express');
const path = require('path');
const app = express();

const hostname = '127.0.0.1';
const port = 80;

app.use(express.static(path.join(__dirname, 'public')));

app.get('/', (req, res) => {
    res.sendFile(path.join(__dirname, 'public', 'index.html'));
});

app.use((req, res) => {
    res.status(404).send('Not Found');
});

app.listen(port, hostname, () => {
    console.log(`Server is running at http://${hostname}:${port}/`);
});
```

<br>
<br>

## Self-Signed SSL Certificate for Node.js

```shell
sudo openssl req -x509 -days 365 -nodes -newkey rsa:4096 -keyout private.key -out certificate.crt
```

<br>

### index.js *with https:*

```javascript
const https = require('https');
const fs = require('fs');
const path = require('path');

const hostname = '127.0.0.1';
const port = 443;

const options = {
    key: fs.readFileSync('private.key'),
    cert: fs.readFileSync('certificate.crt'),
};

const server = https.createServer(options, (req, res) => {
    let filePath = path.join(__dirname, 'public', req.url === '/' ? 'index.html' : req.url);

    fs.readFile(filePath, (err, data) => {
        if (err) {
            res.writeHead(404);
            res.end('Not Found');
            return;
        }

        res.writeHead(200);
        res.end(data);
    });
});

server.listen(port, hostname, () => {
    console.log(`Server is running at https://${hostname}:${port}/`);
});
```

<br>

### index.js *with express:*

```javascript
const https = require('https');
const express = require('express');
const path = require('path');
const app = express();

const hostname = '127.0.0.1';
const port = 443;

const options = {
    key: fs.readFileSync('private.key'),
    cert: fs.readFileSync('certificate.crt'),
};

app.use(express.static(path.join(__dirname, 'public')));

app.use((req, res) => {
    res.status(404).send('Not Found');
});

const server = https.createServer(options, app);

server.listen(port, hostname, () => {
    console.log(`Server is running at https://${hostname}:${port}/`);
});
```

<br>
<br>

## Redirect

### index.js:

```javascript
const http = require('http');
const https = require('https');
const express = require('express');
const fs = require('fs');
const path = require('path');
const app = express();

const hostname = '127.0.0.1';
const httpPort = 80;
const httpsPort = 443;

const options = {
    key: fs.readFileSync('private.key'),
    cert: fs.readFileSync('certificate.crt'),
};

app.use(express.static(path.join(__dirname, 'public')));

app.use((req, res) => {
    res.status(404).send('Not Found');
});

const httpServer = http.createServer((req, res) => {
    res.writeHead(301, { Location: `https://${req.headers.host}${req.url}` });
    res.end();
});

const httpsServer = https.createServer(options, app);

httpServer.listen(httpPort, hostname, () => {
    console.log(`Server is running at http://${hostname}:${httpPort}/`);
});

httpsServer.listen(httpsPort, hostname, () => {
    console.log(`Server is running at https://${hostname}:${httpsPort}/`);
});
```
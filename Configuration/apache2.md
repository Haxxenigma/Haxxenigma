# [Apache2](https://httpd.apache.org/)

### Install Apache2:

```shell
apt install apache2
```

### Create folder for website:

```shell
mkdir /var/www/example.com/
chown -R $USER:$USER /var/www/example.com/
chmod -R 755 /var/www/example.com/
nano /var/www/example.com/index.html
```

### /etc/apache2/sites-available/example.com.conf:

```xml
<VirtualHost *:80>
    ServerAdmin webmaster@example.com
    ServerName example.com
    ServerAlias www.example.com
    DocumentRoot /var/www/example.com
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```

### Enable website:

```shell
sudo a2ensite example.com.conf
sudo a2dissite 000-default.conf
```

### Start Apache2 service:

```shell
systemctl start apache2
systemctl enable apache2
```

```shell
service apache2 start
service apache2 enable
```

### Create rule in firewall:

```shell
ufw allow 'Apache'
ufw reload
ufw show
```

### Config test:

```shell
sudo apache2ctl configtest
```

<br>

## Self-Signed SSL Certificate for Apache2

```shell
sudo a2enmod ssl
```

```shell
sudo openssl req -x509 -days 365 -nodes -newkey rsa:4096 -keyout private-key.pem -out public-cert.pem
```

### /etc/apache2/sites-available/example.com.conf:

```xml
<VirtualHost *:80>
        Servername example.com
        ServerAlias www.example.com
        
        Redirect permanent / https://example.com
</VirtualHost>

<VirtualHost *:443>
        ServerName example.com
        ServerAlias www.example.com
        ServerAdmin webmaster@example.com
        DocumentRoot /var/www/example.com

        SSLEngine on
        SSLCertificateFile      public-cert.pem
        SSLCertificateKeyFile   private-key.pem

        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```

# [React.js](https://react.dev/)

```shell
npx create-react-app my-react-app
```

```shell
npm i react@latest react-dom@latest
```

```shell
npm start
```

### index.html:

```html
<!DOCTYPE html>
<html>
  <head><title>My app</title></head>
  <body>
    <p>This paragraph is a part of HTML.</p>
    <nav id='root'></nav>
    <p>This paragraph is also a part of HTML.</p>
  </body>
</html>
```

### index.js:

```js
import { createRoot } from 'react-dom/client';

function App() {
    return <h1>Hello, world</h1>;
}

const root = createRoot(document.getElementById('root'));
root.render(<App />);
```

# [Next.js](https://nextjs.org/a)

```shell
npx create-next-app@latest
```

```shell
npm run dev
```

### app/app/page.js:

```js
export default function Page() {
    return <h1>Hello, Home</h1>
}
```

### app/app/dashboard/page.js:

```js
export default function Page() {
    return <h1>Hello, Dashboard</h1>
}
```

### app/app/layout.js:

```js
import { Inter } from 'next/font/google'
import './globals.css'

const inter = Inter({ subsets: ['latin'] })

export const metadata = {
    title: 'Title',
    description: 'Description',
}

export default function RootLayout({ children }) {
    return (
        <html lang='en'>
            <body className={inter.className}>{children}</body>
        </html>
    )
}
```

# MySQL

```shell
sudo apt install mysql-server mysql-client
```

```shell
mysql -u root -p < create_db.sql
```

### create_db.sql:

```sql
CREATE DATABASE IF NOT EXISTS db;

USE db;

CREATE USER IF NOT EXISTS 'user'@'%' IDENTIFIED BY 'password';
GRANT ALL PRIVILEGES ON db.* TO 'user'@'%';
FLUSH PRIVILEGES;

CREATE TABLE IF NOT EXISTS users (
    id INTEGER PRIMARY KEY AUTO_INCREMENT,
    name NVARCHAR(255) UNIQUE NOT NULL,
    email NVARCHAR(255) UNIQUE NOT NULL,
    password TEXT NOT NULL,
    birth_date DATE,
    user_image TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);

CREATE TABLE IF NOT EXISTS articles (
    id INTEGER PRIMARY KEY AUTO_INCREMENT,
    title NVARCHAR(255) NOT NULL,
    author NVARCHAR(255) NOT NULL,
    content TEXT NOT NULL,
    thumbnail TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
    FOREIGN KEY (author) REFERENCES users(name) ON UPDATE CASCADE
);
```

### /etc/mysql/mysql.conf.d/mysqld.cnf:

```conf
bind-address = 0.0.0.0
```

```shell
systemctl restart mysql
```

# MySQL x Next.js

### mysql2:

```shell
npm install mysql2
```

### .env:

```shell
HOST=<server-ip-addr>
USER=<user>
PASS=<password>
DB=<db>
```

### app/db.js:

```js
const mysql = require('mysql2/promise');

const connectToDatabase = async () => {
    const db = await mysql.createConnection({
        host: process.env.HOST,
        user: process.env.USER,
        password: process.env.PASS,
        database: process.env.DB,
    });

    await db.connect();
    return db;
}

module.exports = async function execQuery(query, values) {
    const db = await connectToDatabase();
    try {
        const res = await db.query(query, values);
        return res;
    } catch (err) {
        return { err };
    } finally {
        db.end();
    }
}
```

### app/app/page.js:

```js
import Link from 'next/link';
const execQuery = require('db.js');

export const metadata = {
    title: 'Main',
    description: 'Main page',
}

export default async function Home() {
    const [users, _] = await execQuery('SELECT * FROM users');
    return (
        <>
            {
                users.map(user => (
                    <Link href={user.name} key={user.id}>{user.name}</Link>
                ))
            }
        </>
    );
}
```
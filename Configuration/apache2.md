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

### /app/page.js:

```js
export default function Page() {
    return <h1>Hello, Home</h1>
}
```

### /app/dashboard/page.js:

```js
export default function Page() {
    return <h1>Hello, Dashboard</h1>
}
```

### /app/layout.js:

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

# Next.js x MySQL

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

### /db.js:

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

### /app/page.js:

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

# Next.js x Prisma

```shell
npm install prisma
```

```shell
npx prisma init
```

### /prisma/schema.prisma:

```
datasource db {
  provider = "mysql"
  url      = env("DATABASE_URL")
}
```

### /.env:

```
DATABASE_URL='mysql://USER:PASSWORD@HOST:PORT/DATABASE'
```

<br>

### Create Models in the schema.prisma from the database:

```shell
npx prisma db pull
```

### Create Tables in the database from the schema.prisma:

```shell
npx prisma db push
```

### Create a migration from changes in Prisma schema, apply it to the database, trigger generators:

```shell
npx prisma migrate dev [--name <name>]
```

### Reset your database and apply all migrations:

```shell
npx prisma migrate reset
```

<br>

### Install Prisma Client:

```shell
npm install @prisma/client
```

### Generate Prisma Client:

```shell
npx prisma generate
```

###  Importing Prisma Client:

```javascript
import { PrismaClient } from '@prisma/client';

const prisma = new PrismaClient();
```

### Create:

```javascript
const newRecord = await prisma.model.create({
    data: {
        name: 'John',
        email: 'john@email.com',
    },
});

const newRecords = await prisma.model.createMany({
    data: [
        { name: 'John', email: 'john@email.com' },
        { name: 'Eve', email: 'eve@email.com' },
        { name: 'Alice', email: 'alice@email.com' },
    ],
    skipDuplicates: true,
});
```

### Read:

```javascript
const record = await prisma.model.findUnique({
    where: {
        email: 'john@email.com',
    },
});

const records = await prisma.model.findMany({
    where: {
        email: {
            endsWith: 'prisma.io',
        },
    },
});
```

### Update:

```javascript
const updateRecord = await prisma.model.update({
    where: {
        email: 'john@email.com',
    },
    data: {
        name: 'John Doe',
    },
});

const updateRecords = await prisma.model.updateMany({
    where: {
        email: {
            contains: 'prisma.io',
        },
    },
    data: {
        role: 'admin',
    },
});

const upsertRecord = await prisma.model.upsert({
    where: {
        email: 'john@email.com',
    },
    update: {
        name: 'John Doe',
    },
    create: {
        email: 'john@email.com',
        name: 'John Doe',
    },
});
```

### Delete:

```javascript
const deleteRecord = await prisma.model.delete({
    where: {
        email: 'john@email.com',
    },
});

const deleteRecords = await prisma.model.deleteMany({
    where: {
        email: {
            contains: 'prisma.io',
        },
    },
});
```
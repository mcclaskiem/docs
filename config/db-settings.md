# Database Connection Settings

Craft supports several database connection settings that give you control over how Craft connects to the database.

Ultimately, database connection settings must be set from  `config/db.php`, but we recommend you initially set them as environment variables (such as in your `.env` file), and then pull the environment variable value into `config/db.php` using [getenv()](http://php.net/manual/en/function.getenv.php).

For example, in a new Craft 3 project, your `.env` file should define these environment variables:

```bash
ENVIRONMENT="dev"
SECURITY_KEY=""
DB_DSN="mysql:host=<host>;port=<port>;dbname=<dbname>"
DB_USER="root"
DB_PASSWORD=""
DB_SCHEMA="public"
DB_TABLE_PREFIX=""
```

The variables that start with `DB_` are database connection settings, and they get pulled into `config/db.php` like this:

```php
return [
    'dsn' => getenv('DB_DSN'),
    'user' => getenv('DB_USER'),
    'password' => getenv('DB_PASSWORD'),
    'schema' => getenv('DB_SCHEMA'),
    'tablePrefix' => getenv('DB_TABLE_PREFIX'),
];
```

::: tip NOTE
If you installed Craft before 3.4 was released, you will have `DB_DRIVER`, `DB_SERVER`, `DB_DATABASE`, and `DB_PORT` environment variables (a well as corresponding values in `config/db.php`) instead of `DB_DSN`. Both approaches work, but setting `DB_DSN` instead is recommended in Craft 3.4 and later. 
:::

We recommend this environment variable approach for two reasons:

1. It keeps sensitive information out of your project’s codebase. (`.env` files should never be shared or committed to Git.)
2. It makes collaborating with other developers easier, as each developer can define their own settings without overwriting someone else’s settings.

Here’s the full list of database connection settings that Craft supports:

<!-- BEGIN SETTINGS -->

### `attributes`

Allowed types

:   [array](http://php.net/language.types.array)

Default value

:   `[]`

Defined by

:   [DbConfig::$attributes](api:craft\config\DbConfig::$attributes)



An array of key => value pairs of PDO attributes to pass into the PDO constructor.

For example, when using the MySQL PDO driver (http://php.net/manual/en/ref.pdo-mysql.php),
if you wanted to enable a SSL database connection (assuming SSL is enabled in MySQL
(https://dev.mysql.com/doc/refman/5.5/en/using-secure-connections.html) and `'user'`
can connect via SSL, you'd set these:

```php
[
    PDO::MYSQL_ATTR_SSL_KEY    => '/path/to/my/client-key.pem',
    PDO::MYSQL_ATTR_SSL_CERT   => '/path/to/my/client-cert.pem',
    PDO::MYSQL_ATTR_SSL_CA     => '/path/to/my/ca-cert.pem',
],
```



### `charset`

Allowed types

:   [string](http://php.net/language.types.string)

Default value

:   `'utf8'`

Defined by

:   [DbConfig::$charset](api:craft\config\DbConfig::$charset)



The charset to use when creating tables.



### `database`

Allowed types

:   [string](http://php.net/language.types.string)

Default value

:   `null`

Defined by

:   [DbConfig::$database](api:craft\config\DbConfig::$database)



The name of the database to select.



### `driver`

Allowed types

:   [string](http://php.net/language.types.string)

Default value

:   `null`

Defined by

:   [DbConfig::$driver](api:craft\config\DbConfig::$driver)



The database driver to use. Either 'mysql' for MySQL or 'pgsql' for PostgreSQL.



### `dsn`

Allowed types

:   [string](http://php.net/language.types.string)

Default value

:   `null`

Defined by

:   [DbConfig::$dsn](api:craft\config\DbConfig::$dsn)



The Data Source Name (“DSN”) that tells Craft how to connect to the database.

DSNs should begin with a driver prefix (`mysql:` or `pgsql:`), followed by driver-specific parameters.
For example, `mysql:host=127.0.0.1;port=3306;dbname=acme_corp`.

- MySQL parameters: http://php.net/manual/en/ref.pdo-mysql.connection.php
- PostgreSQL parameters: http://php.net/manual/en/ref.pdo-pgsql.connection.php



### `password`

Allowed types

:   [string](http://php.net/language.types.string)

Default value

:   `''`

Defined by

:   [DbConfig::$password](api:craft\config\DbConfig::$password)



The database password to connect with.



### `port`

Allowed types

:   [integer](http://php.net/language.types.integer)

Default value

:   `null`

Defined by

:   [DbConfig::$port](api:craft\config\DbConfig::$port)



The database server port. Defaults to 3306 for MySQL and 5432 for PostgreSQL.



### `schema`

Allowed types

:   [string](http://php.net/language.types.string)

Default value

:   `'public'`

Defined by

:   [DbConfig::$schema](api:craft\config\DbConfig::$schema)



The schema that Postgres is configured to use by default (PostgreSQL only).



### `server`

Allowed types

:   [string](http://php.net/language.types.string)

Default value

:   `null`

Defined by

:   [DbConfig::$server](api:craft\config\DbConfig::$server)



The database server name or IP address. Usually `localhost` or `127.0.0.1`.



### `tablePrefix`

Allowed types

:   [string](http://php.net/language.types.string)

Default value

:   `''`

Defined by

:   [DbConfig::$tablePrefix](api:craft\config\DbConfig::$tablePrefix)



If you're sharing Craft installs in a single database (MySQL) or a single
database and using a shared schema (PostgreSQL), then you can set a table
prefix here to avoid table naming conflicts per install. This can be no more than 5
characters, and must be all lowercase.



### `unixSocket`

Allowed types

:   [string](http://php.net/language.types.string), [null](http://php.net/language.types.null)

Default value

:   `null`

Defined by

:   [DbConfig::$unixSocket](api:craft\config\DbConfig::$unixSocket)



MySQL only. If this is set, then the CLI connection string (used for yiic) will
connect to the Unix socket, instead of the server and port. If this is
specified, then 'server' and 'port' settings are ignored.



### `url`

Allowed types

:   [string](http://php.net/language.types.string), [null](http://php.net/language.types.null)

Default value

:   `null`

Defined by

:   [DbConfig::$url](api:craft\config\DbConfig::$url)



The database connection URL, if one was provided by your hosting environment.

If this is set, the values for [driver](https://docs.craftcms.com/api/v3/craft-config-dbconfig.html#driver), [user](https://docs.craftcms.com/api/v3/craft-config-dbconfig.html#user), [database](https://docs.craftcms.com/api/v3/craft-config-dbconfig.html#database), [server](https://docs.craftcms.com/api/v3/craft-config-dbconfig.html#server), [port](https://docs.craftcms.com/api/v3/craft-config-dbconfig.html#port), and [database](https://docs.craftcms.com/api/v3/craft-config-dbconfig.html#database)
will be extracted from it.



### `user`

Allowed types

:   [string](http://php.net/language.types.string)

Default value

:   `'root'`

Defined by

:   [DbConfig::$user](api:craft\config\DbConfig::$user)



The database username to connect with.




<!-- END SETTINGS -->

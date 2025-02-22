# MySQL Storage for [OAuth 2.0](https://github.com/go-oauth2/oauth2)

![example workflow](https://github.com/httpoz/go-oauth2-mysql/actions/workflows/unit-test.yml/badge.svg)
 [![GoDoc][godoc-image]][godoc-url] [![License][license-image]][license-url]

## Install

```bash
$ go get -u -v github.com/httpoz/go-oauth2-mysql/v2
```

## MySQL drivers

The store accepts an `sqlx.DB` which interacts with the DB. `sqlx.DB` is a specific implementations from [`github.com/jmoiron/sqlx`](https://github.com/jmoiron/sqlx)

## Usage example

```go
package main

import (
	_ "github.com/go-sql-driver/mysql"
	mysql "github.com/httpoz/go-oauth2-mysql/v2"
	"github.com/jmoiron/sqlx"
)

func main() {
	db, err := sqlx.Connect("mysql", "user:password@tcp(127.0.0.1:3306)/oauth_db?parseTime=true")
	if err != nil {
		log.Fatalln(err)
	}

	clientStore, _ := mysql.NewClientStore(db, mysql.WithClientStoreTableName("custom_table_name"))
	tokenStore, _ := mysql.NewTokenStore(db)
}
```

## How to run tests

You will need running MySQL instance. E.g. the one running in docker and exposing a port to a host system

```bash
$ docker run -it  -p 3306:3306 -e MYSQL_ROOT_PASSWORD=oauth2 -d mysql
$ docker exec -it <container_id> bash
$ mysql -u root -poauth2
> create database oauth_db
```

```bash
$ MYSQL_URI=root:oauth2@tcp(127.0.0.1:3306)/oauth_db?parseTime=true go test .
```

## MIT License

```
Copyright (c) 2019 Imre Nagi
```

## Credits
- MySQL Storage for OAuth 2.0 [`https://github.com/imrenagi/go-oauth2-mysql`](https://github.com/imrenagi/go-oauth2-mysql)
- Oauth Postgres Implementation [`github.com/vgarvardt/go-pg-adapter`](https://github.com/vgarvardt/go-pg-adapter)

[godoc-url]: https://godoc.org/github.com/httpoz/go-oauth2-mysql/v2
[godoc-image]: https://godoc.org/github.com/httpoz/go-oauth2-mysql/v2?status.svg
[license-url]: http://opensource.org/licenses/MIT
[license-image]: https://img.shields.io/npm/l/express.svg

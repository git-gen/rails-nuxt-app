# docker-example

docker 雛形

- ruby on rails
- nuxt.js
- postgresql

## 導入方法

軽量化する為、alpinelinux を採用

rails を backend、nuxt を fontend として作成します

**nuxt 作成**

```bash
$ docker-compose run --rm nuxt yarn create nuxt-app ./app
```

**rails 作成**

```bash
$ docker-compose run ror rails new . --force --no-deps --database=postgresql --skip-yarn --skip-action-mailer --skip-active-storage --skip-action-cable --skip-sprockets --skip-javascript --skip-turbolinks --skip-test --api --skip-bundle

$ docker-compose run ror bundle install
```

config/database.ymlを書き換える

```yml
default: &default
  adapter: postgresql
  encoding: utf8
  username: <%= ENV["POSTGRES_USER"] %>
  password: <%= ENV["POSTGRES_PASSWORD"] %>
  database: <%= ENV["POSTGRES_DB"] %>
  host: db
```

イメージとコンテナを作る

```bash
$ docker-compose build

$ docker-compose up -d
```

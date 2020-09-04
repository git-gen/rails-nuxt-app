# docker-example

docker の雛形を docker-compose を使ってまとめて作成します

- ruby on rails
- nuxt.js
- postgresql

## 導入方法

軽量化する為、alpinelinux を採用

rails を backend、nuxt を fontend として作成します  
db は postgresql を使用します

### nuxt 作成

nuxt は docker から作成すると、以下のようなエラーが発生しました

```bash
$ mkdir nuxt && cd nuxt

# Dockerfile作成
$ touch Dockerfile && vi Dockerfile

$ docker-compose run --rm nuxt yarn create nuxt-app .

Error: "Can't create . because there's already a non-empty directory . existing in path."
```

その為、local で作成した nuxt を後から docker 化させて作成します

```bash
# localにyarnが必要
$ yarn create nuxt-app nuxt

# tempフォルダに入れてあるnuxt用のDockerfileを作成したnuxtのフォルダに移す
$ mv temp/Dockerfile nuxt

# tempフォルダは不要になったので削除する
$ rm -rf temp
```

docker で nuxt のポートは 3333 に設定してあるので、  
作成した nuxt アプリの設定もnuxt.config.jsから合わせましょう

```javascript
/* nuxt.config.js */

module.exports = {
  server: {
    port: 3333,
  },
};
```

### rails 作成

docker から rails を作成します  
Gemfile は ror フォルダに入れてあるので、`bundle init`は必要ありません  
railsはAPIでしか使用しない想定なので、いらない機能は軽量化の為オプションでスキップします

```bash
$ docker-compose run ror rails new . --force --no-deps --database=postgresql --skip-yarn --skip-action-mailer --skip-active-storage --skip-action-cable --skip-sprockets --skip-javascript --skip-turbolinks --skip-test --api --skip-bundle

$ docker-compose run ror bundle install
```

config/database.yml を書き換える

```yml
# config/database.yml

default: &default
  adapter: postgresql
  encoding: utf8
  username: developergeeeen
  password: testpass
  database: testdb
  host: db
  pool: <%= ENV.fetch("RAILS_MAX_THREADS") { 5 } %>

development:
  <<: *default

test:
  <<: *default

production:
  <<: *default
```

### サーバーを立てる

イメージとコンテナを作る

```bash
$ docker-compose build

$ docker-compose up -d
```

rails
http://localhost:3000

nuxt
http://localhost:3333

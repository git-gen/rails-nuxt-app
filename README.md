# docker-example

docker 雛形

- ruby on rails
- nuxt.js
- nginx
- postgresql

## 導入メモ

軽量化する為、alpinelinux を採用

rails を backend、nuxt を fontend として想定

rails作成
```bash
$ docker-compose run ror rails new . --force --no-deps --database=postgresql --skip-yarn --skip-action-mailer --skip-active-storage --skip-action-cable --skip-sprockets --skip-javascript --skip-turbolinks --skip-test --api --skip-bundle

$ docker-compose run ror bundle install
```

nuxt作成
```bash
$ docker-compose run --rm nuxt yarn create nuxt-app .
```

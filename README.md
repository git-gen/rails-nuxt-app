# docker-example

docker 雛形

- ruby on rails
- nuxt.js
- nginx
- postgresql

## 導入メモ

軽量化する為、alpinelinux を採用

rails を backend、nuxt を fontend として想定

API として rais new する

```bash
bundle exec rails new . --database=postgresql --skip-yarn --skip-action-mailer --skip-active-storage --skip-action-cable --skip-sprockets --skip-javascript --skip-turbolinks --skip-test --api --skip-bundle
```

docker で新規に rails new する場合

```bash
docker-compose run ror rails new . --force --no-deps --database=postgresql --skip-yarn --skip-action-mailer --skip-active-storage --skip-action-cable --skip-sprockets --skip-javascript --skip-turbolinks --skip-test --api --skip-bundle

docker-compose run ror bundle install
```

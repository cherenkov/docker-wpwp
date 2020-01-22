# Docker WordPress Browser-sync Webpack

Docker上にWordPress/browser-sync/webpack環境を構築するテンプレート。  
phpmyadminも入ってる。

## images

- mysql:5.7
- wordpress:latest
- phpmyadmin/phpmyadmin
- ustwo/browser-sync
- node:12.12.0

## Usage

### Setting

``` sh
# envファイルを作成
cp .env.template .env

# 自分用に編集（プロジェクト名、テーマ名等々を変更）
vi .env

# テーマディレクトリをTHEME_NAMEにあわせる
mv app/themes/my_theme app/themes/${THEME_NAME}
```

./docker/webpack/webpack.config.js
``` diff
- const THEME_NAME = 'my_theme';// in .env
+ const THEME_NAME = ${THEME_NAME};// in .env
```

### docker build & up

``` sh
# docuer立ち上げ
docker-compose up -d

# 所有権を変更
# これをしないと言語選択できない
docker-compose exec -T ${PROJECT_NAME}-wp chown -R www-data:www-data /var/www/html/
```

open http://localhost:3000/

## Option

### Webpack Production Build

```sh
# webpackのcontainerにログイン
docker exec -it ${PROJECT_NAME}-webpack sh

# build
yarn build
```

### DB dump

```sh
./backup-db.sh
```

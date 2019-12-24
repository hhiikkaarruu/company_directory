# company_directory
社員一覧ウェブサイト

## Description
Laravel学習のための社員一覧ウェブサイト。
Dockerを使って手軽に動かせるように作りました。

## Feature (2019/12/21:Comming soon !!)
- 社員一覧表示
- 社員登録
- 社員削除

## Usage
```
$ git clone https://github.com/hhiikkaarruu/company_directory
$ cd company_directory
$ docker-compose up
$ firefox http://localhost
```

## Tech
- PHP
	- Version:7.4.0
- Laravel
	- Version:5.5.48
- Apache
	- Version:2.4.38
- MySQL
	- Version:5.7.48
- phpMyAdmin
	- Version:5.7.28

## Done
### 自分の環境(macOS + VirtualBox + ArchLinux)に開発環境構築
- PHPインストール
	```
	$ sudo pacman -S php
	```
- composerインストール
	```
	$ sudo pacman -S composer
	```
- Laravelインストーラーインストール
	```
	$ composer global require laravel/installer
	```
- PATH追加
	```
	$ nvim .zshenv
# 下記追記
	export PATH=${HOME}/.config/composer/vendor/bin:${PATH}
	```
### Github・Docker環境構築
- githubリポジトリ作成
	- このリポジトリを作成
- リポジトリを自分の環境にクローン
	```
	$ git clone https://github.com/hhiikkaarruu/company_directory
	```
- docker-compose環境設計・構築
	- ディレクトリ構成決定
	- Laravelプロジェクト作成
	```
	$ cd company_directory/php
	$ composer create-project "laravel/laravel=5.5.*" laravel
	```
	- Apache設定ファイル作成
	```
	$ nvim company_directory/php/apache/000-default.conf
	```
	- PHP設定ファイル作成
	```
	$ nvim company_directory/php/php.ini
	```
	- MySQL設定ファイル作成 (必要になるのかはまだ理解していない)
	```
	$ cd company_directory/mysql
	$ touch my.cnf init/001_create_tables.sql init/init_db.sh
	```
	- docker-compose作成
	```
	$ nvim docker-compose.yml
	```
- 起動・アクセス
	```
	$ docker-compose up -d
	$ firefox http://localhost
	```
	- 下記エラー発生
		```
		The stream or file "/var/www/html/storage/logs/laravel.log" could not be opened: failed to open stream: Permission denied
		```
	- 上記エラー解消
		```
		$ nvim company_directory/php/init.sh
		# 下記記述
		chown -R www-data:www-data /var/www/html/storage/logs

		$ nvim docker-compose.yml
		# phpコンテナのボリュームに下記追記
		- ./php/init.sh:/docker-entrypoint-initdb.d/init.sh:ro
		```
	- 下記エラー発生
		```
		file_put_contents(/var/www/html/storage/framework/sessions/Yv5UavpKvZrypLNVlWaDOHz73ea22rQ059xI5k9A): failed to open stream: Permission denied
		```
	- 上記エラー解消
		```
		$ nvim company_directory/php/init.sh
		# 下記記述
		chmod -R 777 /var/www/html/storage/framework
		```
	- 再度立ち上げ。エラー無くLaravelのスタートページが表示された。
### 社員一覧ウェブページ実装
- Doing now. (2019/12/24)

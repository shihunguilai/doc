# composerd 的使用


## 1.安装composer
- composer 需要php5.3.+，全局安装

```
curl -sS https://getcomposer.org/installer | php
mv composer.phar /usr/local/bin/composer

```

- 替换composer的全局配置文件到中国镜像

`composer config -g repo.packagist composer https://packagist.phpcomposer.com`

## 2.composer.json文件
- require:是项目必须使用的包，require-dev:开发测试时要用的包，正式环境不需要的
- `composer update` require 和require－dev的包都会安装
- `composer update --no-dev` 只会安装require的包

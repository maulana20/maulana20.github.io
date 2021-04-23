### Ssh
```bash
ssh -i key.pem user@host => login
scp -i key.pem file user@host:location_path => upload
```

### Git
```bash
git branch
git diff
git checkout feature/update_content
git checkout -p public/js/app.js => revert
git pull origin release/1.0.0
git reset --hard => note : revert all
git reset --hard origin/develop
```

### Permission Storage
```bash
sudo chown -R $USER:www-data {directory}
sudo chmod -R 775 {directory}
```

### Install Package Other Php
```bash
/usr/bin/php7.3 /usr/local/bin/composer install
```

### Restart `php.ini`
```bash
sudo service nginx restart
sudo service php7.3-fpm restart
```

### Up Max Size Upload
```bash
upload_max_filesize = 10M
post_max_size = 10MB
client_max_body_size = 10MB
```

### Reload Cache
```bash
php artisan config:cache
php artisan config:clear

composer global update
composer dump-autoload
```

### Update Package
```bash
composer update facade/ignition
```

### Cek Log
```bash
/var/log/nginx
sudo tail error.log
```

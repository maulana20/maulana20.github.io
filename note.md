### Ssh
```bash
ssh -i key.pem user@host => login
scp -i key.pem file user@host:location_path => upload
```

### Git
```bash
git fetch
git branch
git diff
git checkout feature/update_content
git checkout -p public/js/app.js => revert
git pull origin release/1.0.0
git reset --hard => note : revert all
git reset --hard origin/develop
git filter-branch --index-filter 'git rm -rf --cached --ignore-unmatch backend/xxx.json' feature/xxx => remove file and history
git reset --hard [commitId]
git push --force
git add [pathFile]
git commit --amend --no-edit
git rebase branch-parent
git rebase --onto new-parent old-parent
```

### Permission Storage
```bash
sudo chown -R $USER:www-data {directory}
sudo chmod -R 775 {directory}
```

### Install Package
```bash
/usr/bin/php7.3 /usr/local/bin/composer install => another php
sudo apt-get update
sudo apt-get upgrade
sudo apt-get install xxx
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
composer update => note : for all
composer update facade/ignition
```

### Certificate Update
```bash
git config --global http.sslVerify false
```

### Cek Log
```bash
/var/log/nginx
sudo tail error.log
```

### Redis
```bash
cli > KEYS *
cli > KEYS tus:*
cli > GET tus:xxx
cli > FLUSHALL
cli > MONITOR
```

### Docker Python First
```bash
pip freeze > requirements.txt
pip install -r requirements.txt
--------------------------------------
command: tail -f /dev/null
ENV VIRTUAL_ENV=/app/env
$ . env/bin/activate
```

### Git Config
```bash
$PATH\.git\config
```

### Linux Information
```bash
uname -sr
lsb_release -a
sudo systemctl status xxx
```

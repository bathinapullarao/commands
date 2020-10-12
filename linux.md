## SCP
* scp -r -i id_rsa -P61854 /tmp/sugar.zip dev_bathinapullarao@153.146.159.201:/tmp
* scp -r -i ~/.ssh/dev_chef01.pem /tmp/sugar.sql dev_chef01@dev-gcm-db04:/tmp
* scp -i ~/.ssh/dev_chef01.pem dev_chef01@dev-db99:/tmp/* /home/dev_chef01/DB-BACKUP/
## diff 
// compare two files
* diff -y /etc/my.cnf_20190107 /etc/my.cnf |grep "|"
## IF
if [ $(echo qa01 | cut -c 1-3) != "dev" -a $(echo qa01 | cut -c 1-2) != "qa" ]; then
    rm -rf /var/www/html/catch /var/www/html/*.conf
fi
##sed
sed -i -e "s/MEMORY_STORE_IP/10.61.199.44/g" /etc/php.ini
##mount
mount -t gcsfuse -o implicit_dirs,uid=48,gid=48,allow_other qa01-gcm-uploads /var/www/html/upload

# /etc/crontab
echo "# SugarCRM Sucheduled JOB (DF-106)" >> /etc/crontab
echo "* * * * * apache cd /var/www/html; php -f cron.php > /dev/null 2>&1" >> /etc/crontab

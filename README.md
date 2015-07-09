# CLI-tool: Add Apache vhost in one line

This script makes it a bit easier to add a new Apache 2.4+ vhost and document root on Ubuntu.
It was built as a means for me to quickly add new sites on my development server.


## Installation

You can either download it from this git repo, or you can download it from your server with:
```bash
wget http://dl.maer.se/cli/addvhost
```
It will always download the latest version (the master from this repository).

Make the file executable and move it to `/usr/local/bin/`folder:
```bash
# Ubuntu example
sudo chmod +x addvhost
sudo mv addvhost /usr/local/bin/addvhost
```


## Configuration

There are a few things you should (or rather need) to change to fit your environment.

Open the script in an editor like nano or vim. In the top of the file, you should edit these variables:

```bash
# Default user/group when creating
# new directories for the web root
wwwroot_user="username"
wwwroot_group="group"

# Default paths
wwwroot="/var/www/"
apache_path="/etc/apache2"

```
Modify `wwwroot_user` and `wwwroot_group` to the user/group the webserver uses, or can read. Example: vagrant/vagrant, www-data/www-data or what ever works on your server.



## Usage:

Let's say we want to add a new vhost with the hostname: `example.com`.
This is what we would need to enter (always use sudo or as root since we need to write to Apache's folder):

```bash
sudo addvhost example.com

```

Thats it!

#### What it actually does

1. Creates a new vhost-config in `/etc/apache2/sites-available` called `example.com.conf`
2. Setting `example.com` as ServerName and log files to `/var/log/example.com-access.log` and `/var/log/example.com-error.log`
2. Creates document root `/var/www/example.com/public`
3. Enables the site `example.com.conf` using `a2ensite example.com`
4. Restarts Apache using `apache2ctl restart`

As you can see, it creates a subfolder called `public` in `/var/www/example.com`. You can change the name of that subfolder by sending in a second parameter when you create the vhost:
```bash
sudo addvhost example.com public_html
```
Now the document root will be: `/var/www/example.com/public_html` instead.

So there isn't much magic here. It just makes things a bit easier. :)


---

This was brought to you from someone who likes to make repetitive tasks less so...

Happy coding!

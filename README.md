# CLI-tool: Add Apache vhost in one line

This script makes it a bit easier to add a new Apache 2.4+ vhost on Ubuntu/Debian (or any other similar dists).
I built it for me and my colleagues to quickly be able to add new vhosts on our development servers.


## Installation

You can either get it from this repo or from:
```bash
wget http://dl.maer.se/cli/addvhost
```
This will always download the latest version (master).

Make the file executable and move it to `/usr/local/bin/`folder:
```bash
# Ubuntu example
sudo chmod +x addvhost
sudo mv addvhost /usr/local/bin/addvhost
```


## Configuration

There are a couple of settings you need to change before you get started.

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
Modify `wwwroot_user` and `wwwroot_group` to the user/group the webserver uses or can read. Example: vagrant/vagrant, www-data/www-data or whatever fits your servers environment.



## Usage:

Let's say we want to add a new vhost with the hostname: `example.com`.
All you need to do is run:

```bash
sudo addvhost example.com

```

Thats it!

#### What it actually does

1. Creates a new vhost called `example.com.conf`
2. Sets `example.com` as ServerName and the log files to `/var/log/example.com-access.log` and `/var/log/example.com-error.log`
2. Creates a document root called `/path/to/wwwroot/example.com/public`
3. Enables the site `example.com.conf` using `a2ensite example.com`
4. Restarts Apache using `apache2ctl restart`

As you can see, it creates a subfolder called `public` in `/path/to/wwwroot/example.com`. You can change the name of that subfolder by sending in a second parameter when you create the vhost:
```bash
sudo addvhost example.com serve_this_folder_instead
```
Now the document root will be: `/var/www/example.com/serve_this_folder_instead`.

So there isn't much magic here. It just makes things a bit easier. :)


---

This was brought to you from someone who likes to make repetitive tasks less so...

Happy coding!

# Using ddclient to update wireguard DNS records

using ddclient to update Cloudflare DNS on Raspberry Pi Dynamic DNS allows for a record to be automatically updated. These are the steps on how to configure ddclient on your Raspberry Pi.

Currently, all my domains are managed using Cloudflare. I wanted to use ddclient to update the IP addresses of my domains. These are the steps I followed.

```
sudo apt install ddclient
```

Go through the setup process, it does not really matter what you add as we will be chaning the config file.

For some reason not all the setup is done so running

```
sudo dpkg-reconfigure ddclient
```

will allow the rest of the setup to run, as mentioned before does not rally matter what options are used as we will be changeing the config file.

You can now change the configuration by changing the configuration file. Open this file using the editor.

```
sudo nano /etc/ddclient.conf
```

Delete what is in the configeration file and replace it with (updating "Update Me" sections with your info;

##
```
##
## [sub domain.top level doamin]- Cloudflare ## Update Me 
##
protocol=cloudflare
use=web
login=[CLOURDFLARE LOGIN EMAIL ADDRESS] ## Update Me
password=[CLOUDFLARE GLOBAL API KEY] ## Update Me
zone=[top level domain you want to change] ## Update Me
[sub domain.top level domain] ## Update Me
```
##

After making the necessary changes to the configuration file, restart the ddclient service in order for the changes to take effect.

```
sudo systemctl restart ddclient.service We can test our configuration by running the following command.
```

Now we can test that everything is workig with;
```
sudo ddclient -daemon=0 -verbose -noquiet
```

Somewhere near the bottom, you should see a line like this.

SUCCESS: [subdomain.topleveldomain -- Updated Successfully to ***********


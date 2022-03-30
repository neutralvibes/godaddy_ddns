# GODADDY DDNS UPDATER

## Introduction

Mapping your private networks public facing ip address to a domain name is a requirement many people have. If you have purchased a domain name from GoDaddy, this will easily allow you to keep a sub domain name pointing to that ip address without any additional cost. The only requirement otherwise is having a linux machine to schedule the updating from.

The script uses https://api64.ipify.org to identify your external ip address and checks it against the ip your chosen subdomain name is set to. If the differ it will update the subdomain address to the current value.


## Getting started

### Grab the code

```bash
git clone https://github.com/neutralvibes/godaddy_ddns.git
cd godaddy_ddns

# set execute bit
chmod +x ddns_updater on_change on_fail
```
### Get keys and secrets
1. Login to your GoDaddy account and go to https://developer.godaddy.com/getstarted.

2. Create your API Key and Secret for testing and live

3. Update the sections in the config file for you **keys**, **secrets**, main **domain name** and **sub domain** to be used.

### Set live or test mode?

At the bottom of the config file set `LIVE_MODE=1` to 0 to use the test api if required.

### Running

There are two modes `run` and `run-silent` which supresses messages.

```bash
./ddns_updater run
```
If it has worked you should see output similar to the following

```
Using LIVE mode: https://api.godaddy.com/v1/domains/your-domain.com/records
Checking for changes
Getting info for subdomain.your-domain.com from daddy url https://api.godaddy.com/v1/domains/your-domain.com/records
Get external ip from https://api64.ipify.org
subdomain.your-domain.com ip =  xxx.xxx.xxx.xxx
currentIp: xxx.xxx.xxx.xxx
```

### Ip change or failure notifications

There are two files `on_change` and `on_failure` whose names are self explanatory. You can edit these files to enable your desired action to take place on the condition the file name suggests. For instance, I use them to send a pushover message to my phone.


### Last of all

Once you have it working, setting up a cron job every 15 minutes or so should  keep things nicely in step.

## Credits

Special thanks to mfox for his ps script
https://github.com/markafox/GoDaddy_Powershell_DDNS

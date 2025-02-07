Ansible Paperbot
=========

An Ansible role to install paperbot on a server.  

See https://github.com/cppalliance/paperbot for the main codebase.  

Review the defaults/main.yml file which contains configurable variables. Those may generally stay unmodified except the following tokens which should be configured in host_vars:  

```
paperbot_slack_bot_token: 
paperbot_slack_signing_secret: 
```

To find the 'bot token', go to Settings (for this app) -> OAuth & Permissions -> OAuth Tokens -> Bot User OAuth Token  
https://api.slack.com/apps/_app_id_/oauth?

To find the 'signing secret', go to Basic Information -> App Credentials -> Signing Secret
 https://api.slack.com/apps/_app_id_/general?

Other important configuration:   

In the slack app settings, enable Event Subscriptions.  
https://api.slack.com/apps/_app_id_/event-subscriptions  
Set the Request URL (https://www.example.com/slack/events)  

Assuming an app name such as "apaperbot" the permission scope of the app should (at least) be something similar to this when creating the app in slack:    

```
channels:history
View messages and other content in public channels that apaperbot has been added to

chat:write
Send messages as @npaperbot

groups:history
View messages and other content in private channels that apaperbot has been added to

im:history
View messages and other content in direct messages that apaperbot has been added to

mpim:history
View messages and other content in group direct messages that apaperbot has been added to
```

Role Details:  

After install Passenger the following symlink should already exist -  

```
ln -s /usr/share/nginx/modules-available/mod-http-passenger.load /etc/nginx/modules-enabled/50-mod-http-passenger.conf
```

as well as the file -    

```
/etc/nginx/conf.d/mod-http-passenger.conf
```

## Let's Encrypt TLS Certificates

The role does not currently install certificates, however you should add them.  

After installing paperbot, run:   

```
certbot certonly
```

Install certs. Then run ansible a second time which will adjust the nginx vhost to use the new certs.  



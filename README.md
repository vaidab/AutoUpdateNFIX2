# AutoUpdateNFIX2
Python script that automates the update of the freqtrade strategy of NostalgiaForInfinityX2 (https://github.com/iterativv/NostalgiaForInfinity) and/or the blacklist and/or pairlist associated with your exchange.

## ⚡ How does it work?
The script checks the online and local version of the strategy and/or blacklist and/or pairlist.
There are 4 files available:
- update_strategy: update only the strategy
- update_strategy_blacklist: update of strategy and blacklist
- update_strategy_pairlist: update of strategy and pairlist
- update_strategy_blacklist_pairlist: update of the strategy, the blacklist and the pairlist
 
If there is a difference, it updates the local version, restarts the docker, and notifies the user on Telegram of the update.
<p align="center">
<img src="https://i.imgur.com/SgE3nYI.png"/></a>
</p>

## 🔧 Adapt the script
You have to modify the following variables with the path of your strategy, your blacklist/pairlist and your docker-compose.yml :
```
file = "/your-path/NostalgiaForInfinityX2.py"
file_blacklist = "/your-path/blacklist-kucoin.json"
file_pairlist = "/your-path/pairlist-volume-kucoin-usdt.json"
command = "cd your-docker-compose-path && /usr/bin/docker-compose restart"
```
You must also adapt the URL of the blacklist with the one adapted to your exchange :
```
url_blacklist = "https://raw.githubusercontent.com/iterativv/NostalgiaForInfinity/main/configs/blacklist-kucoin.json"
```
You must also enter your Telegram token and chat-id to receive notifications when updates are made:
```
bot_token = "6XXXXXXXXXXXXXXXXXXXXXXXX8U"
chat_id = "12XXXXX35"
```

## 📤 Automatically run the script :
###  🕖 With a cron:
Personally I want the script to be executed every hour to be updated as often as possible. To do this I run the following command on my server:
```
sudo crontab -e
```
And I add the following line:
```
15 * * * * /usr/bin/python3 /your-path/update_strategy.py >> /var/log/logs_update_strategy.log 2>&1
```
### 💻 With a script:
For people who don't have access to the cron of their server it is possible to use this script (provided by mandark of the NFI Discord/@Mandark-droid
):
```
 #!/bin/bash
while [ : ]
do
    dt=date +%d-%m-%y-%H:%M:%S
    echo "Last pole :" $dt
        cd /home/user/;python update_strategy_blacklist_pairlist.py >>log_update_strategy.log 2>&1
    sleep 600 ## Update this based on how frequently you want to run the script.
done
```
Save this as run_cron.sh and execute as :
```
nohup sh run_cron.sh &
```
## 🚀 Next developments:
- [x] Update the blacklist associated with his exchange and his crypto currency at the same time
- [x] Update the pairlist associated with his exchange and his crypto currency at the same time
- [ ] Automatic execution of the script at each commit of the NFI repo.

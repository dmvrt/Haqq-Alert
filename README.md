# Haqq-Alert
Haqq chain monitoring and alerting telegram bot
This telegram alerting will senв you a diffirient information about your validator ( jails, active/inactive status, missed blocks and others). Also it will send you every hour your node status.

Guide:

1. Create telegram bot via @BotFather, customize , get bot API token here: https://www.siteguarding.com/en/how-to-get-telegram-bot-api-token .

2. Create 2 groups in telegram and add your bot into the gropus: alarm and log. Then get chat ID with https://t.me/username_to_id_bot

3. Connect to your server and create status folder in the $HOME directory with mkdir $HOME/status/.

4. In this folder, $HOME/status/, you have to create cosmos.sh file with nano $HOME/status/cosmos.sh. You don't have to do any edits on haqq.sh file. cosmos.sh is in this repository.

5. In this folder, $HOME/status/, you have to create haqq.conf file with nano $HOME/status/haqq.conf. Customize it for your own.
Haqq.conf is in this repository.

6. Install some packages with sudo apt-get install jq sysstat bc smartmontools fdisk -y.

7.Run bash cosmos.sh to check your settings. Normal output:
root@htz-ax41:~/status# bash cosmos.sh
 
/// 2022-10-16 19:18:24 ///
 
haqq-contest  |  load

cpu_used >>>> 3%.
ram_used >>>> 22%.
part_used >>> 17%.
serv_load >>> 0.53.

disk_spare >> nvme0n1 has 100% spare.
disk_used >>> nvme0n1 has 3% used.
disk_spare >> nvme1n1 has 100% spare.
disk_used >>> nvme1n1 has 3% used.
 
haqq-contest  |  dmvrt

exp/me >>>>>> 526322/526322.
priv_key >>>> right.
place >>>>>>> 83/150.
stake >>>>>>> 11111.11 ISLM.
missed >>>>>> 0 blocks.
gov >>>>>>>>> no unvoted proposals.
upgrade >>>>> no.

8. Add some rules with chmod u+x $HOME/status/cosmos.sh.

9. Edit crontab with crontab -e.
# status
1,11,21,31,41,51 * * * * bash $HOME/status/cosmos.sh >> $HOME/status/cosmos.log 2>&1
Check your logs with cat $HOME/status/cosmos.log or tail $HOME/status/cosmos.log -f.

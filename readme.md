

<!-- sudo mkdir SCHEDTC_SCRIPT
cd /volume1/SCHEDTC_SCRIPT/
sudo cp /etc/tc/eth0.conf /volume1/SCHEDTC_SCRIPT/eth0.conf.slow
cd /volume1/SCHEDTC_SCRIPT/ -->
<!-- sudo cp /volume1/SCHEDTC_SCRIPT/eth0.conf.slow /volume1/SCHEDTC_SCRIPT/eth0.conf.fast -->

sudo chmod +x makefast.sh
sudo cp makefast.sh makeslow.sh

1. Create a normal traffic control rule (or multiple traffic control rules)
2. SSH into your Synology box
3. Create a directory in /volume1 (or wherever) called SCHEDTC_SCRIPT
4. CD into /etc/tc and copy the <dev>.conf rule to /volume1/SCHEDTC_SCRIPT/<dev>.conf.slow - where <dev> is the name of the network device on the Synology machine (eg.: eth0, eth1, bond0, etc.)
5. CD into /volume1/SCHEDTC_SCRIPT
6. Copy <dev>.conf.slow to <dev>.conf.fast
7. Edit <dev>.conf.fast changing the "maxrate" value of any/all of your rules to the higher limit you want (the values are exactly as you set them in the GUI)
8. Open vi to create the scrip with this cmd: 'vi makefast.sh'
9. Add the following three lines:
CODE: SELECT ALL

#!/bin/bash
cp /volume1/SCHEDTC_SCRIPT/<dev>.conf.fast /etc/tc/<dev>.conf
/usr/syno/bin/synotc_common restart
10. Then save and exit, and issue these commands back at the shell:
CODE: SELECT ALL

chmod +x makefast.sh
cp makefast.sh makeslow.sh
11. Then edit the "makeslow.sh" script substituting <dev>.conf.slow for <dev>.conf.fast
12. You can now use the GUI task scheduler to run /volume1/SCHEDTC_SCRIPT/makefast.sh to speed up the limit, and makeslow to slow it down.


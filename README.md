# VDR-EPG-LIST
Get only available channels that have <b>EPG</b> and print the result in a format of table ( <b>Channel name, epg title, Time, Duration, Elapsed</b> )

Put this code inside your <code>~/.bashrc</code> or create a bash script if you want:

<b>As a function inside ~/.bashrc:</b>

<code>EPG_LIST() {
(echo "Channel ==>  Title ==>Time ==>Duration==>Elapsed"
(paste -d">" <(grep -A4 "^C " /var/cache/vdr/epg.data | grep -B2 "^T " | grep "^C " |awk '{print substr($0, index($0,$3))}') \
<(grep -A4 "^C " /var/cache/vdr/epg.data | grep "^T ") \
<br>
<(for ts in $(grep -A4 "^C " /var/cache/vdr/epg.data | grep -B2 "^T " | grep "^E " |awk '{print $3}'); do date -d @$ts +%H:%M; done) \
<(for ts in $(grep -A4 "^C " /var/cache/vdr/epg.data | grep -B2 "^T " | grep "^E " |awk '{print $4}'); do date -d @$ts +%H:%M; done) \
<(for ts in $(grep -A4 "^C " /var/cache/vdr/epg.data | grep -B2 "^T " | grep "^E " |awk '{print $2}'); do date -d @$ts +%H:%M; done) \
 | sed 's/>T/==> /g')|sort) | column -t -s "==\>"
}</code><br><br>
<b>As a <code>Bash</code> script:</b><br><br>
<code>#!/bin/bash</code>
<br>
<code># Simple epg list by karirovax </code>
<br>
<code>(echo "Channel ==>  Title ==>Time ==>Duration==>Elapsed"
(paste -d">" <(grep -A4 "^C " /var/cache/vdr/epg.data | grep -B2 "^T " | grep "^C " |awk '{print substr($0, index($0,$3))}') \
<(grep -A4 "^C " /var/cache/vdr/epg.data | grep "^T ") \
<(for ts in $(grep -A4 "^C " /var/cache/vdr/epg.data | grep -B2 "^T " | grep "^E " |awk '{print $3}'); do date -d @$ts +%H:%M; done) \
<(for ts in $(grep -A4 "^C " /var/cache/vdr/epg.data | grep -B2 "^T " | grep "^E " |awk '{print $4}'); do date -d @$ts +%H:%M; done) \
<(for ts in $(grep -A4 "^C " /var/cache/vdr/epg.data | grep -B2 "^T " | grep "^E " |awk '{print $2}'); do date -d @$ts +%H:%M; done) \
 | sed 's/>T/==> /g')|sort) | column -t -s "==\>"</code><br><br>
<b>PS:</b> This is my first use of github, i like to share anything that can help any user ( English is not my native language )<br>
 
 Enjoy it! :)

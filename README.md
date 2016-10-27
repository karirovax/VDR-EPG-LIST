# VDR-EPG-LIST
Get only available channels that have epg and print the result in a format of table ( channel name, epg title, begin time )

Put this code inside your ~/.bashrc or create a bash script if you want:

<b>As a function inside ~/.bashrc:</b>

EPG_LIST() {
paste -d">" <(grep -A4 "^C " /var/cache/vdr/epg.data | grep -B2 "^T " | grep "^C " |awk '{print substr($0, index($0,$3))}') \
<(grep -A4 "^C " /var/cache/vdr/epg.data | grep "^T ") \
<(for ts in $(grep -A4 "^C " /var/cache/vdr/epg.data | grep -B2 "^T " | grep "^E " |awk '{print $3}'); do date -d @$ts +%H:%M; done) \
 | sed 's/>T/ ==> /g' | column -t -s "==\>"
}

<b>As a bash script:</b>

<code>#!/bin/bash</code>

<code># Simple epg list by karirovax </code>

<code>paste -d">" <(grep -A4 "^C " /var/cache/vdr/epg.data | grep -B2 "^T " | grep "^C " |awk '{print substr($0, index($0,$3))}') \
<(grep -A4 "^C " /var/cache/vdr/epg.data | grep "^T ") \
<(for ts in $(grep -A4 "^C " /var/cache/vdr/epg.data | grep -B2 "^T " | grep "^E " |awk '{print $3}'); do date -d @$ts +%H:%M; done) \
 | sed 's/>T/ ==> /g' | column -t -s "==\>"</code>

<b>PS:</b> This is my first use of github, i like to share anything that can help any user ( English is not my native language )
 
 Enjoy it! :)

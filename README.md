# VDR-EPG-LIST
Get only available channels that have <b>EPG</b> and print the result in a format of table ( <b>Channel name, epg title, Time, Duration, Elapsed</b> )

Put this code inside your <code>~/.bashrc</code> or create a bash script if you want:

<b>As a function inside ~/.bashrc:</b>
<pre>
<code>EPG_LIST() {
echo " "
echo -e "\t\t\e[1;32;100mN°. \e[1;101m Chaîne          \e[44m Titre                        \e[1;32;100m Temps \e[43m Durée   \e[45m Passé \e[0m"
((paste -d">" <(grep -A4 "^C " /var/cache/vdr/epg.data | grep -B2 "^T " | grep "^C " |awk '{printf "\t\t\033[1;32;100m%02d  \033[0m\n", NR}') \
<br>
<(grep -A4 "^C " /var/cache/vdr/epg.data | grep -B2 "^T " | grep "^C " |awk '{print substr($0, index($0,$3))}') \
<(grep -A4 "^C " /var/cache/vdr/epg.data | grep "^T "| cut -c1-29) \
<(for ts in $(grep -A4 "^C " /var/cache/vdr/epg.data | grep -B2 "^T " | grep "^E " |awk '{print " "$3}'); do date -d @$ts +%H:%M; done) \
<(for ts in $(grep -A4 "^C " /var/cache/vdr/epg.data | grep -B2 "^T " | grep "^E " |awk '{print " "$4}'); do date -d @$ts +"%H:%M  "; done) \
<(for ts in $(grep -A4 "^C " /var/cache/vdr/epg.data | grep -B2 "^T " | grep "^E " |awk '{print " "$2}'); do date -d @$ts +"%H:%M  "; done) \
 | sed 's/>T/==>/g')| sort -n) | column -t -s "==\>"
 echo -e "\t\t\e[1;32;100m    \e[1;101m                 \e[44m                              \e[1;32;100m       \e[43m         \e[45m       \e[0m"
echo " "
}</code></pre><br><br>
<b>As a <code>Bash</code> script:</b><br><br>
<code>#!/bin/bash</code>
<br>
<code># Simple epg list by karirovax </code>
<br>
<pre><code>echo " "
echo -e "\t\t\e[1;32;100mN°. \e[1;101m Chaîne          \e[44m Titre                        \e[1;32;100m Temps \e[43m Durée   \e[45m Passé \e[0m"
((paste -d">" <(grep -A4 "^C " /var/cache/vdr/epg.data | grep -B2 "^T " | grep "^C " |awk '{printf "\t\t\033[1;32;100m%02d  \033[0m\n", NR}') \
<(grep -A4 "^C " /var/cache/vdr/epg.data | grep -B2 "^T " | grep "^C " |awk '{print substr($0, index($0,$3))}') \
<(grep -A4 "^C " /var/cache/vdr/epg.data | grep "^T "| cut -c1-29) \
<(for ts in $(grep -A4 "^C " /var/cache/vdr/epg.data | grep -B2 "^T " | grep "^E " |awk '{print " "$3}'); do date -d @$ts +%H:%M; done) \
<(for ts in $(grep -A4 "^C " /var/cache/vdr/epg.data | grep -B2 "^T " | grep "^E " |awk '{print " "$4}'); do date -d @$ts +"%H:%M  "; done) \
<(for ts in $(grep -A4 "^C " /var/cache/vdr/epg.data | grep -B2 "^T " | grep "^E " |awk '{print " "$2}'); do date -d @$ts +"%H:%M  "; done) \
 | sed 's/>T/==>/g')| sort -n) | column -t -s "==\>"
 echo -e "\t\t\e[1;32;100m    \e[1;101m                 \e[44m                              \e[1;32;100m       \e[43m         \e[45m       \e[0m"
echo " "</code></pre><br><br>
<b>PS:</b> This is my first use of github, i like to share anything that can help any user ( English is not my native language )<br>
 
 Enjoy it! :)

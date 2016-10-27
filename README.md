# VDR-EPG-LIST
get only available channels that have epg and print the result in a format of table ( channel name, epg title, begin time )

put this code inside your ~/.bashrc or create a bash script if you want:


EPG_LIST() {
paste -d">" <(grep -A4 "^C " /var/cache/vdr/epg.data | grep -B2 "^T " | grep "^C " |awk '{print substr($0, index($0,$3))}') \
<(grep -A4 "^C " /var/cache/vdr/epg.data | grep "^T ") \
<(for ts in $(grep -A4 "^C " /var/cache/vdr/epg.data | grep -B2 "^T " | grep "^E " |awk '{print $3}'); do date -d @$ts +%H:%M; done) \
 | sed 's/>T/ ==> /g' | column -t -s "==\>"
}

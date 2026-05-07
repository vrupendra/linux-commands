# linux-commands
linus commands

df -Ph . | awk 'NR==2 {print $4}'
disk cleanup of old snap packages
LANG=C snap list --all | awk '/disabled/{print $1, $3}' | while read snapname revision; do sudo snap remove "$snapname" --revision="$revision"; done
sudo apt autoclean
sudo sh -c 'rm -rf /var/lib/snapd/cache/*'
sudo snap set system refresh.retain=2

disk utilization 
sudo time du -hc --max-depth=1 /var |sort -rh -k1  [ r - reverse order, k - sort field/column, h - human readable and by size ] 


getent passwd devops | awk -F: '{ print $6 }'

http serve 
sudo python3 -m http.server 80

sudo lastb

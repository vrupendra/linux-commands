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

create a user without home directory
sudo useradd -M julie
-M do not create home directory

Create Service account / application account

Often do not set a password and optionally prevent interactive login:

$ sudo useradd -M -s /sbin/nologin username

delete user
sudo userdel julie   -> this will only removes users entry from /etc/passwd, /etc/shadow, /etc/group . it will not delete user's home directory or the users mailbox which is located at /var/spool/mail/username | /var/mail/username

delete user along with its home directory and mailbox 

sudo userdel -r julie

$ create a user with expiry 2027-01-05 - THIS IS NOT PASSWD EXPIRY. ITS ACCOUNT EXPIRY

sudo useradd -m -e 2025-01-05 julie

id julie
sudo chage -l julie

If the user already exists:
sudo usermod -e 2027-01-01 john

To remove the expiration date completely:
sudo usermod -e "" john
or
sudo chage -E -1 john    --> Capital E - remove expiry

chage -l username      # View password aging
chage -M 90 username   # Set password expiry
chage -d 0 username    # Force password reset at next login
chage -E YYYY-MM-DD username  # Set account expiry

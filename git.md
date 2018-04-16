# Git
## list existing keys
```
ls -al  ~/.ssh
```

## Add SSH Key
```
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

## Start SSH agent and add key
```
eval $(ssh-agent -s)
ssh-add ~/.ssh/id_rsa
```

## Add key to git
copy the contents of your public key to the clipboard:
```
clip < ~/.ssh/id_rsa.pub
```
then go to your own profile page...
click your profile icon |  your profile | edit profile | SSH and GPG keys | click 'new ssh key'

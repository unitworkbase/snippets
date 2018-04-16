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



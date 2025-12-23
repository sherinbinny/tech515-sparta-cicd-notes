## Commands used

```
 1027  eval `ssh-agent -s`
 1028  ssh-add sherin-github-key
 1029  ssh -T git@github.com
 1030  cd
 1031  cd github
 1032  cd Documents/github
 1033  ls
 1034  git clone git@github.com:sherinbinny/test-ssh2.git
 1035  ls
 1036  cd test-ssh2
 1037  ls
 1038  cat README.md
 1039  nano README.md
 1040  git add .
 1041  git commit -m "update readme"
 1042  git push
```

# to create a new key

```
 1045  cd /Users/sherinbinny/.ssh
 1046  ssh-keygen -t rsa -b 4096 -C "sherinbinny@gmail.com"
 1047  ls
 1048  cat sherin-jenkins-2-github-key.pub
```

![Scrrenshot of create key](images/create-key.png)

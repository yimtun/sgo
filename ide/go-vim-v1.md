```
yum remove vim-* -y
wget http://mirror.ghettoforge.org/distributions/gf/gf-release-latest.gf.el7.noarch.rpm
rpm -ivh gf-release-latest.gf.el7.noarch.rpm
yum --enablerepo=gf-plus install vim-enhanced
```



```
[gf-plus]
name=Ghettoforge packages that will overwrite core distro packages.
mirrorlist=http://mirrorlist.ghettoforge.org/el/7/plus/$basearch/mirrorlist
# Please read http://ghettoforge.org/index.php/Usage *before* enabling this repository!
enabled=0
gpgcheck=0
```




```
curl -fLo ~/.vim/autoload/plug.vim --create-dirs   https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
git clone https://github.com/fatih/vim-go.git  /root/.vim/plugged/vim-go
```





```
cat > /root/.vimrc << EOF
call plug#begin()
Plug 'fatih/vim-go'
call plug#end()
EOF
```


```
mkdir  -p $GOPATH/src/golang.org/x/
```

```
git clone https://github.com/golang/tools.git         /opt/go/src/golang.org/x/tools
```


```
git clone https://github.com/golang/lint.git          /opt/go/src/golang.org/x/lint
```

```
git clone https://github.com/golang/sync.git          /opt/go/src/golang.org/x/sync
```



```
go install golang.org/x/tools/cmd/guru
go install golang.org/x/lint/golint
go install golang.org/x/tools/go/packages
go install golang.org/x/tools/cmd/gorename
go install golang.org/x/tools/cmd/goimports
go install golang.org/x/tools/gopls
```

```
go  install github.com/bhcleek/lsp-position/cmd/lsp-position
go  install github.com/golangci/golangci-lint/cmd/golangci-lint
```





```
vim  +GoInstallBinaries
```




# 开启代理
# 配置终端开启代理命令2
```
# 代理配置

function p_on() {

    export http_proxy=http://127.0.0.1:7897

    export https_proxy=$http_proxy

    echo -e "终端代理已开启。"

}

function p_off(){

    unset http_proxy https_proxy

    echo -e "终端代理已关闭。"

}

```
# 开启代理

```
p_on
```

# 安装nvm

执行命令 brew reinstall nvm

配置.zshrc文件
```
export NVM_DIR="$HOME/.nvm"
[ -s "$(brew --prefix nvm)/nvm.sh" ] && \. "$(brew --prefix nvm)/nvm.sh"  # This loads nvm
[ -s "$(brew --prefix nvm)/bash_completion" ] && \. "$(brew --prefix nvm)/bash_completion"  # This loads nvm bash_completion
```


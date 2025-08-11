# 开启代理
# 配置终端开启代理命令
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

# 开启自动开启SSH

**打开终端，编辑（或创建）SSH 配置文件：**`nano ~/.ssh/config`

添加以下内容：
```
Host *
	AddKeysToAgent yes
	UseKeychain yes
	IdentityFile ~/.ssh/id_rsa`
```
- `AddKeysToAgent yes` ：每次使用该密钥时自动加入代理
- `UseKeychain yes` ：把密钥存进 macOS 钥匙串，实现自动加载
- `IdentityFile` ：你的私钥路径，改成你自己的文件名

**把密钥添加到 ssh-agent 并存进钥匙串（只需执行一次）：**

`ssh-add --apple-use-keychain ~/.ssh/id_rsa`
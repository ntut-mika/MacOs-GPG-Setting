# MacOS GPG Setting
在 MacOs 上為 git commit 紀錄添加 gpg 簽章

### Step 1 安裝軟體
```sh
brew install gnupg pinentry-mac 
```

### Step 2 創建目錄
```sh
mkdir ~/.gnupg
echo "pinentry-program $(brew --prefix)/bin/pinentry-mac" > ~/.gnupg/gpg-agent.conf
```

### Step 3: 更新或創建 ~/.gnupg/gpg.conf
```sh
echo 'use-agent' > ~/.gnupg/gpg.conf
```

### Step 4: 修改 ~/.zshrc
```txt
...
export GPG_TTY=$(tty)
```
### Step 5: 重開 terminal

### Step 6: 修改權限
```sh
chmod 700 ~/.gnupg
```
### Step 7: 關閉 gpg-agent
```sh
killall gpg-agent
```

### Step 8: 創建 GPG Key
```sh
gpg --full-gen-key
```
### Step 9: 回答問題
1. 選擇 RSA (sign only)
2. 輸入 4096
3. 輸入 0
4. 輸入 y 確認
5. 真實姓名輸入你 github 名稱
6. 電子郵件地址輸入你 github 信箱
7. 註釋不用填直接 enter
8. 輸入 O 確認
9. 密碼可以不用填
    
## Step 10: 取得 key id
```sh
gpg -K --keyid-format SHORT
```

```txt
sec   rsa4096/######## 2022-07-17 [SC]
      C23B0710A84EE9C19B4EB623B4560A801AFE863F
uid         [ultimate] ntut-mika <t107590003@ntut.org.tw>
```


## Step 11: 輸出公鑰並貼到 github 上
```sh
gpg -armor --export ########
```

## Step 12: 設定 git
```sh
git config --global gpg.program $(which gpg)
git config --global user.signingkey ########
git config --global commit.gpgsign true
git config --global tag.gpgSign true
```

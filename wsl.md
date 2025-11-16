# WSL

## リセット

### WSL のリセット後の起動エラー

```text
... を WSL2 にアタッチできませんでした: 指定されたファイルが見つかりません。
エラー コード: Wsl/Service/CreateInstance/MountDisk/HCS/ERROR_FILE_NOT_FOUND
```

上記が表示される場合、コマンドプロンプトで以下を実行

```shell
wsl -l -v
wsl --unregister Ubuntu-24.04
# 対象のWSL名を指定する
```

## Visual Studio Code

```shell
echo 'alias code="'\'''`which code`''\''"' >> .bashrc
source ~/.bashrc
```

---

## Git

### インストールの確認

Ubuntu では既にインストール済み

```shell
which git
# -> /usr/bin/git
```

### .gitconfig 設定

```shell
vi ~/.gitconfig
```

```text
[core]
  autocrlf = false
  safecrlf = false
[user]
  name = [name]
  email = [email]
[init]
  defaultBranch = main
```

---

## Python

### uv

```shell
curl -LsSf https://astral.sh/uv/install.sh | sh
source $HOME/.local/bin/env
uv python install 3.14 3.13 3.12 3.11 3.10 3.9
```

---

## Docker

```shell
curl -fsSL https://get.docker.com -o get-docker.sh
sh get-docker.sh
rm get-docker.sh

# sudoなしで使用できるようにする
sudo usermod -aG docker $USER

docker --version
docker compose version
```

---

## Postgresql

### インストール

```shell
sudo apt update
sudo apt install postgresql postgresql-contrib
```

### パスワード認証の設定

```shell
sudo vi /etc/postgresql/16/main/pg_hba.conf
# 「16」はインストールしたバージョンに合わせる
```

以下の通り編集

```text
# local   all             all                                     peer
local   all             all                                     md5
```

```shell
sudo service postgresql restart
```

### ロール・データベース作成

```shell
sudo -u postgres -i

psql

create role testuser with login password 'testuser';
create database testdb with owner testuser;
```

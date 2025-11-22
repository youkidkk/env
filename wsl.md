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
# ※対象のWSL名を指定する
```

---

## Git

### インストールの確認

Ubuntu 24.04 では既にインストール済み

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
uv --version

# Python の各バージョンをインストール
uv python install 3.14 3.13 3.12 3.11 3.10 3.9
```

---

## Docker

```shell
curl -fsSL https://get.docker.com | sh

# sudoなしで使用できるようにする
sudo usermod -aG docker $USER

# 以下、バージョンが表示されることを確認
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

### パスワード認証の確認

```shell
sudo vi $(sudo find /etc -name pg_hba.conf)
```

以下の行を確認

```text
host    all             all             127.0.0.1/32            scram-sha-256
```

```shell
# サービス再起動
sudo service postgresql restart
```

### ロール・データベース作成

```shell
sudo -u postgres -i

psql

create role testuser with login password 'testuser';
create database testdb with owner testuser;
```

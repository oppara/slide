# Vagrant について 

コマンドとかプラグインとか

---

## Version


### 1.8.6  

https://www.vagrantup.com/downloads.html

最近バージョンアップしたばっか

https://github.com/mitchellh/vagrant/commit/70d3c1fa2c933e88c27c4777709e479fc87842d5

---

## vagrant global-status

https://www.vagrantup.com/docs/cli/global-status.html

- VM の一覧と状態を表示
- 以前あったプラグインではなく vagrant 自体のコマンド

___

## 実行結果

```
$ vagrant global-status
id       name    provider   state   directory
-----------------------------------------------------------------------------------------------
a918be2  default virtualbox running /Users/oppara/sandbox/foo/repo
9e379a7  default virtualbox aborted /Users/oppara/sandbox/bar/repo/vagrant
59d8113  default virtualbox running /Users/oppara/sandbox/baz/repo/vagrant
a33a1ec  default virtualbox running /Users/oppara/sandbox/hoge/repo/vagrant

The above shows information about all known Vagrant environments
on this machine. This data is cached and may not be completely
up-to-date. To interact with any of the machines, you can go to
that directory and run Vagrant, or you can use the ID directly
with Vagrant commands from any directory. For example:
"vagrant destroy 1a2b3c4d"
```


---

## dotenv

https://github.com/bkeepers/dotenv

- 環境変数を変更設定してくれる Gem
- 元ネタは Ruby. 
- PHP(Laravelでも使われている), Perl, Python 版あり 
- E2 の Vagrantfile で使ってる

___

## E2 の Vagrantfile の場合

<strong>:private_network のIPアドレスの設定に使ってます</strong>

<br/>

とりあえず、インストールしとく

```
$ vagrant plugin install dotenv
```

___

Vagrantfile のあるディレクトリで、以下の .env ファイルを作成する

```
VAGRANT_IP_ADDRESS = '192.168.100.100'
```

で `vagrant up` すると、

Vagrantfileで設定されたIPアドレスではなく、

.env で設定されたIPアドレスが、:private_network に使用されます。

___

## 何がうれしいの？


---

## vagrant-hostsupdater

https://github.com/cogitatio/vagrant-hostsupdater

- ホストOSの hosts 設定をしてくれるプラグイン
- WebPiece の Vagrantfile で使ってる

___

## 設定

Vagrantfileに以下の設定をして `vagrant up` すると

(hostname と :private_network の設定は必須)

``` ruby:Vagrantfile
config.vm.network :private_network, ip: "192.168.3.10"
config.vm.hostname = "www.example.com"
if Vagrant.has_plugin?("vagrant-hostsupdater")
  config.hostsupdater.aliases = ["foo.example.com", "bar.example.com"]
end
```

hosts に以下の設定をしてくれる

```
192.168.3.10 www.example.com
192.168.3.10 foo.example.com
192.168.3.10 bar.example.com
```

`suspend`, `halt` すると hosts から削除してくれる

`destroy` は？

___

## Passwordless sudo

ファイル書き込み時にパスワード入力を求められる時は、  

`sudo visudo` で以下を設定

```sh
# Allow passwordless startup of Vagrant with vagrant-hostsupdater.
Cmnd_Alias VAGRANT_HOSTS_ADD = /bin/sh -c echo "*" >> /etc/hosts
Cmnd_Alias VAGRANT_HOSTS_REMOVE = /usr/bin/env sed -i -e /*/ d /etc/hosts
%admin ALL=(root) NOPASSWD: VAGRANT_HOSTS_ADD, VAGRANT_HOSTS_REMOVE
```

もしくは /etc/hosts のパーミッションを変えちゃう

```
$ ls -l /etc/hosts
-rw-r--r--  1 root  wheel   240B Mar 24  2016 /etc/hosts

$ sudo chmod g+w /etc/hosts

$ ls -l /etc/hosts
-rw-rw-r--  1 root  wheel   240B Mar 24  2016 /etc/hosts
```


---

## まとめ

他にも良さげなコマンドあったりするので

(`package`, `powershell`, `snapshot` とか)

たまにはヘルプをみるべし

```
$ vagrant help
```



___

## 以上

<https://slideck.io/github.com/oppara/slides/vagrant/recent_2016.md>

Check out Slideck now!

<https://slideck.io/>


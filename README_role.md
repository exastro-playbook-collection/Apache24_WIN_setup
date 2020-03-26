# Ansible Role: Apache24_WIN\_setup

## Description
本Ansble RoleはWebサーバソフトウェアである"Apache HTTP Server"の初期設定を行います。
対象バージョンは以下のバージョンです。

- Apache2.4 (Apache Launge版)

以下のファイルを設定します。
- C:\Apache24\conf\httpd.conf
- C:\Apache24\conf\extra\httpd-default.conf
- C:\Apache24\conf\extra\httpd-info.conf
- C:\Apache24\conf\extra\httpd-mpm.conf
- C:\Apache24\conf\extra\proxy.conf
  * Apache インストール先が「C:\Apache24」の場合

## Supports

- 管理マシン(Ansibleサーバ)
  * Linux系OS（RHEL/CentOS）
  * Ansible バージョン 2.3 以上 (動作確認済みバージョン：2.4、2.9)
  * Python バージョン 2.x、3.x  (動作確認済みバージョン：2.6、2.7、3.6)


- 管理対象マシン(インストール対象マシン)
  - Windows Server 2016
  - PowerShell 5.0

## Requirements

- 管理マシン(Ansibleサーバ)
  - 管理対象マシンへ	WinRM接続できること
  - WinRM接続設定は次のサイトを参考にすること
    - http://docs.ansible.com/ansible/intro_windows.html#windows-system-prep


- 管理対象マシン(インストール対象マシン)
  - Apache Launge版 Apache 2.4 がインストールされていること
  - PowerShell 5.0を利用できること
  - ファイアフォールが適切に設定されていること

## Role Variables

Role の変数値について説明します。

### Mandatory variables

以下の変数は必ず指定します。

- WinRM設定（group_varsもしくはhost_varsに設定）
  * ''ansible_user'': ユーザ名(string)
  * ''ansible_password'': パスワード(string)
  * ''ansible_port'': ポート(number)
  * ''ansible_connection'': 接続方式(string)
  * ''ansible_winrm_server_cert_validation'': 暗号化有無(string)

### Optional variables

以下の変数は任意で指定します。

- 基本設定
   + ''VAR_Apache24_WIN_path'': Apacheインストール先ディレクトリ(string, default:"C:\Apache24")


- 設定ファイル「httpd.conf」
  * ''VAR_Apache24_WIN_Http'': 設定ファイル「httpd.conf」を更新するか(on|off, default: "on")
    + off を指定した場合は、設定ファイル「httpd.conf」の更新は行われません。
  * ''VAR_Apache24_WIN_Http_ServerRoot'': ServerRoot(string, default: "C:/Apache24")
  * ''VAR_Apache24_WIN_Http_Listen'': Listen(number, default: "80")
  * ''VAR_Apache24_WIN_Http_ServerAdmin'': ServerAdmin(string, default: "admin@localhost")
  * ''VAR_Apache24_WIN_Http_ServerName'': ServerName(string, default: "")
  * ''VAR_Apache24_WIN_Http_DocumentRoot'': DocumentRoot(string, default: "C:/Apache24/htdocs")
  * ''VAR_Apache24_WIN_Http_DirectoryIndex'': DirectoryIndex(string, default: "index.html index.html.var")
  * ''VAR_Apache24_WIN_Http_TypesConfig'': TypesConfig(string, default: "conf/mime.types")
  * ''VAR_Apache24_WIN_Http_AddDefaultCharset'': AddDefaultCharset(string, default: "UTF-8")
  * ''VAR_Apache24_WIN_Http_MIMEMagicFile'': MIMEMagicFile(string, default: "")
  * ''VAR_Apache24_WIN_Http_ErrorLog'': ErrorLog(string, default: "log/error_log")
  * ''VAR_Apache24_WIN_Http_LogLevel'': LogLevel(string, default: "warn")
  * ''VAR_Apache24_WIN_Http_LogFormat'': LogFormat(string, default: "")
    + 設定値には「'」を付与してください。(例:' "%h %l %u %t \"%r\" %>s %b" common ')
  * ''VAR_Apache24_WIN_Http_LogFormat_IO'': LogFormat(string, default: "")
    + 設定値には「'」を付与してください。(例:' "%h %l %u %t \"%r\" %>s %b" common ')
    + IO関連オプション（「%I」,「%O」）を指定することができます。
    + mod_log_config  モジュールが必要です。
  * ''VAR_Apache24_WIN_Http_CustomLog'': CustomLog(string, default: "logs/access_log combined")
  * ''VAR_Apache24_WIN_Http_EnableMMAP'': EnableMMAP("On"|"Off", default: "On")
  * ''VAR_Apache24_WIN_Http_EnableSendfile'': EnableSendfile("On"|"Off", default: "On")


- 設定ファイル「httpd-default.conf」
  * ''VAR_Apache24_WIN_Default'': 設定ファイル「httpd-default.conf」を更新するか(on|off, default: "off")
    + off を指定した場合は、設定ファイル「httpd-default.conf」の更新は行われません。
    + on を指定した場合は、httpd.conf ファイルに「Include conf/extra/httpd-default.conf」行が追加されます。
    （VAR_Apache24_WIN_Httpがonの場合）
  * ''VAR_Apache24_WIN_Default_ServerTokens'': ServerTokens(string, default: "Prod")
  * ''VAR_Apache24_WIN_Default_Timeout'': Timeout(number, default: "")
  * ''VAR_Apache24_WIN_Default_KeepAlive'': KeepAlive(on|off, default: "")
  * ''VAR_Apache24_WIN_Default_MaxKeepAliveRequests'': MaxKeepAliveRequests(number, default: "")
  * ''VAR_Apache24_WIN_Default_KeepAliveTimeout'': KeepAliveTimeout(number, default: "")
  * ''VAR_Apache24_WIN_Default_UseCanonicalName'': UseCanonicalName(on|off, default: "")
  * ''VAR_Apache24_WIN_Default_AccessFileName'': AccessFileName(string, default: ".htaccess")
  * ''VAR_Apache24_WIN_Default_MaxKeepAliveRequests'': MaxKeepAliveRequests(number, default: "")
  * ''VAR_Apache24_WIN_Default_HostnameLookups'': HostnameLookups(string, default: "")
  * ''VAR_Apache24_WIN_Default_ServerSignature'': ServerSignature(on|off, default: "")
  * ''VAR_Apache24_WIN_Default_RequestReadTimeout'': RequestReadTimeout(string, default: "'header=20-40,MinRate=500 body=20,MinRate=500'")


- 設定ファイル「httpd-info.conf」
  * ''VAR_Apache24_WIN_Info'': 設定ファイル「httpd-info.conf」を更新するか(on|off, default: "off")
    + off を指定した場合は、設定ファイル「httpd-info.conf」の更新は行われません。
    + on を指定した場合は、httpd.conf ファイルに「Include conf/extra/httpd-info.conf」行が追加されます。
    （VAR_Apache24_WIN_Httpがonの場合）
  * ''VAR_Apache24_WIN_Info_ExtendedStatus'': ExtendedStatus(on|off, default: "off")
  * ''VAR_Apache24_WIN_Info_ServerStatus'': ServerStatusを有効にするか(on|off, default: "off")
  * ''VAR_Apache24_WIN_Info_ServerStatus_Location'': ServerStatusのアクセスURL(string, default: "/server-status")
  * ''VAR_Apache24_WIN_Info_ServerStatus_Require'': ServerStatusのRequire設定(RequireAll|RequireAny, default: "RequireAny")
    + [RequireAll]を指定した場合、Requireディレクティブは、<RequireAll>内に設定されます。
    + [RequireAny]を指定した場合、Requireディレクティブは、<RequireAny>内に設定されます。
    + 空白を指定した場合は、Requireディレクティブは、<RequireAll>や<RequireAny>の中には設定されません。
  * ''VAR_Apache24_WIN_Info_ServerStatus_RequireResource'': Require(string[], default: "'["host .example.com","ip 127"]'")
    + Requireディレクティブに設定する内容を指定します。配列形式で複数設定することができます。


- 設定ファイル「httpd-mpm.conf」
  * ''VAR_Apache24_WIN_MPM'': 設定ファイル「httpd-mpm.conf」を更新するか(on|off, default: "off")
    + off を指定した場合は、設定ファイル「httpd-mpm.conf」の更新は行われません。
    + on を指定した場合は、httpd.conf ファイルに「Include conf/extra/httpd-mpm.conf」行が追加されます。
    （VAR_Apache24_WIN_Httpがonの場合）
  * ''VAR_Apache24_WIN_MPM_ThreadsPerChild'': ThreadsPerChild(number, default: "64")
  * ''VAR_Apache24_WIN_MPM_MaxConnectionsPerChild'': MaxConnectionsPerChild(number, default: "0")
  * ''VAR_Apache24_WIN_MPM_AcceptFilter'': AcceptFilter(string[], default: "")
    + 配列形式で複数の値を指定可能
  * ''VAR_Apache24_WIN_MPM_MaxMemFree'': MaxMemFree(number, default: "2048")


- Tomcat連携設定ファイル「proxy.conf」
  * ''VAR_Apache24_WIN_Proxy'': ProxyPass(on|off, default: "off")
    + Tomcat連携ディレクティブを有効にするためには、"on"を指定します。
    + デフォルトもしくは、"off"を指定した場合は、Tomcat連携ディレクティブが有効になりません。
    + on を指定した場合は、httpd.conf ファイルに次の行が追加されます。（VAR_Apache24_WIN_Httpがonの場合）
      - LoadModule proxy_module modules/mod_proxy.so
      - LoadModule proxy_ajp_module modules/mod_proxy_ajp.so
      - LoadModule proxy_balancer_module modules/mod_proxy_balancer.so
      - LoadModule proxy_connect_module modules/mod_proxy_connect.so
      - LoadModule proxy_express_module modules/mod_proxy_express.so
      - LoadModule proxy_fcgi_module modules/mod_proxy_fcgi.so
      - LoadModule proxy_ftp_module modules/mod_proxy_ftp.so
      - LoadModule proxy_hcheck_module modules/mod_proxy_hcheck.so
      - LoadModule proxy_html_module modules/mod_proxy_html.so
      - LoadModule proxy_http_module modules/mod_proxy_http.so
      - LoadModule proxy_http2_module modules/mod_proxy_http2.so
      - LoadModule proxy_scgi_module modules/mod_proxy_scgi.so
      - LoadModule proxy_wstunnel_module modules/mod_proxy_wstunnel.so
      - LoadModule slotmem_shm_module modules/mod_slotmem_shm.so
      - LoadModule watchdog_module modules/mod_watchdog.so
      - LoadModule lbmethod_byrequests_module modules/mod_lbmethod_byrequests.so
      - LoadModule xml2enc_module modules/mod_xml2enc.so
  * ''VAR_Apache24_WIN_ProxyPass'': ProxyPass(string[], default: "["/ ajp://localhost:8009/"]")
    + 配列形式で複数の値を指定可能
  * ''VAR_Apache24_WIN_ProxyPassReverse'': ProxyPassReverse(string[], default: "["/ ajp://localhost:8009/"]")
    + 配列形式で複数の値を指定可能
  * ''VAR_Apache24_WIN_ProxyPassReverseCookieDomain'': ProxyPassReverseCookieDomain(string[], default: "")
  * ''VAR_Apache24_WIN_ProxyPassReverseCookiePath'': ProxyPassReverseCookiePath(string[], default: "")
  * ''VAR_Apache24_WIN_ProxyPassMatch'': ProxyPassMatch(string[], default: "")
    + 配列形式で複数の値を指定可能
  * ''VAR_Apache24_WIN_ProxySet'': ProxySet(string, default: "")
  * ''VAR_Apache24_WIN_ProxyBadHeader'': ProxyBadHeader(string, default: "")
  * ''VAR_Apache24_WIN_ProxyBlock'': ProxyBlock(string, default: "")
  * ''VAR_Apache24_WIN_ProxyDomain'': ProxyDomain(string, default: "")
  * ''VAR_Apache24_WIN_ProxyErrorOverride'': ProxyErrorOverride("On"|"Off", default: "")
  * ''VAR_Apache24_WIN_ProxyIOBufferSize'': ProxyIOBufferSize(number, default: "")
  * ''VAR_Apache24_WIN_ProxyMaxForwards'': ProxyMaxForwards(number, default: "")
  * ''VAR_Apache24_WIN_ProxyPassInterpolateEnv'': ProxyPassInterpolateEnv("On"|"Off", default: "")
  * ''VAR_Apache24_WIN_ProxyPreserveHost'': ProxyPreserveHost("On"|"Off", default: "")
  * ''VAR_Apache24_WIN_ProxyReceiveBufferSize'': ProxyReceiveBufferSize(number, default: "")
  * ''VAR_Apache24_WIN_ProxyStatus'': ProxyStatus("On"|"Off"|"Full", default: "")
  * ''VAR_Apache24_WIN_ProxyTimeout'': ProxyTimeout(number, default: "")
  * ''VAR_Apache24_WIN_ProxyVia'': ProxyVia("On"|"Off"|"Full"|"Block", default: "")
  * ''VAR_Apache24_WIN_ProxyAddHeaders'': ProxyAddHeaders("On"|"Off", default: "")
  * ''VAR_Apache24_WIN_ProxyPassInherit'': ProxyPassInherit("On"|"Off", default: "")
  * ''VAR_Apache24_WIN_ProxySourceAddress'': ProxySourceAddress(string, default: "")


## Dependencies

特にありません。

## Usage

1. 本Roleを用いたPlaybookを作成します。
2. 必須変数を指定します。
3. 任意変数を必要に応じて指定します。
4. Playbookを実行します。


## Example Playbook

インストールとすべての設定をする場合は、提供した以下のRoleを"roles"ディレクトリに配置したうえで、
以下のようなPlaybookを作成してください。

- フォルダ構成
~~~
  - group_vars/
    ・ server1
    ・ server2
  - host_vars/
    ・ host1
    ・ host2
  - roles/
    ・ Apache_install/
    ・ Apache_setup/
  - Apache24_WIN_install.yml
  - Apache24_WIN_ossetup.yml
  - Apache24_WIN_setup.yml
  - conf.yml
  - hosts
  - site.yml
~~~

- マスターPlaybook サンプル「Apache24_WIN_setup.yml」
~~~
# Apache24_WIN_setup.yml
 - name: setup Apache2.4
   hosts: all
   gather_facts: yes
   become: no
   tags:
    - setup
   roles:
     - Apache24_WIN_setup
~~~

## Running Playbook
- extra-vars を利用する場合の実行例
> ansible-playbook site.yml  -i hosts --extra-vars="@conf.yml"

- group_vars を利用する場合の実行例  
group_vars で指定したグループ名が webserver1 の場合
> ansible-playbook site.yml  -i hosts -l webserver1

- host_vars を利用する場合の実行例  
host_vars で指定したグループ名が server1 の場合
> ansible-playbook site.yml  -i hosts -l server1

- 本Roleのみを実行する場合は、 --tags "install" を付け加える
> ansible-playbook site.yml  -i hosts --extra-vars="@conf.yml" --tags "setup"


# Copyright
Copyright (c) 2017 NEC Corporation

# Author Information
NEC Corporation

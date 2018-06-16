# TLS 1.2対応について
近年、脆弱なTLS 1.1以前を無効化し、TLS 1.2のみを有効化するサーバーが増えています。ここではffftpでTLS 1.2を有効化する方法を説明します。
ffftp 3.0以降ではWindows付属の暗号化ライブラリ[Schannel SSP](https://docs.microsoft.com/ja-jp/windows-server/security/tls/tls-ssl-schannel-ssp-overview)を使用しているため、TLS 1.2が使用できるかどうかはWindowsの設定に依存します。ここではバージョンごとに設定方法を説明します。

## Windows 8以降
既定でインストールされており、有効となっています。特に設定は必要ありません。


## Windows 7
既定でインストールされているものの、無効となっています。管理者用コマンドプロンプトで次のコマンドを実行することで有効化できます。
```
REG ADD "HKLM\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client" /v DisabledByDefault /t REG_DWORD /d 0
REG ADD "HKLM\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0\Client" /v Enabled /t REG_DWORD /d 0
```


## Windows Vista
既にサポートは終了しており、セキュリティパッチが提供されない状況です。アップグレードすることを推奨します。

既定ではインストールされていません。

Windows Server 2008 SP2向けに[更新プログラム](https://support.microsoft.com/en-us/help/4019276/update-to-add-support-for-tls-1-1-and-tls-1-2-in-windows)が用意されており、[Microsoft Updateカタログ](https://www.catalog.update.microsoft.com/)から[更新プログラムKB4019276](https://www.catalog.update.microsoft.com/Search.aspx?q=KB4019276)でダウンロードできます。なお、この更新プログラムは2018年5月現在、[セキュリティ更新プログラムKB4056564](https://www.catalog.update.microsoft.com/Search.aspx?q=KB4056564)で置き換えられています。Windows Server 2008 SP2向けとされていますがWindows Vistaにもそのまま適用できます。  
更新プログラム適用し、管理者用コマンドプロンプトで次のコマンドを実行することで有効化できます。
```
REG ADD "HKLM\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client" /v DisabledByDefault /t REG_DWORD /d 0
REG ADD "HKLM\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0\Client" /v Enabled /t REG_DWORD /d 0
```


## Windows XP
既にサポートは終了しており、セキュリティパッチが提供されない状況です。アップグレードすることを推奨します。

既定ではインストールされていません。

Windows Embedded POSReady 2009向けに[更新プログラム](https://support.microsoft.com/en-us/help/4019276/update-to-add-support-for-tls-1-1-and-tls-1-2-in-windows)が用意されており、[Microsoft Updateカタログ](https://www.catalog.update.microsoft.com/Search.aspx?q=KB4019276)からダウンロードできます。Windows Embedded POSReady 2009向けとされていますがコマンドプロンプトで次のコマンドを実行することでWindows XPに適用できるようになります。
```
REG ADD "HKLM\SYSTEM\WPA\PosReady" /v Installed /t REG_DWORD /d 1
```
更新プログラム適用し、コマンドプロンプトで次のコマンドを実行することで有効化できます。
```
REG ADD "HKLM\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client" /v DisabledByDefault /t REG_DWORD /d 0
REG ADD "HKLM\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0\Client" /v Enabled /t REG_DWORD /d 0
REG ADD "HKLM\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\PCT 1.0\Client" /v Enabled /t REG_DWORD /d 0
```


## Internet Explorer
なお、Internet Explorerは上記レジストリは参照していません。Windows 7以降では既定で利用できます。Windows Vista以前ではコマンドプロンプトで次のコマンドを実行することで利用できるようになります。
```
REG DELETE "HKLM\SOFTWARE\Microsoft\Internet Explorer\AdvancedOptions\CRYPTO\TLS1.2" /v OSVersion /f
```
これによりインターネットオプション、詳細設定のセキュリティの項目に TLS 1.2 が表示されるようになり、有効化できます。ただし、TLS 1.2を有効化できても、暗号アルゴリズムが不足している、ルート証明書が古い等で接続できない場合があります。
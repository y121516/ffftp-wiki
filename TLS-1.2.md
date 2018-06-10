# TLS 1.2対応について
ffftpではWindows付属の暗号化ライブラリを使用しているため、TLS 1.2が使用できるかどうかはWindowsの設定に依存します。ここではバージョンごとに設定方法を説明します。

## Windows 8以降
既定でインストールされており、有効となっています。特に設定は必要ありません。


## Windows 7
既定でインストールされているものの、無効となっています。次のレジストリを設定することで有効化できます。
```
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client
名前 DisabledByDefault、種類 DWORD、値 0
```
もし同じ場所に`Enabled`が存在する場合、値が`1`であることを確認してください。


## Windows Vista
既にサポートは終了しており、セキュリティパッチが提供されない状況です。アップグレードすることを推奨します。

既定でインストールされていません。

Windows Server 2008 SP2向けに[更新プログラム](https://support.microsoft.com/en-us/help/4019276/update-to-add-support-for-tls-1-1-and-tls-1-2-in-windows)が用意されており、[Microsoft Updateカタログ](https://www.catalog.update.microsoft.com/)から[更新プログラムKB4019276](https://www.catalog.update.microsoft.com/Search.aspx?q=KB4019276)でダウンロードできます。なお、この更新プログラムは2018年5月現在、[セキュリティ更新プログラムKB4056564](https://www.catalog.update.microsoft.com/Search.aspx?q=KB4056564)で置き換えられています。Windows Server 2008 SP2向けとされていますがWindows Vistaにもそのまま適用できます。  
更新プログラム適用後は次のレジストリを設定することで有効化できます。
```
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client
名前 DisabledByDefault、種類 DWORD、値 0
```
もし同じ場所に`Enabled`が存在する場合、値が`1`であることを確認してください。


## Windows XP
既にサポートは終了しており、セキュリティパッチが提供されない状況です。アップグレードすることを推奨します。

既定でインストールされていません。

Windows Embedded POSReady 2009向けに[更新プログラム](https://support.microsoft.com/en-us/help/4019276/update-to-add-support-for-tls-1-1-and-tls-1-2-in-windows)が用意されており、[Microsoft Updateカタログ](https://www.catalog.update.microsoft.com/Search.aspx?q=KB4019276)からダウンロードできます。Windows Embedded POSReady 2009向けとされていますが次のレジストリを設定することでWindows XPに適用できるようになります。
```
HKEY_LOCAL_MACHINE\SYSTEM\WPA\PosReady
名前 Installed、種類 DWORD、値 1
```
更新プログラム適用後は次のレジストリを設定することで有効化できます。
```
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client
名前 DisabledByDefault、種類 DWORD、値 0
```
もし同じ場所に`Enabled`が存在する場合、値が`1`であることを確認してください。


## Internet Explorer
なお、Internet Explorerは上記レジストリを参照していません。
```
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Internet Explorer\AdvancedOptions\CRYPTO\TLS1.2
名前 OSVersion
```
このレジストリを削除することで、インターネットオプション、詳細設定のセキュリティの項目に TLS 1.2 が表示されるようになります。この項目により、TLS 1.2が有効化できます。  
ただし、TLS 1.2を有効化できても、暗号アルゴリズムが不足している、ルート証明書が古い等で接続できない場合があります。
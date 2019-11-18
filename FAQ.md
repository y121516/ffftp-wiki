# バージョンの違いについて
ffftpは次の３種類があります。
 - 原作者 曽田純さんの開発による [～Version 1.97b [～2010/10/24]](http://www2.biglobe.ne.jp/sota/ffftp.html)
 - OSDN上での開発 [～Version 2.00 [～2018/4/15]](https://ja.osdn.net/projects/ffftp/)
 - GitHub上での開発 [Version 3.0～ [2018/1/1～]](https://github.com/ffftp/ffftp)

## Version 3.0以降の特徴
次のような変更を行っています。
 - Windows XP以降に対応（Windows 2000は動作対象外となりました）
 - Windows標準機能の有効活用
   - 暗号化ライブラリをOpenSSL他からWindows付属のSChannelおよびCryptoAPIに変更（Windows付属なためWindows Updateで脆弱性対応されます）
   - MUI; Multilingual User Interfaceにより表示言語の切替
   - NLS APIによる国際化ドメイン名処理
 - C++言語により効率的なコード記述
   - `std::wstring`により暗黙的な長さ制限の排除
   - 正規表現による文字列解析
   - コンテナ・アルゴリズムの活用
 - コンパイラー機能の活用
   - C++標準準拠
   - コード分析

# 接続エラーについて
様々な理由によりエラーが発生します。

 - まずは`PASV`モードを試してください。非`PASV`モード（`PORT`モード）の場合、ftpサーバーからftpクライアントへのデータ接続が行われますが、ルータ・firewall等によりブロックされる接続できないことが多いです。
 - `PASV`モードで接続できない場合、非`PASV`モードにした上で、`UPnP`をオンとオフの両方を試してください。UPnP Gatewayが存在しても経由する場合としない場合があり、どちらが正しいか一概には言えません。
 - IPv6を無効化することで接続できる場合があります。

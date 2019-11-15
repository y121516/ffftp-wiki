# 互換性
## [vsFTPd](http://vsftpd.beasts.org/)
接続には次のいずれかの条件を満たす必要があります。
- vsFTPdがOpenSSL 1.1.0以降を使用する
- vsFTPdに対し`require_ssl_reuse=NO`の設定を行う
- vsFTPdに対し`ssl_enable=NO`の設定を行う

<details>
  <summary>詳細</summary>
  vsFTPdはセキュリティ強化のため、データコネクションについて、コントロールコネクションのTLSセッションを引き継ぐことを強制します。しかしTLSセッションの引き続きでセッションが乗っ取られる危険性があります。これに対し<a href="https://tools.ietf.org/html/rfc7627">RFC 7627 Extended Master Secret</a>の対策があります。Windowsでは2019年10月のWindows UpdateでRFC 7627に対応していますが、同時にRFC 7627未対応サーバーに対しTLSセッションの引き継ぎが行えなくなっています。vsFTPdはOpenSSLを使用していますが、OpenSSLは1.1.0でRFC 7627に対応していますので、逆にOpenSSL 1.1.0未満ではセッションの引き継ぎが行なえません。vsFTPdで使用するOpenSSLは1.1.0以降とするか、セッション引き継ぎを要求しないよう設定変更が必要です。
</details>

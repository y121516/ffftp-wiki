# 互換性
## [vsFTPd](http://vsftpd.beasts.org/)
接続には次のいずれかの条件を満たす必要があります。
- vsFTPdがOpenSSL 1.1.0以降を使用し、Windows 8以降でFFFTPを実行する
- vsFTPdに対し`require_ssl_reuse=NO`の設定を行う
- FFFTP v2.00以前を使用する

<details>
  <summary>詳細</summary>
  vsFTPdはセキュリティ強化のため、データコネクションについて、コントロールコネクションのTLSセッションを引き継ぐことを強制します。しかしvsFTPdが使用しているOpenSSLには相性問題があります。FFFTP v3.0以降ではWindowsに付属するSChannelを使用していますが、OpenSSL 1.1.0未満とSChannelの組み合わせではTLSセッションの引き継ぎが行われません。また、SChannelにTLSセッションの引き継ぎ機能が実装されたのはWindows 8以降となります。
</details>

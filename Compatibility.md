# 互換性
## RFC7627 Extended Master Secret問題
2019年10月のWindows Update以降、古いFTP Serverと接続できない問題が発生しています。特にOpenSSL 1.1.0未満を使用されている例が多くあります。FTP Serverの脆弱性を修正するか、設定を変更する必要があります。

<details>
  <summary>詳細説明</summary>

  FTPにはコントロール接続とデータ接続とがあります。それぞれの接続を暗号化したとしても、データ接続がコントロール接続とは別の第三者の可能性を排除できません。この脆弱性を緩和するために一部のFTP Serverは、データ接続について、コントロール接続のTLSセッションを引き継ぐことを強制します。これによりTLSセッション情報を持たない攻撃者を排除できます。

  しかし強力な攻撃者の場合、TLSセッションを割り出しTLSセッションを引き継ぐ可能性があります。これに対し<a href="https://tools.ietf.org/html/rfc7627">RFC7627 Extended Master Secret</a>の対策があります。RFC7627を使用することで第三者がTLSセッションを引き継ぐ可能性を緩和します。

  Windowsでは2019年10月のWindows Updateで、TLSセッションを引き継ぐ際にはRFC7627の使用を強制するようになりました。この動作は<a href="https://support.microsoft.com/en-us/help/4528489/transport-layer-security-tls-connections-might-fail-or-timeout-when-co">Transport Layer Security (TLS) connections might fail or timeout when connecting or attempting a resumption</a>で説明されています。RFC7627に対応していない接続先に対してはTLSセッションを引き継がないようになっています。このことは、RFC7627に対応していないFTP Serverに対してTLSセッションが引き継がれず、接続できないことを意味します。

  TLS暗号化で広く使われているOpenSSLは2016年7月の1.1.0以降でRFC7627に対応しています。
</details>


### [vsFTPd](http://vsftpd.beasts.org/)
vsFTPdは長らく更新されておらず、最新の3.0.3が公開されたのは2015年7月となっています。OpenSSL 1.1.0未満を使用している場合は問題が発生します。次のどちらかの対応が必要です。
- vsFTPdが使用するOpenSSLを1.1.0以降に更新する
- vsFTPdに対し`require_ssl_reuse=NO`の設定を行う

### [FileZilla Server for Windows](https://filezilla-project.org/)
FileZilla Server for Windowsは長らく更新されておらず、最新の0.9.60.2が公開されたのは2017年2月となっています。0.9.60.2はOpenSSL 1.0.2kを使用しているため問題が発生します。次のどちらかの対応が必要です。
- `PROT Pを使用する場合、データ接続でTLSセッション再開を要求する`のチェックを外す
- OpenSSL 1.1.0以降を使用してビルドし直す

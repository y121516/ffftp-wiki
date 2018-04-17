# ffftpのビルド方法

## 環境

- Windows 7 SP1以降
  - .NET Framework 3.5
- Visual Studio 2017
  - MSBuild
  - VC++ 2017 v141 toolset (x86,x64)
  - Windows XP support for C++
  - Windows SDK (10.0.16299.0) for Desktop C++ [x86 and x64]

インストーラープロジェクトのビルドには[.NET Framework 3.5が必要](https://github.com/wixtoolset/issues/issues/5523)です。特にWindows 8以降は標準でインストールされていないので注意してください。

Visual Studio 2017はUpdateを適用し最新版を使用してください。 _Workloads_ から **Desktop development with C++** を選択し _Optional_ から **Windows XP support for C++** を選択します。 _Indivisual components_ にある同名コンポーネントは不完全なため注意が必要です。

**VC++ 2017 version 15.5 v14.12 toolset** 以降であれば動作するはずですが、現在は最新の **v141** をターゲットとしています。Windows SDKについてもバージョン依存しないはずですが、現在は **10.0.16299.0** をターゲットとしています。

## ビルド方法

**Developper Command Prompt for VS 2017** 上で次のコマンドを実行します。
```
MSBuild ffftp.sln /p:Configuration=Release;Platform=Win32
MSBuild ffftp.sln /p:Configuration=Release;Platform=x64
```
コンパイルの後、インストーラーが作成されます。`Release`ディレクトリに`ffftp-x86.msi`、`ffftp-x86.zip`、`ffftp-x64.msi`、`ffftp-x64.zip`が生成されます。

## 開発

Visual Studioで`ffftp.sln`を開いてください。インストーラープロジェクトを参照するためには拡張機能の[Wix Toolset Visual Studio 2017 Extension](https://marketplace.visualstudio.com/items?itemName=RobMensching.WixToolsetVisualStudio2017Extension)をインストールする必要があります。

`char*`の文字コードはWindows標準のANSI（日本語ではShift-JIS）ではなくUTF-8となっています。現在、順次`std::wstring`に移行中です。
# ffftpのビルド方法

## 環境

- Windows 7 SP1以降
  - .NET Framework 3.5
- Visual Studio 2019
  - MSBuild
  - MSVC v142 - VS 2019 C++ x64/x86 build tools (v14.22)
  - Windows 10 SDK (10.0)
  - Wix Toolset Visual Studio 2019 Extension
- vcpkg
  - boost.regex

### Visual Studio 2019について
Updateを適用し最新版を使用してください。

ターゲットとしては **Visual Studio 2019 (v142)** および **10.0 (latest installed version)** を選択しています。

Updateを適用し最新版を使用してください。大事なことなので二回言いました。

### vcpkgについて
[vcpkg](https://github.com/microsoft/vcpkg)のドキュメントに従い導入してください。

### インストーラープロジェクトについて
インストーラープロジェクトのビルドには[.NET Framework 3.5が必要](https://github.com/wixtoolset/issues/issues/5523)です。特にWindows 8以降は標準でインストールされていないので注意してください。ただし、.NET Framework 3.5が未インストールであってもビルドに支障ない場合もあるようです。

インストーラープロジェクトを参照するためには拡張機能の[Wix Toolset Visual Studio 2019 Extension](https://marketplace.visualstudio.com/items?itemName=WixToolset.WixToolsetVisualStudio2019Extension)をインストールする必要があります。

## ビルド方法

**Developper PowerShell for VS 2019** 上で、ffftpリポジトリをカレントディレクトリに設定して次のコマンドを実行します。
```
PS C:\Path\to\ffftp> git -C C:\Path\to\vcpkg apply -C0 --whitespace=fix (gi vcpkg\*.patch)
PS C:\Path\to\ffftp> C:\Path\to\vcpkg\vcpkg --overlat-triplets=vcpkg/triplets install boost-regex:x86-windows-ffftp boost-regex:x64-windows-ffftp
PS C:\Path\to\ffftp> MSBuild ffftp.sln /p:Configuration=Release;Platform=Win32
PS C:\Path\to\ffftp> MSBuild ffftp.sln /p:Configuration=Release;Platform=x64
```
コンパイルの後、インストーラーが作成されます。`Release`ディレクトリに`ffftp-x86.msi`、`ffftp-x86.zip`、`ffftp-x64.msi`、`ffftp-x64.zip`が生成されます。

## 開発

Visual Studioで`ffftp.sln`を開いてください。

`char*`の文字コードはWindows標準のANSI（日本語ではShift-JIS）ではなくUTF-8となっています。現在、`char8_t`は使われておらず、UTF-8文字列は順次`std::wstring`に移行中です。
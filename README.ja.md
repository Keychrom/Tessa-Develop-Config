# Tessa Develop Config

[Tessa](https://github.com/Keychrom/Tessa) の開発に使っている Arch Linux
マシンの `~/.config` から、公開しても安全な設定だけを抜き出したスナップショット
です。Vermilion Ink テーマで動かしている実際の環境（Tessa、Kitty、Starship、
Fcitx5/Mozc、セッション環境）を再現できます。

これは**完全なバックアップではなく、公開用に選別したサブセット**です。
ブラウザのプロファイルや入力履歴などの個人データは意図的に除外しています。

## 収録内容

| パス | 内容 |
| --- | --- |
| `tessa/config` | Tessa コンポジタと共有テーマ。レイアウト、ウィンドウルール、エフェクト、入力、XWayland、キーバインド、パレット |
| `tessa/panel.conf` | Tessa Panel。統合コントロールセンター、バー、ランチャー、ポップオーバー、壁紙、パネルのフォント/色 |
| `kitty/kitty.conf` | Vermilion Ink パレット、JetBrains Mono Nerd Font、powerline タブ、日本語 CJK フォールバックを含む Kitty 設定 |
| `starship.toml` | ホスト名、ディレクトリ、Git、各言語モジュールを表示する Starship プロンプト。[Hayao0819/dotfiles](https://github.com/Hayao0819/dotfiles/tree/master) から流用 |
| `fcitx5/config` | Fcitx5 の動作設定 |
| `fcitx5/profile` | JP キーボードレイアウトと Mozc を既定入力メソッドにした設定 |
| `fcitx5/conf/classicui.conf` | `TessaInk` テーマと Inter フォントを使う候補ウィンドウ設定 |
| `fcitx5/conf/notifications.conf` | Fcitx5 の通知設定 |
| `environment.d/90-fcitx5.conf` | Tessa セッション向けの GTK/Qt/SDL/XIM 入力メソッド環境変数 |

Tessa は `tessa/config`、`tessa/panel.conf`、`tessa/theme-colors.conf` の順に
読みます。分割した `panel.conf` は現在の 0.2.5 開発ツリーの Tessa が必要です。
古いビルドは無視します。`config` に残したパネルキーは互換性のため動作します。

## 意図的に除外したもの

開発機の `~/.config` には次のファイルがありますが、このリポジトリには含めて
いません。

- `mozilla/` — Firefox のプロファイル（`logins.db`、`key4.db`、
  `cookies.sqlite`、履歴、セッションデータなど）
- `mozc/` — 入力履歴、辞書、セッション状態、暗号化キー
- `dconf/user` — バイナリ形式のデスクトップ設定データベース
- Fcitx5 のキャッシュと一時ファイル（`cached_layouts`、
  `notifications.conf_*` など）
- `tessa/*.bak-*` — 日時付きのローカルバックアップ
- ロックファイル、ソケット、その他の実行時状態

元の `~/.config` は約 55 MB ありますが、ここに収録した安全な設定は数十 KB
程度で、認証情報やブラウザデータは含まれていません。

## 使い方

まず既存の設定をバックアップします:

```sh
cp -a ~/.config "$HOME/.config.backup-$(date +%Y%m%d-%H%M%S)"
```

リポジトリを取得して配置します:

```sh
git clone https://github.com/Keychrom/Tessa-Develop-Config.git
cd Tessa-Develop-Config
cp -a tessa kitty starship.toml fcitx5 environment.d ~/.config/
```

Fcitx5 とセッション環境を反映するため、ログアウトして再ログインするか、
各サービスを再起動してください。

別のマシンへそのまま上書きする場合は注意してください。`tessa/config` の
モニタ名、タッチパッド設定、アプリケーション ID、キーバインドは開発機向け
に調整されています。

## 必要なもの・注意点

- Tessa 設定は `Inter`、`JetBrainsMono Nerd Font`、日本語表示用の
  `Noto Sans Mono CJK JP` を前提にしています。
- `wallpaper_image` は
  `~/Pictures/Wallpapers/vermilion-ink.png` を参照しますが、画像自体は
  含まれていません。
- Fcitx5 の `TessaInk` テーマは `~/.config` の外にインストールされているため
  含まれていません。
- 設定内のパスは `~` か `PATH` 上のコマンドで、`/home/<user>` のような
  固定パスは使っていません。
- `tessa/panel.conf` は `panel_style = unified`、`control_features = all` です。
  個別ポップオーバーに戻す場合は `panel_style = classic` に変更します。
- Kitty は Nerd Font のグリフを多用します。タブやアイコンが崩れる場合は
  Nerd Font 対応フォントをインストールしてください。

## クレジット

- `starship.toml` は
  [Hayao0819/dotfiles](https://github.com/Hayao0819/dotfiles/tree/master)
  から流用しています。最新の内容と利用条件は上流リポジトリを確認してください。

## 関連リンク

- [Tessa コンポジタ / パネル](https://github.com/Keychrom/Tessa)
- [Tessa 公式サイト・ドキュメント](https://keychrom.github.io/)
- [Tessa ISO ビルダー](https://github.com/Keychrom/TessaISO)

## 状態

- スナップショット日: 2026-11-11
- 取得元: Arch Linux 開発機（`Arch-Suiren`）
- Tessa: 0.2.5 開発ツリー、Zig 0.17 / wlroots 0.20 / scenefx 0.5

## Tkinter
matplotlibとtkinterを組み合わせてデスクトップアプリを作成した場合、matplotlibのイベントループとtkinterのイベントループの両方を終了する必要がある
```sample.py
~~~省略~~~
    self.root.protocol("WM_DELETE_WINDOW", self.on_close)
def on_close(self):
    plt.close()
    self.root.destroy()
~~~省略~~~
```

親ウィジェット.pack_propagate(0)は、親ウィジェットが子ウィジェットのサイズに合わせてオートスケールすることを防止する
tkinter.PhotoImage()ではpngしか使えない
jpgを使いたいときはfrom PIL import ImageTk, Image; ImageTk.PhotoImage(Image.open())とする
RadioButtonではIntVar()でインスタンス生成した変数に値を持たせる。初期値はinstance.set()で設定

tkinter.messageboxの使い方は以下の7つ
- messagebox.showinfo()
- messagebox.showerror()
- messagebox.showwarning()
- messagebox.askyesno() True or False はい/いいえの選択肢
- messagebox.askquestion() yes or no
- messagebox.askokcancel() True or False OK/キャンセルの選択肢
- messagebox.askretrycancel() True or False 再試行 キャンセルの選択肢

## API
APIには次の2種類がある
1. Web API
   インターネットを介してリモートのサーバ上のソフトウェアを利用するためのAPI。REST APIはWeb APIの一種だが、REST API以外のWeb APIはあまり使われていないのでほぼ同じ意味。
   REST APIはHTTPプロトコルを使用してリソースの操作を行う。URLを通じてリソースを指定し、HTTPメソッド(GET、POST、PUT、DELETEなど)を使ってそのリソースに対する操作を行う。
2. ライブラリ API
   同じソフトウェア内、またはローカルの別のソフトウェアの機能を利用するためのAPI。Pythonのライブラリ関数などが一例であり、これらの関数を呼び出すことでライブラリが提供する機能を利用できる。

## coderabbit
github actions上でOpenAIのAPIをたたき、PRに直接レビューコメントを残してくれる

## rye
poetryやpipenvに代わるかもしれないpythonパッケージ管理ツール

## pythonで作成するデスクトップアプリのデータ保存
- ファイルシステム(テキスト, JSON, ...)
- SQLite
- ConfigParser

## google翻訳API
googletransは非公式なため、google-cloud-translateが望ましい
- googletrans==4.0.0-rc1
```
from googletrans import 
translator = Translator()
after_text = translator.translate(
        before_text,
        src=before_language_code,  # ex. 'ja'
        dest=after_language_code,  # ex. 'en'
    )
print(after_text.text)
```
- google-cloud-translate
```
from google.cloud import translate_v2 as translate
translator = translate.Client()
after_text = translator.translate(
        before_text,
        source_language=before_language_code,  # ex. 'ja'
        target_language=after_language_code,  # ex. 'en'
    )
print(after_text['translatedText'])
```

## 音源ファイル
pygameのデフォルト設定ではmp3に対応していない
mp3を使用する場合は以下を組み込む
$sudo apt-get update
$sudo apt-get install libpulse-dev
```
# NOTE tkinter等と併用しないと再生しない
import os
import pygame

os.environ["SDL_AUDIODRIVER"] = "pulseaudio"
pygame.init()
pygame.mixer.init()
pygame.mixer.music.load(mp3_file_name)
pygame.mixer.music.play()
pygame.mixer.music.set_volume(0.1)

# 以下よく使うコード
pygame.mixer.music.load()
pygame.mixer.music.play()
pygame.mixer.music.get_busy()
pygame.mixer.music.stop()
pygame.mixer.music.pause()
pygame.mixer.music.unpause()
pygame.mixer.music.set_volume()
```

## pythonライブラリ
### auto-py-to-exe
pyinstallerをGUIで操作できる
#### 使い方
$pipenv install auto-py-to-exe
$auto-py-to-exe

### loguru
ログ用ライブラリ

### kivy
レイアウトに関する情報などはKvファイル(拡張子.kv)に書く

## 環境構築
### WSLでのpyenv + pipenv
$sudo apt update && sudo apt install -y --no-innstall-recommends \
    build-essential \
    libffi-dev \
    libssl-dev \
    zlib1g-dev \
    libbz2-dev \
    libreadline-dev \
    libsqlite3-dev \
    git
$git clone https://github.com/pyenv/pyenv.git ~/.pyenv

## AWS
S3からファイルを削除するには、バケットとオブジェクト両方のリソースに対する権限が必要
ストレージサービス
- S3: オブジェクトストレージであり、静的コンテンツのホスティングやバックアップとして使用。
- EBS: ブロックストレージであり、低遅延のデータアクセスが必要なアプリケーションやデータベースのストレージとして使用。
- EFS: 複数のEC2インスタンスにマウントできる、オートスケーリング可能なストレージ。

table.scan()とtable.query()であれば、巨大なテーブルの読み込みパフォーマンスの関係からquery()を使うのが望ましい

## Unity
ラーニングパス
1. https://qiita.com/nmxi/items/7950fb12ef925efa276d
2. https://fujitsu.udemy.com/course/unity-chan-tutorial-01/

Update(): デフォルト。マシンのfpsに依存。
FixedUpdate(): マシンに依存せず統一されたfpsで実行。
LateUpdate(): 他のUpdate関数が全て実行された後に実行。

## git
git stash popとgit stash applyの違い
- git stash apply
  スタッシュした変更を適用した後でも、そのスタッシュをスタッシュリストに保持
- git stash pop
  スタッシュした変更を適用した後、そのスタッシュをスタッシュリストから削除

LinuxからWindowsに移してgit add .すると
warning: LF will be replaced by CRLF in til.md.
The file will have its original line endings in your working directory
と出る。これは、Gitがファイルの行末コードを変更しようとするため。
Windowsを使うのであれば、`git config --global core.autocrlf true`
Linuxを使うのであれば、`git config --global core.autocrlf input`

## SQL
- CREATE: 新しいデータベースやテーブルの定義
- DROP: 定義したテーブルなどの削除
- ALTER: 定義した内容の変更
- JOIN: テーブルの結合

## その他
pygameやtkinterを使用するならwslよりgit-bash
現在のシェルの.bashrcは以下
export PS1='\[\e]0;\[\033[01;32m\]\u@\h\[\033[01;33m\] \w\[\033[01;31m\] $(__git_ps1 "[%s]")\[\033[01;31m\]\[\033[01;34m\] $\[\033[00m\] '
Unixエポック: 1970年1月1日00:00:00 UTC
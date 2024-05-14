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

## pythonで作成するデスクトップアプリのデータ保存
- ファイルシステム(テキスト, JSON, ...)
- SQLite
- ConfigParser
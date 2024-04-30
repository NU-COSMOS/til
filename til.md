matplotlibとtkinterを組み合わせてデスクトップアプリを作成した場合、matplotlibのイベントループとtkinterのイベントループの両方を終了する必要がある
```sample.py
~~~省略~~~
    self.root.protocol("WM_DELETE_WINDOW", self.on_close)
def on_close(self):
    plt.close()
    self.root.destroy()
~~~省略~~~
```
# 顔検出ライブラリ比較(haarcascade/HOG+SVM/CNN)

大阪Pythonの会#06のハンズオン資料

haarcascadeはopencv。HOG+SVMとCNNはdlibのface_recognition。  
いずれも作成済みのモデルを使用します。

## Anacondaで環境構築

※windows環境は動作確認できていません。わからない場合は会で尋ねてください。

### windows

インストーラーでAnacondaを導入します。https://www.continuum.io/downloads

```
conda create -n face_detector python=3.5 jupyter numpy matplotlib
activate face_detector
conda install -c https://conda.anaconda.org/menpo opencv3
pip install face_recognition #エラーが出たら下記のboost.pythonが必要
jupyter notebook
```
libは元々c++のライブラリであるため、pythonでラッピングするためのboost.pythonが必要です。  
cmake、boost、boost pythonをインストールしてください。  
http://tadaoyamaoka.hatenablog.com/entry/2016/09/22/223507

### mac

まずpyenv(anyenv)を経由してインストールします。未導入の方はこちらから[anyenvで開発環境を整える](http://qiita.com/luckypool/items/f1e756e9d3e9786ad9ea)

```
pyenv install anaconda3-4.3.0
pyenv local anaconda3-4.3.0

conda create -n face_detector python=3.5 jupyter numpy matplotlib
```

cond info -eで表示されるrootのパス末尾に"/bin/activate"を追加して、エイリアスを作成します。

```
conda info -e
 face_detector          /Users/(user_name)/.anyenv/envs/pyenv/versions/anaconda3-4.3.0/envs/face_detector
 root                  *  /Users/(user_name)/.anyenv/envs/pyenv/versions/anaconda3-4.3.0

echo "alias activate='source /Users/(user_name)/.anyenv/envs/pyenv/versions/anaconda3-4.3.0/bin/activate'" >> ~/.bashrc
source ~/.bashrc
echo "source ~/.bashrc" >> ~/.bash_profile #毎回 source ~/.bashrcが面倒なら実行
```

homebrewでcmake、boost、boost-pythonを導入します。  
homebrewを未導入の方は下記を参照してインストールしてください。  
https://brew.sh/index_ja.html

```
brew install cmake boost
brew install boost-python --with-python3 --without-python
```

libboost_python3-mt.dylibにlibboost_python-mt.dylibというシンボリックリンクを貼ります。

```
sudo find / -name "libboost_python3-mt.dylib"
cd <find path above> #私の環境では/usr/local/opt/boost-python/lib/
ln -s libboost_python3-mt.dylib libboost_python-mt.dylib
```

仮想環境に入り、opencvとface_recognitionを導入。  
jupyterを起動します。

```
activate face_detector
conda install -c https://conda.anaconda.org/menpo opencv3
pip install face_recognition
jupyter notebook
```

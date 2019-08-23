# MuninDHT
　最低限動作するだけの DHT 系温湿度センサーの Munin 用プラグイン。

## 動作環境
　DHT11/22, AM2302 の何れかを接続した Raspberry Pi で動作するハズ。  
　当方環境は Raspberry Pi 3 + AM2302 (DHT22)

## 使い方
　[Adafruit_Python_DHT](https://github.com/adafruit/Adafruit_Python_DHT) をインストールし、同梱の AdafruitDHT.py を次の様に設置する。

    cp /path/to/Adafruit_Python_DHT/examples/AdafruitDHT.py /usr/local/bin

　/etc/munin/plugins 以下へ本スクリプトを設置する。

    cp dht /etc/munin/plugins

　/etc/munin/plugin-conf.d/00-default 等の設定ファイルに次のエントリを追加する。

    [dht]
    user root              - センサーにアクセス出来るユーザー名を指定 (必須)
    env.script             - Adafruit_Python_DHT 同梱のサンプルスクリプト "AdafruitDHT.py" の設置位置
    env.templog            - 取得した温度を一時的に保存しておくファイルを指定
    env.sensor             - 使用しているセンサーの種別。11 or 22 or 2302
    env.gpio               - 接続している GPIO 番号
    env.tempcorrection     - 温度補正値
    env.humiditycorrection - 湿度補正値
    env.retry              - エラー発生時のリトライ回数

　env による変数未設定時のデフォルト値は以下の通り。

    [dht]
    user root
    env.script /usr/local/bin/AdafruitDHT.py
    enc.templog /tmp/dht_temp_log
    env.sensor 2302
    env.gpio 4
    env.tempcorrection 0
    env.humiditycorrection 0
    env.retry 2

　munin-node を再起動して設定反映後にデータを収集し、グラフ化が開始される。

  ex)
  sudo systemctl restart munin-node.service

### ちょっとした特長
#### 補正機能
　TempCorrection と HumidityCorrection に値を設定することにより、取得した温度/湿度を校正する事が可能となる。  
　温度は特に補正の必要はないかもしれないが、ベースとして信用たるセンサーに合わせるなどすると良い。  
　湿度は飽和塩法を用いて補正するのが一般家庭ではベスト。

#### スパイク防止
　当方個体では長時間運用していると実際の室温 -12 度程度のスパイクが出来てしまうことがあった。  
　その為、取得した温度を一時的に保存しておき、次回データ取得時に比較する事で異常検知を行う。  
　実際には前回との温度差が 10 度以上低い場合はデータ取得を 1 度限りリトライする事で異常を防止する仕組み。

### 表示サンプル

![表示サンプル](https://bucci.bp7.org/dht22.png)


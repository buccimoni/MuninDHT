# MuninDHT
　最低限動作するだけの DHT 系温湿度センサーの Munin 用プラグインです。

## 動作環境
　Adafruit_Python_DHT をインストールし、同梱の AdafruitDHT.py を次の様に設置する。
`cp AdafruitDHT.py /usr/local/bin/dht.py`

　<https://github.com/adafruit/Adafruit_Python_DHT>

## 使い方
　基本的に /etc/munin/plugins 以下へ本スクリプトを設置するだけ。
`cp dht.sh /etc/munin/plugins`

### 冒頭の変数設定
　SENSOR はセンサーの種別をセットする。

* 11 = DHT11
* 22 = DHT22
* 2302 = AM2302

　GPIO には使用する Raspberry Pi の GPIO を指定する。

### 補正値
　TempCorrection と HumidityCorrection に値を設定することにより、取得した温度/湿度を校正する事が可能となる。

## 今後
　スクリプトの書き換えをすること無く設定ファイルからセンサー種別など指定出来る様にしたい。

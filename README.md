# MuninDHT
　最低限動作するだけの DHT 系温湿度センサーの Munin 用プラグイン。

## 動作環境
　[Adafruit_Python_DHT](https://github.com/adafruit/Adafruit_Python_DHT) をインストールし、同梱の AdafruitDHT.py を次の様に設置する。

    cp /path/to/Adafruit_Python_DHT/examples/AdafruitDHT.py /usr/local/bin/dht.py

## 使い方
　/etc/munin/plugins 以下へ本スクリプトを設置する。

    cp dht /etc/munin/plugins

　/etc/munin/plugin-conf.d/00-default 等の設定ファイルに次のエントリを追加する。

    [dht]
    user root

　munin-node を再起動して設定反映後にデータを収集し、グラフ化が開始される。

  ex)
  sudo systemctl restart munin-node.service

### 冒頭の変数設定
　SENSOR はセンサーの種別をセットする。

* 11 = DHT11
* 22 = DHT22
* 2302 = AM2302

　GPIO には使用する Raspberry Pi の GPIO を指定する。

### 補正値
　TempCorrection と HumidityCorrection に値を設定することにより、取得した温度/湿度を校正する事が可能となる。

### 表示サンプル

![表示サンプル](https://bucci.bp7.org/dht22.png)

## 今後
　スクリプトの書き換えをすること無く設定ファイルからセンサー種別など指定出来る様にしたい。

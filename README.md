# MuninDHT
　最低限動作するだけの DHT 系温湿度センサーの Munin 用プラグインです。

# 使い方
## 冒頭の変数設定
　SENSOR はセンサーの種別をセットする。

* 11 = DHT11
* 22 = DHT22
* 2302 = AM2302

　GPIO には使用する Raspberry Pi の GPIO を指定する。

## 補正値
　TempCorrection と HumidityCorrection に値を設定することにより、取得した温度/湿度を校正する事が可能となる。

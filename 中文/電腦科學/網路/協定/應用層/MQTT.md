---
tags: 筆記
---

# MQTT

MQTT 是一個專門對於物聯網設計的傳輸協議，
其中採用了非常節省流量和電力的方式來實現傳輸。

## 完整結構

使用 MQTT 前需要一台 MQTT Broker 來作為媒介，
並且使用一個 Client 去訂閱 Broker 的內容，
通常會使用另一個 Client 去發布訊息到 Broker 中。

## 訂閱與發布

### 主題 (Topic)

MQTT 訂閱與發佈都需要指定一個主題 (頻道)，
指定後就會收到該頻道的訊息或是發送訊息到該主題。

以下 MQTT 指令皆以 mosquitto 做示範。

### 訂閱

```sh
mosquitto_sub -t home/door -h 192.168.0.123
```

### 發布

```sh
mosquitto_pub -t home/door -h 192.168.0.123 -m "on"
```

## 傳輸模式 QoS

MQTT 分為 3 種不同的傳輸模式，

1. QoS 0

最多一次傳送 (可能沒送到)

2. QoS 1

最少一次傳送 (可能送到不只一次)

3. QoS 2

剛好一次傳送 (剛好只有一次)
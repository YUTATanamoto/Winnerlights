# BLE and Mesh Network  
## Provisioning  

## ATT  
#### Overview  
- Attribute Protocol（アトリビュートプロトコル/ATT）  
- Client-Serverアーキテクチャを実現するためのプロトコル  
- ServerとClientはそれぞれ属性データを持っており, 双方の確認のためにその属性のやり取りをするプロトコルがATTプロトコル  
- 属性(Attribute)はどのような機能やデータを持つかを示す  
- ATTプロトコルはClient-Server間の1対1通信を実現するための通信プロトコル  
- あくまで双方の属性を確認するためのプロトコルであり, データを読み込むなどの動作は含まない  
- データの読み込み等を行うためには一段上のレイヤのGATTを使う必要がある  

#### Server/ClientのAttribute  
- Attributeは以下の4つの値で構成される  
| Value Type | Discription |
| - | - |
| Attribute Handle | 各属性が持つ連番のインデックス |  
| Attributr Type | 128ビットのUUID |  
| Attribute value | 属性値, 上位レイヤが利用する値, 512バイトまで |    
| Attribute Permissions | 読み書きの権限, 値の意味は上位レイヤ(GATT)により決定される |  

#### 属性へのアクセス方法  
- ATTでは属性へのアクセス方法として以下の6つの方法が提供されている  
| Method | Discription |
| - | - |
| Request | ClientからServerにデータを要求する |
| Response | Requestに対する応答 |
| Indication | ServerからClientに通知を送る |
| Confirmation | Indicationを受け取ったことをClientからServerに通知する |  
| Command | ClientからServerに命令を送る, 返答は要求しない |  
| Nortification | ServerからClientに通知を送る, 受け取りの確認は不要 |   
- ClientとServerは同時に１つのやり取りしか行えない  
- CommandとNortification一方向の通信なので同時に複数送信することができるが遅延の原因位なるので上位レイヤで何かしらの対処をする必要がある  

### ATTプロトコルのPUD(Protocol Data Unit)  
- ATT protocolでは各Attributeの値を読み書きするために以下の3つの機能が提供されている  
| Method | Discription |    
| - | - |  
| Find |  |  

#### References  
- [TechWeb ATT](https://techweb.rohm.co.jp/iot/knowledge/iot02/s-iot02/04-s-iot02/3088?_ga=2.198053353.752863195.1595310844-839266698.1595310844)  
- [TechWeb ATT PDU](https://techweb.rohm.co.jp/iot/knowledge/iot02/s-iot02/04-s-iot02/3225?_ga=2.198053353.752863195.1595310844-839266698.1595310844)

## GATT  
- ATTを用いてデータを構造化する方法と, アプリケーション間でのやり取りの方法を定義する  
- 複数のServiceからなる  

## Service  
- 1つ以上のCharacteristicからなる

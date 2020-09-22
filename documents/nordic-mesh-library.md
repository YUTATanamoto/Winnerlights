# Nordic Semiconductor: IOS-nRF-Mesh-Library  

## MeshNetworkManager  
- メッシュネットワークを管理するためのメインオブジェクト  
- transparent independent ?   
- 受け取ったデータをこのオブジェクトに渡す際には```manager.bearerDidDeliverData(_,ofType)```メゾットを呼び出す  
- メッシュネットワークにパケットを送信する時には```trasmitter.send(_,ofType)```メゾットを飛び出す  
- Proxy機能を使用する際にはtransport implementationでパケットの分割と統合が必要  

#### Example   
```
let meshNetworkManager = MeshNetworkManager()
```
   or
```
let meshNetworkManager = MeshNetworkManager(using: MyStorage(), queue: DispatchQueue.someQueue, delegateQueue: DispatchQueue.main)
```  
## MeshNetworkManagerのプロパティ    
- MeshNetworkManagerのインスタンス生成後, プロパティの設定を行う  
- Bluetooth Meshの仕様に準拠した値がデフォルトで設定されている  

#### Example
```
meshNetworkManager.acknowledgmentTimerInterval = 0.600
meshNetworkManager.transmissionTimerInteral = 0.600
meshNetworkManager.retransmissionLimit = 2
meshNetworkManager.acknowledgmentMessageInterval = 5.0
meshNetworkManager.acknowledgmentMessageTimeout = 40.0
meshNetworkManager.logger = self
```  

## メッシュネットワークの作成, 読み込み, インポート　　
- メッシュネットワークマネージャーを作成しただけではダメ  
- ネットワークを作成すると空のネットワークと1つのProvisioner, プライマリNetworkKeyが生成される  
- 設定を保存するために```save()```を呼び出す  
- 最後に使用した設定を読み込む際には```load()```を呼び出す  
- ```import (from)```でJSONファイルから設定を読み込むことができる  

#### Example  
```var loaded = false
do {
    loaded = try meshNetworkManager.load()
} catch {
    print(error)
}

// If load failed, create a new MeshNetwork.
if !loaded {
    createNewMeshNetwork() // See AppDelegate in Sample App
} else {
    meshNetworkDidChange() // See AppDelegate in Sample App
}
```  

## GATT Bearers  
-  

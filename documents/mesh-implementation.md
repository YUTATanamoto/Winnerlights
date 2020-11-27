# Implementation of Mesh Network  

## Procedure  
- scan and discover unprovisioned device  
- open bearer  
    ```
    bearer.open()
    ```
- provision device  
    ```
    provisioningManager.provision(...)
    ```
- get Composition Data
    ```
    let message = ConfigCompositionDataGet()
            return try MeshNetworkManager.instance.send(message, to: node))
    ```
- get ttl
    ```
    let message = ConfigDefaultTtlGet()
            return try MeshNetworkManager.instance.send(message, to: node)
    ```
- create new 'Application Key' and save it 
    ```
    try? applicationKey.bind(to: networkKey)
    MeshNetworkManager.instance.save()
    ```
- add 'Application key' to node  
    ```
    try MeshNetworkManager.instance.send(ConfigAppKeyAdd(applicationKey: applicationKey), to: self.node)
    ```
- bind 'Application key' to Models you want to use  
    ```
    let message = ConfigModelAppBind(applicationKey: applicationKey, to: model)
    try MeshNetworkManager.instance.send(message, to: self.model)
    ```
- create Group
    ```
    let group = try Group(name: name, address: address)
    let network = MeshNetworkManager.instance.meshNetwork!
    try network.add(group: group)
    ```
- make 'Server' Models subscribe Group 
    ```
    message: ConfigMessage = ConfigModelSubscriptionAdd(group: group, to: self.model) ?? ConfigModelSubscriptionVirtualAddressAdd(group: group, to: self.model)!
    try MeshNetworkManager.instance.send(message, to: self.model)
    ```  
- set publication
    ```
    let publish = Publish(to: destinationAddress, using: applicationKey,
                    usingFriendshipMaterial: false, ttl: ttl,
                    periodSteps: self.periodSteps, periodResolution: periodResolution,
                    retransmit: Publish.Retransmit(publishRetransmitCount: retransmissionCount, intervalSteps: retransmissionIntervalSteps))
    let message: ConfigMessage = ConfigModelPublicationSet(publish, to: clientModel) ??
    ConfigModelPublicationVirtualAddressSet(publish, to: clientModel)!
    try MeshNetworkManager.instance.send(message, to: clientModel)
    ```
- publish message to subscribers('Server' Models)

## Note
- delete unnecessary subscription
    ```
    let message: ConfigMessage = ConfigModelSubscriptionDelete(group: group, from: self.model) ?? ConfigModelSubscriptionVirtualAddressDelete(group: group, from: self.model)!
    send(message, description: "Unsubscribing...")
    ```
- delete unnecessary publication
    ```
    guard let message = ConfigModelPublicationSet(disablePublicationFor: model) else {
            return
        }
    send(message, description: "Removing Publication...")
    ```
- conform to MeshNetworkDelegate
- to handle response from server, overwrite MeshNetworkDelegate
- 

## Fundamentals  
### configuredNode/unconfiguredNode/ppovisionerNode  


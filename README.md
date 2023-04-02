Test_joer
## *Draft*
# LoRaWAN NS-GW Interface

The LoRa WAN NS-GW interface is based on the following protocol stack:

````
+------------------------------------+
|      Content in Protobuf           |
+------------------------------------+
|      Restful API using CoAP        |
+------------------------------------+
|      WebSockets                    |
+------------------------------------+
|      TLS                           |
+------------------------------------+
|      IP                            |
+------------------------------------+
````

Two websocket connections shall be established between the GW and the NS:
 - one for the controlplan
 - one for the dataplane

The sources in this repository describe the Restful API and the content in Protobuf:

## Control plane

The APIs are described in OPEN API yaml files, separated in Controlplane and Dataplane and NS Interaces and GW Interfaces. 
The APIs are based on GET, POST, PUT and DELETE requests followed by the appropirate Response. The request payload is formed as a list of objects, the corresponding response is carrying the response objects in the same order as the request orders have been received. 

### Control plane API description

The control plane API defines the exchange of GW capabilities and configuration data, as well as asynchronous events (like alarms) and status changes and regular statistics. 

``` 
  GW                                                               NS
  +-----------------------------------------------------------------+
  | Registration     always >>>                                     |
  |                  GW.PUT Identity and Capabilities to NS/r       |
  +-----------------------------------------------------------------+
  | Configuration    either <<<                                     |
  |                  NS.PUT Configuration to GW/c                   |
  |                  GW.GET Configuration from NS/<gwEUI>/c         |
  |                  or >>>                                         | 
  |                  GW.PUT Configuration to NS/<gwEUI>/c           |
  |                  NS.GET Configuration from NS/<gwEUI>/c         |
  |                  NS.GET Capabilities from GW/c                  |
  +-----------------------------------------------------------------+
  | Operation        <<< >>>                                        |
  |                  Configuration as above                         |
  |                  >>>                                            |
  |                  GW.POST Alarms and Events to NS/<gwEUI>/a      | 
  |                  GW.POST regular statistics to NS/<gwEUI>/s     |
  |                  NS.GET status and statistics from GW/s         |
  +-----------------------------------------------------------------+
  | Deregistraion    either <<<                                     |
  |                  NS.DELETE at GW/d                              |
  |                  or >>>                                         | 
  |                  GW.DELETE at NS/<gwEUI>/d                      |
  +-----------------------------------------------------------------+
```
The control plane API are described in:
- LoRaWAN_NS-GW_GW
- LoRaWAN_NS-GW_NS


### Control plane content description 
The control plane content respective the objects being exchanged are described in the protobuf files. The payload of requests and responses is organized as a list of single objects. All supported single objectes are listed in the *.proto file. For each listed objects a corresponding schema MUST exist in the API description field. 

## Data plane
The data plane describes the interface related to LoRaWAN traffic and devices respective multicast groups. 

### Data plane API description
The dataplane APIs 

### Data plane content description 
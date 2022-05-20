# Electric Vehicle Charging REST API Document

This API uses POST request to communicate and HTTP response codes to indenticate status and errors. All responses come in standard JSON. All requests must include a content-type of application/json and the body must be valid JSON.

## API END Point
  http://electricvehiclechargingapi.malakconnect.com/

## Response Codes
```
1: Success
0: Bad request/Data Not Found
```

## Vehicle Charging
**API:** /api/VehicleCharging/VehicleCharging

**Method**: POST

**NOTE** : if we get 1 then success or we get 0 then record not insert

### Request
```
{
  "ElectricVehicleChargingIDP": "00000000-0000-0000-0000-000000000000",
  "esn": "string",
  "voltage": 0,
  "current": 0,
  "power": 0,
  "energy": 0,
  "frequency": 0,
  "power_factor": 0,
  "status": 0,
  "reset": 0,
  "timestamp": "2022-05-19T13:17:02.552Z"
}
```

### Response
```
responsestatus: 1 OR 0
```

## Heart Beat
**API:** /api/VehicleCharging/HeartBeatAPI

**Method**: POST

**NOTE** : if you are pass rr = 1 then status change and set 0 (if rr status is already 1

### Request
```
{
    "esn": "84:f3:eb:0a:1d:7e",
    "rr": 0
}
```

### Response
```
esn: 84:f3:eb:0a:1d:7e, relay1: 0, rtc:0
```
## Get ES NNumber
**API:** /api/VehicleCharging/GetESNNumber

**Method**: POST

### Request
```
No Need to pass any parameter
```

### Response
```
  {
    "Code": 1,
    "IV": "N/A",
    "Message": [
      {
        "ESNIDP": "0745c192-e102-4fc4-b087-629b7afb92ce",
        "ESN": "24:6f:28:da:5f:b0",
        "ESNName": "OFC_TEST",
        "IsMachineRunning": 0,
        "StopMachineMessage": "Machine is currently stoped"
      }]
  }<br/>
  
(NOTE : from this API you will get list of ESN. IsMachineRunning is 1 then you get in StopMachineMessage equal Machine is Running)
```
### `API: /api/VehicleCharging/RelayOnByESN`
  `Method: POST`

### Request
  {
    "ESN": "string",
    "RelayMin": 0,
    "Flag": 0
  }<br/>
  
(NOTE:  you will pass 1 in flag then update relay1 = 1 (also set min which you have passed in RelayMin) and you are passing 0 then relay1 is set 0.)

### Response
  {
    "Code": 1,
    "IV": "N/A",
    "Message": "Relay Is Stopped"
  }<br/>
  
(NOTE : You will pass 1 in IsMachineRunning then message will be this Relay Is Start)

### `API: /api/VehicleCharging/GetRelayStatus`
  `Method: POST`

### Request
  {
    "ESN": "84:f3:eb:0a:1d:7e"
  }<br/>

(NOTE:  you will pass 1 in flag then update relay1 = 1 (also set min which you have passed in RelayMin) and you are passing 0 then relay1 is set 0.)

### Response
  {
    "Code": 1,
    "IV": "N/A",
    "Message": [
     {
      "esn": "84:f3:eb:0a:1d:7e",
      "relay1": false
     }
    ]
  }<br/>
  
(NOTE : Relay is 0(off) then we get relay1:false or if Relay is 1(ON) then we get true.)

### `API: /api/VehicleCharging/GetAcknowledge`
  `Method: POST`

### Request

(NOTE : pass ESN in query string like below)<br/>

`END Point`/api/VehicleCharging/GetAcknowledge?ESN= 9c:9c:1f:25:05:40

### Response
  {
  "Code": 1,
  "IV": "N/A",
  "Message": [
    {
      "status": 0
    }
  ]
}<br/>

(NOTE : in this API we get status True or false (0 or 1))

# APC-SmartUPS Dashboard
Grafana dashboard configuration for UPS-SmartUPS metrics

### ***Requirements:***
1. Grafana 8.5.5+
2. InfluxDB 1.8+
3. Telegraf 1.22+
4. APC Smart-UPS (SMT1500R2X180)
    - Firmware UPS 08.3(ID18)+
5. UPS Network Management Card 2 (AP9630)
    - SNMP Enabled
6. PowerNet-MIB
    - [https://download.schneider-electric.com/files?p_enDocType=Firmware&p_File_Name=powernet441.mib&p_Doc_Ref=APC_POWERNETMIB_441_EN&_ga=2.1327155.308134662.1655066635-1868855171.1655066635](https://download.schneider-electric.com/files?p_enDocType=Firmware&p_File_Name=powernet441.mib&p_Doc_Ref=APC_POWERNETMIB_441_EN&_ga=2.1327155.308134662.1655066635-1868855171.1655066635)

### ***Metrics Captured:***
- upsBasicIdentModel
- upsBasicIdentName
- upsAdvIdentFirmwareRevision
- upsAdvIdentDateOfManufacture
- upsAdvIdentSerialNumber
- upsAdvIdentSkuNumber
- upsBasicBatteryTimeOnBattery
- upsBasicBatteryLastReplaceDate
- upsAdvBatteryCapacity
- upsAdvBatteryTemperature
- upsAdvBatteryRunTimeRemaining
- upsAdvBatteryReplaceIndicator
- upsAdvBatteryActualVoltage
- upsAdvBatteryInternalSKU
- upsAdvInputLineVoltage
- upsAdvInputFrequency
- upsAdvInputLineFailCause
- upsBasicOutputStatus
- upsAdvOutputVoltage
- upsAdvOutputFrequency
- upsAdvOutputLoad
- upsAdvOutputActivePower
- upsAdvOutputApparentPower
- upsHighPrecOutputCurrent
- upsAdvConfigLowBatteryRunTime
- upsAdvTestDiagnosticSchedule
- upsAdvTestDiagnosticsResults

### ***Collector Output Configuration:***
#### Reference the outputs.influxdb in the kubernetes deployment
- [/kubernetes/deployment.yml](https://github.com/Condoamanti/grafana/blob/master/dashboard/apc-smartups/kubernetes/deployment.yaml)
```
  [[outputs.influxdb]]
      urls = ["my-influxdb.example.com:8086"]
      database = "apc-smartups"
      insecure_skip_verify = true
      #ssl_ca = "/usr/local/etc/telegraf.ca"
```
### ***Collector Input Configuration:***
#### reference inputs.snmp in the kubernetes deployment
- [/kubernetes/deployment.yml](https://github.com/Condoamanti/grafana/blob/master/dashboard/apc-smartups/kubernetes/deployment.yaml)
```
  [[inputs.snmp]]
    # List of agents to poll
    agents = ["my-apc-smartups.example.com"]
    # Polling interval
    interval = "60s"
    # Timeout for each SNMP query.
    timeout = "10s"
    # Number of retries to attempt within timeout.
    retries = 3
    # SNMP version
    version = 2
    # SNMP community string.
    community = "public"
    # Measurement name
    name = "snmp.UPS"
```
### ***GitHub Repository:***
- [https://github.com/Condoamanti/grafana/tree/master/dashboard/apc-smartups](https://github.com/Condoamanti/grafana/tree/master/dashboard/apc-smartups)
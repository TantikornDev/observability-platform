# Architecture Decidion Diagram

## (Topic) 
```bash
กำหนด query command ของ config Tempo datasource ใน  Grafana Dashboard 
```

## (Sub Topic) Context and Problem Statement
```bash
เงื่อนไขการ query command สำหรับการ navigate trace to log 
```

## Considered Options
```bash
* query command เริ่มด้วย 
( {instance="${__span.instance}"} |= `traceID` | json | traceID = "${__trace.traceId}" )

* query command เริ่มด้วย 
( {job="loki.source.kubernetes.pods"} |= `traceID` | json | traceID = "${__trace.traceId}" )
```

## Decision Outcome
```bash
ตัวเลือกที่ตัดสินใจเลือก: คือ query command เริ่มด้วย 
( {job="loki.source.kubernetes.pods"} |= `traceID` | json | traceID = "${__trace.traceId}" )
เนื่องจาก trace ไม่ได้มีการส่งข้อมูล instance name มากับ attributes ดังนั้นจึงจำเป็นต้อง query จาก job ของ log แทน
```
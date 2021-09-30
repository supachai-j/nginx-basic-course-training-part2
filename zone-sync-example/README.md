# ตัวอย่างการทำ Zone Sync บน NGINX Plus

### ตรวจสอบสถานะการตั้งค่าผ่านทาง API
```sh
curl -s '127.0.0.1:8080/api/6/stream/zone_sync' | jq
```
> ต้องติดตั้ง jq package ด้วย

### ผลลัพธ์
```json
{ "status": { "nodes_online": 1, "msgs_in": 12, "msgs_out": 13, "bytes_in": 524, "bytes_out": 422 }, "zones": { "req": { "records_total": 2, "records_pending": 0 } } }
```
สังเกตค่า records_total จะเปลี่ยนแปลง หรือเพิ่มขึ้น

# LOGIVAN - Interview Questions

## FREIGHT MATCHING

### Mô tả

LOGIVAN là một platform kết nối Chủ hàng có hàng hoá cần vận chuyển và các công ty vận tải hoặc tài xế xe tải cá nhân. Đơn hàng được tạo trên LOGIVAN sẽ được kết nối tới hàng ngàn bên vận tải trên cả nước.

Vấn đề mà LOGIVAN đang gặp phải là khi có quá nhiều đơn hàng và tài xế mới, thì tài xế sử dụng platform sẽ nhìn thấy nhiều đơn hàng không liên quan đến năng lực vận tải của mình, ví dụ tuyến đường không phù hợp hay không có loại xe mà đơn hàng yêu cầu; từ đó mà tỉ lệ thoả mãn đơn hàng sẽ giảm.

Team đang xây dựng một thuật toán Digital Freight Matching, mục đích là để đẩy đơn hàng đến các bên vận tải phù hợp.

### Mô hình hoá


Điểm bốc hàng, điểm dỡ hàng, tuyến của bên vận tải đều là một object Location, có dạng (`address`, `lat`, `lng`, `radius`), ví dụ:
```json
{
  "address": "Cảng Cái Lân, Bãi Cháy, Quảng Ninh",
  "lat": 1.10218,
  "lng": -1.123843,
  "radius": 2000
}
```

Một đơn hàng sẽ có điểm bốc hàng (`Location`) và điểm dỡ hàng (`Location`)
Bên vận tải có thông tin các tuyến có thể chạy được, là một danh sách các địa điểm mà họ có thể chạy được (`[Location]`)


Ví dụ với một đơn có thông tin:
```json
  {
    "pickup_location": {
      "address": "Cảng Cái Lân, Bãi Cháy, Quảng Ninh",
      "lat": 1.10218,
      "lng": -1.123843,
      "radius": 2000
    },
    "dropoff_location": {
      "address": "Khu công nghiệp Phố Nối 1, Hưng Yên",
      "lat": 1.10218,
      "lng": -1.123843,
      "radius": 2000
    }
  }
```
và các bên vận tải: 
```json
  [
    [
      "pickup_location": {
        "address": "Cảng Cái Lân, Bãi Cháy, Quảng Ninh",
        "lat": 1.10218,
        "lng": -1.123843,
        "radius": 2000
      },
      {
        "address": "Hà Nội, Việt Nam",
        "lat": 1.10218,
        "lng": -1.123843,
        "radius": 100000
      }, 
      {
        "address": "Miền Bắc, Việt Nam",
        "lat": 1.10218,
        "lng": -1.123843,
        "radius": 500000
      }
    ], [
      {
        "address": "Hưng Yên, Việt Nam",
        "lat": 1.10218,
        "lng": -1.123843,
        "radius": 50000
      }, 
      {
        "address": "Miền Bắc, Việt Nam",
        "lat": 1.10218,
        "lng": -1.123843,
        "radius": 5000000
      }
    ]
  ]
```

### Yêu cầu

__*Viết một hàm tính toán*__ hoặc đề xuất cách giải quyết cho việc với mỗi một đơn hàng, đưa ra danh sách các bên vận tải phù hợp.

# 🌐📡 HỆ THỐNG GIÁM SÁT VÀ ĐIỀU KHIỂN TỪ XA QUA LoRa VỚI ESP32

---

## 📖 Mục lục

- [🚀 Giới thiệu](#-giới-thiệu)
- [⚙️ Thông số kỹ thuật](#️-thông-số-kỹ-thuật)
- [🧰 Danh sách linh kiện](#-danh-sách-linh-kiện)
- [📐 Sơ đồ nguyên lý và PCB](#-sơ-đồ-nguyên-lý-và-pcb)
- [🛠️ Hướng dẫn lắp ráp](#️-hướng-dẫn-lắp-ráp)
- [🧠 Lập trình firmware](#-lập-trình-firmware)
- [🌐 Cách sử dụng](#-cách-sử-dụng)
- [✅ Kiểm thử](#-kiểm-thử)
- [📸 Ảnh / Video demo](#-ảnh--video-demo)
- [🤝 Đóng góp](#-đóng-góp)
- [📄 Giấy phép](#-giấy-phép)

---

## 🚀 Giới thiệu

**ESP32 LoRa Web Server** là hệ thống giám sát và điều khiển từ xa thông qua giao tiếp **LoRa không dây** giữa các thiết bị **ESP32**, phù hợp cho các ứng dụng:

- 🌾 Nông nghiệp thông minh  
- 🌍 Giám sát môi trường  
- 🏠 Nhà thông minh

**Cấu trúc hệ thống:**

- 🧠 **ESP32 Master**: Thu thập dữ liệu từ các slave, lưu trữ và hiển thị lên **giao diện Web**.
- 📡 **ESP32 Slave (x2)**: Đọc dữ liệu từ cảm biến (nhiệt độ, độ ẩm, ánh sáng, độ ẩm đất) và truyền về master. Hỗ trợ điều khiển LED từ xa.

---

## ⚙️ Thông số kỹ thuật

| Thông số               | Chi tiết                                  |
|------------------------|--------------------------------------------|
| 🔧 Vi điều khiển         | ESP32 Dev Module                           |
| 📶 Giao tiếp không dây   | LoRa RA-02 (SX1278) - Tần số 433 MHz       |
| 🌐 Web Server            | ESP32 WebServer (HTML nhúng)              |
| 🌡️ Cảm biến tích hợp     | DHT11, LDR, cảm biến độ ẩm đất             |
| 🔋 Nguồn cấp             | 5V DC (USB hoặc nguồn ngoài)              |
| 🔗 Số Slave hỗ trợ       | 2 (có thể mở rộng)                         |
| 💡 Điều khiển            | LED 1, LED 2 trên mỗi Slave qua Web       |

---

## 🧰 Danh sách linh kiện

| 🔩 Linh kiện                   | Số lượng |
|-------------------------------|----------|
| ESP32 Dev Module              | 3        |
| Module LoRa RA-02 (SX1278)    | 3        |
| Cảm biến DHT11                | 2        |
| Cảm biến ánh sáng (LDR)       | 2        |
| Cảm biến độ ẩm đất            | 2        |
| LED + điện trở 220Ω           | 4        |
| Breadboard và dây nối         | Nhiều    |
| Nguồn 5V hoặc pin sạc         | Tùy chọn |

---

## 📐 Sơ đồ nguyên lý và PCB

> 🖼️ **Thêm hình ảnh sơ đồ mạch hoặc thiết kế PCB tại đây.**

📌 Có thể sử dụng phần mềm như:
- [Fritzing](https://fritzing.org/)
- [KiCad](https://kicad.org/)
- [EasyEDA](https://easyeda.com/)

---

## 🛠️ Hướng dẫn lắp ráp

1. 🔌 Kết nối cảm biến với ESP32 Slave theo sơ đồ.
2. 🔗 Nối module LoRa RA-02 với ESP32 qua SPI (MISO, MOSI, SCK, NSS).
3. 💡 Gắn LED và điện trở vào các chân GPIO phù hợp.
4. 📡 Cài đặt module LoRa lên ESP32 Master.
5. ⚙️ Nạp firmware tương ứng cho Master và các Slave.

---

## 🧠 Lập trình firmware

### 📁 Các tệp chính:

| File                    | Mô tả                                                               |
|-------------------------|---------------------------------------------------------------------|
| `gateway_websever.ino` | Firmware cho ESP32 Master – giao tiếp LoRa, cập nhật Web Server    |
| `n1.ino`                | Firmware cho Slave – đọc cảm biến, gửi dữ liệu qua LoRa            |
| `dashboard.h`           | Giao diện Web (HTML, CSS, JS nhúng trực tiếp trong code)           |

### 📚 Thư viện Arduino cần cài đặt:

- `LoRa by Sandeep Mistry`
- `WiFi`
- `ESPAsyncWebServer`
- `AsyncTCP`
- `DHT sensor library`
- `Adafruit Unified Sensor`

💡 *Mẹo: Sử dụng Board Manager để chọn đúng ESP32 Dev Module.*

---

## 🌐 Cách sử dụng

1. 🔌 Cấp nguồn cho tất cả ESP32 (Master + Slave).
2. 🖥️ Mở Serial Monitor, lấy địa chỉ IP từ Master.
3. 🌍 Mở trình duyệt và truy cập địa chỉ IP đó.
4. 📊 Quan sát dữ liệu từ các Slave: Nhiệt độ, độ ẩm, ánh sáng, độ ẩm đất.
5. 💡 Điều khiển bật/tắt LED từ giao diện Web.

---

## ✅ Kiểm thử

- 📡 Slave truyền đúng dữ liệu cảm biến về Master?
- 🔁 Master có nhận đầy đủ dữ liệu?
- 🌐 Giao diện Web hiển thị thông tin chính xác?
- 💡 Kiểm tra chức năng bật/tắt LED có phản hồi thực tế không?

---

## 📸 Ảnh / Video demo

> Thêm ảnh minh họa và video mô phỏng hoặc quay thực tế hệ thống tại đây.

- 🖼️ Sơ đồ mạch kết nối
- 🎥 Video demo hoạt động hệ thống
- 📎 Đường dẫn: [YouTube / Google Drive]

---

## 🤝 Đóng góp

Bạn có ý tưởng cải tiến hoặc phát hiện lỗi?  
📬 Hãy gửi issue hoặc pull request — **mọi đóng góp đều được chào đón!**

---

## 📄 Giấy phép

📜 Dự án được phát hành theo giấy phép [MIT License](LICENSE).  
Bạn có toàn quyền sử dụng, chỉnh sửa và phân phối lại với điều kiện giữ nguyên thông tin giấy phép.

---


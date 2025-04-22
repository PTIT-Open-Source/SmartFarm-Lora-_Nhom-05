# 🌐📡 HỆ THỐNG GIÁM SÁT NÔNG NGHIỆP THÔNG MINH VÀ ĐIỀU KHIỂN TỪ XA QUA LoRa VỚI ESP32

🎯 Mô tả ngắn gọn:

Dự án "Hệ thống giám sát và điều khiển nông nghiệp thông minh sử dụng ESP32 & LoRa" là một giải pháp IoT ứng dụng trong nông nghiệp, cho phép giám sát các thông số môi trường như nhiệt độ, độ ẩm không khí (DHT11), cường độ ánh sáng (BH1750) và độ ẩm đất. Hệ thống sử dụng giao tiếp LoRa không dây giữa các node cảm biến ESP32 và ESP32 Gateway, nơi dữ liệu được hiển thị qua Web Server. Người dùng có thể quan sát thông tin môi trường thời gian thực và điều khiển thiết bị như quạt làm mát và hệ thống phun sương từ xa qua trình duyệt web.



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

📌 Tóm tắt dự án
Dự án: Hệ thống nông nghiệp thông minh không dây sử dụng ESP32 và giao tiếp LoRa.

Chức năng chính:
Giám sát và điều khiển từ xa các thông số môi trường như nhiệt độ, độ ẩm không khí, ánh sáng và độ ẩm đất thông qua giao diện Web. Hệ thống có thể điều khiển thiết bị như quạt làm mát và bơm/phun sương tự động hoặc thủ công.

Người dùng chính:

Học sinh, sinh viên ngành kỹ thuật điện – điện tử, CNTT

Kỹ sư nông nghiệp, nhà nghiên cứu

Người làm vườn, nông dân ứng dụng công nghệ

Mục tiêu:

Giáo dục – học thuật: hỗ trợ học tập và nghiên cứu trong lĩnh vực IoT, điều khiển nhúng, và nông nghiệp thông minh.

Ứng dụng thực tiễn: phục vụ các mô hình canh tác nhỏ, vườn thông minh tại gia, nhà lưới, nhà kính.

Tiềm năng thương mại: có thể phát triển thành sản phẩm thực tế với chi phí thấp và khả năng mở rộng

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
4. ![image](https://github.com/user-attachments/assets/d5b4ecbb-c0c8-4612-b9db-8385282e0364)

5. 📊 Quan sát dữ liệu từ các Slave: Nhiệt độ, độ ẩm, ánh sáng, độ ẩm đất.
6. 💡 Điều khiển bật/tắt LED từ giao diện Web.
7. ☁️ Đẩy dữ liệu lên Firebase Realtime Database
ESP32 Master sẽ gửi dữ liệu cảm biến (nhiệt độ, độ ẩm, ánh sáng...) từ các Slave lên Firebase Realtime Database để lưu trữ và giám sát từ xa.

📦 Thư viện cần thiết
Cài đặt trong Arduino IDE:

Firebase ESP32 Client by Mobizt

ArduinoJson

🔧 Thiết lập Firebase
Truy cập Firebase Console

Tạo Project mới.

Vào Realtime Database → Create Database → Chọn chế độ Test mode

Vào Project Settings → General → lấy Project ID

Chọn tab Service Accounts → Generate new private key → Tải file .json
→ Dùng để lấy databaseURL và API key

🔑 Cấu hình Firebase trong mã nguồn

✅ Lưu ý
Tạo Project bằng tài khoản Google.

Có thể dùng chế độ Anonymous Authentication để không cần email/password.

Nếu có nhiều node (Slave), dùng đường dẫn /node2/..., /node3/... để phân biệt.

## ✅ Kiểm thử

Hệ thống đã được kiểm thử và hoạt động ổn định với các chức năng chính như sau:

📡 Truyền dữ liệu LoRa: Các thiết bị Slave truyền dữ liệu cảm biến (BH1750, DHT11, độ ẩm đất) về thiết bị Master một cách chính xác và liên tục.

🔁 Nhận dữ liệu: Thiết bị Master nhận đầy đủ và kịp thời dữ liệu từ các node Slave thông qua giao tiếp LoRa 433MHz.

🌐 Giao diện Web: Giao diện Web Server trên ESP32 Master hiển thị chính xác các thông số môi trường:

🌡️ Nhiệt độ

💧 Độ ẩm không khí

☀️ Cường độ ánh sáng

🌱 Độ ẩm đất

💡 Điều khiển thiết bị: Chức năng bật/tắt quạt và phun sương hoạt động tốt, phản hồi thực tế nhanh chóng sau khi thao tác trên Web.

🔒 Độ ổn định: Hệ thống hoạt động liên tục và ổn định trong các thử nghiệm thực tế, không xảy ra treo hoặc mất kết nối.

---

## 📸 Ảnh / Video demo


- 🖼️ Sơ đồ hệ thống
  ![image](https://github.com/user-attachments/assets/e04026bb-c00a-4e08-9c98-51f3bc12fc3d)

- Hoàn thiện mô hình hệ thống (sản phẩm )
  ![image](https://github.com/user-attachments/assets/5cc79b0c-3ba8-412b-9333-7e4858604de6)
  
- Demo kết quả
  Dữ liệu được hiển thị lên webwerver và điều khiển các thiết bị từ xa
  ![image](https://github.com/user-attachments/assets/98a4548b-dd76-4181-8722-bc7d4055ee37)

- Log dữ liệu chạy trong nhiều ngày liên tục
  ![image](https://github.com/user-attachments/assets/f5cf74f7-0420-4dfc-964f-8d6b89d5c80d)

  -Kiểm thử đo khả năng truyền nhận dữ liệu qua Lora ở khoảng cách xa trong thực tế
  ![image](https://github.com/user-attachments/assets/41bed124-c67a-4cc8-ace4-589d019a4068)


---

## 🤝 Đóng góp

Bạn có ý tưởng cải tiến hoặc phát hiện lỗi?  
📬 Hãy gửi issue hoặc pull request — **mọi đóng góp đều được chào đón!**

---

## 📄 Giấy phép

📜 Dự án được phát hành theo giấy phép [MIT License](LICENSE).  
Bạn có toàn quyền sử dụng, chỉnh sửa và phân phối lại với điều kiện giữ nguyên thông tin giấy phép.

---
## ✍️ Tác giả
Dự án được thực hiện bởi nhóm sinh viên:

👨‍💻 Nguyễn Bá Bách

👨‍💻 Hoàng Mạnh Quỳnh

👨‍💻 Nguyễn Ngọc Lâm

👨‍💻 Nguyễn Trọng Đạt

Xin chân thành cảm ơn sự hỗ trợ và hướng dẫn từ giảng viên và nhà trường trong suốt quá trình thực hiện dự án.


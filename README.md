# Game: Hệ Thống Mã Hóa Ngân Hàng

Chào mừng bạn đến với "Game: Hệ Thống Mã Hóa Ngân Hàng", một trò chơi mô phỏng tương tác được xây dựng bằng Python và Tkinter. Trò chơi này được thiết kế để giải thích một cách trực quan các quy trình và công nghệ mã hóa cốt lõi được sử dụng để bảo mật các giao dịch tài chính trong thế giới thực.

Bạn sẽ vào vai một nhân viên an ninh ngân hàng, chịu trách nhiệm xác minh và phê duyệt các giao dịch đang chờ xử lý. Nhiệm vụ của bạn là áp dụng đúng các bước giải mã và xác thực để phân biệt giữa giao dịch hợp lệ và giao dịch lừa đảo.
<img width="468" alt="image" src="https://github.com/user-attachments/assets/b6524c88-359e-4132-9636-a3cb766c86cd" />


* **Giao Diện Trực Quan:** Sử dụng Tkinter để tạo ra một giao diện người dùng thân thiện, giúp người chơi dễ dàng tương tác và theo dõi quy trình.
* **Mô Phỏng Thực Tế:** Quy trình xử lý giao dịch được mô phỏng theo các bước bảo mật chuẩn trong ngành ngân hàng.
* **Học Mà Chơi:** Tìm hiểu về các khái niệm mã hóa phức tạp như RSA, AES và SHA-256 một cách sinh động và dễ hiểu.
* **Lối Chơi Thử Thách:** Độ khó tăng dần theo cấp độ, với các giao dịch lừa đảo xuất hiện thường xuyên và tinh vi hơn.
* **Phản Hồi Tức Thì:** Hệ thống nhật ký (log) cung cấp phản hồi ngay lập tức về mỗi hành động của người chơi, giải thích kết quả thành công hay thất bại.

---

## 🚀 Yêu Cầu và Cài Đặt

Để chạy trò chơi này, bạn cần có Python 3 và cài đặt một số thư viện cần thiết.

1.  **Cài đặt Python:**
    Nếu chưa có, hãy tải và cài đặt Python từ trang chủ [python.org](https://www.python.org/).

2.  **Tải mã nguồn:**
    Lưu file `main.py` vào máy tính của bạn.

3.  **Cài đặt thư viện:**
    Trò chơi yêu cầu thư viện `cryptography`. Hãy mở Terminal (trên macOS/Linux) hoặc Command Prompt (trên Windows) và chạy lệnh sau:
    ```bash
    pip install cryptography
    ```

---

## 🎮 Cách Chơi

1.  **Chạy ứng dụng:**
    Mở Terminal hoặc Command Prompt, di chuyển đến thư mục chứa file `main.py` và thực thi lệnh:
    ```bash
    python main.py
    ```
2.  **Giao dịch xuất hiện:**
    Các giao dịch mới sẽ tự động xuất hiện trong danh sách "Giao Dịch Đang Chờ" ở bên trái.

3.  **Chọn giao dịch:**
    Nhấp vào một ID giao dịch (ví dụ: `TXN...`) để bắt đầu quá trình xác minh.

4.  **Thực hiện các bước bảo mật:**
    Bạn phải thực hiện tuần tự các hành động ở khung bên phải để kiểm tra giao dịch:
    * **1. Giải Mã Khóa (RSA):** Ngân hàng (chính là bạn) sử dụng *Private Key* của mình để giải mã *khóa phiên (session key)* AES mà khách hàng đã gửi. Khóa phiên này ban đầu được mã hóa bằng *Public Key* của ngân hàng.
    * **2. Giải Mã Giao Dịch (AES):** Sử dụng khóa phiên vừa giải mã để giải mã toàn bộ dữ liệu của giao dịch (người gửi, người nhận, số tiền).
    * **3. Xác Thực & Kiểm Tra (SHA/RSA):** Đây là bước quan trọng nhất. Hệ thống sẽ:
        * Tạo một bản băm (hash) mới từ dữ liệu giao dịch vừa giải mã bằng thuật toán **SHA-256**.
        * Sử dụng *Public Key* của khách hàng để xác thực *chữ ký số* đi kèm. Chữ ký này chính là bản băm gốc của giao dịch đã được khách hàng ký bằng *Private Key* của họ.
        * Nếu bản băm mới trùng khớp với bản băm được giải mã từ chữ ký, giao dịch được xác nhận là **toàn vẹn** (không bị thay đổi) và **xác thực** (đúng là của khách hàng).

5.  **Ra quyết định:**
    Dựa trên kết quả ở bước 3, hãy quyết định:
    * **CHẤP NHẬN:** Nếu kết quả xác thực là `HỢP LỆ ✓`.
    * **TỪ CHỐI:** Nếu kết quả xác thực là `KHÔNG HỢP LỆ ✗`.

6.  **Tính điểm và Lên cấp:**
    * **Xử lý đúng:** +10 điểm.
    * **Xử lý sai** (chấp nhận giao dịch lừa đảo hoặc từ chối giao dịch hợp lệ): -20 điểm.
    * Đạt đủ điểm, bạn sẽ được lên cấp, và tốc độ xuất hiện giao dịch sẽ nhanh hơn.

---

## 🔐 Các Khái Niệm Mã Hóa Trong Game

Trò chơi mô phỏng một **hệ thống mã hóa hybrid (lai)**, kết hợp giữa mã hóa đối xứng và bất đối xứng để đạt được cả hiệu suất và bảo mật.

### 1. Mã Hóa Bất Đối Xứng (RSA)

* **Mục đích:** Dùng để trao đổi khóa bí mật một cách an toàn và để tạo chữ ký số.
* **Trong game:**
    * **Mã hóa khóa:** Khách hàng dùng **Public Key của Ngân hàng** để mã hóa khóa phiên AES. Chỉ có Ngân hàng với **Private Key** tương ứng mới giải mã được.
    * **Chữ ký số:** Khách hàng dùng **Private Key của mình** để "ký" lên bản băm (hash) của giao dịch. Sau đó, Ngân hàng dùng **Public Key của Khách hàng** để xác thực chữ ký đó.

### 2. Mã Hóa Đối Xứng (AES)

* **Mục đích:** Dùng để mã hóa lượng lớn dữ liệu một cách nhanh chóng. Thuật toán này yêu cầu cả bên gửi và bên nhận đều phải có cùng một khóa bí mật.
* **Trong game:** Dữ liệu giao dịch (số tiền, tài khoản, v.v.) được mã hóa bằng một **khóa phiên AES** ngẫu nhiên. Khóa này được tạo riêng cho mỗi giao dịch.

### 3. Hàm Băm Bảo Mật (SHA-256)

* **Mục đích:** Tạo ra một "dấu vân tay" kỹ thuật số có độ dài cố định cho một khối dữ liệu. Bất kỳ thay đổi nhỏ nào trong dữ liệu đầu vào cũng sẽ tạo ra một giá trị băm hoàn toàn khác.
* **Trong game:** Thuật toán SHA-256 được dùng để tạo bản băm của dữ liệu giao dịch. Bản băm này được dùng để kiểm tra **tính toàn vẹn** của dữ liệu, đảm bảo nó không bị thay đổi trên đường truyền.

### Các loại Lừa Đảo (Fraud) trong Game

* **Dữ liệu bị thay đổi (Tampered Data):** Kẻ gian chặn và thay đổi nội dung giao dịch (ví dụ: tăng số tiền) *sau khi* nó đã được ký. Khi bạn xác thực, bản băm của dữ liệu đã bị thay đổi sẽ không khớp với chữ ký gốc.
* **Chữ ký giả mạo (Bad Signature):** Giao dịch được ký bằng một khóa private không phải của khách hàng. Khi bạn dùng public key của khách hàng để xác thực, quá trình sẽ thất bại.

# Transformation

![img](https://imgur.com/qcRk6X5.png)

Download file enc và xem nội dung: 

![img](https://imgur.com/e1PQBj2.png)

--> Có vẻ nội dung đã được mã hóa. 

Để ý đoạn code python phía sau: 

*<enc_content>''.join([chr((ord(flag[i]) << 8) + ord(flag[i + 1])) for i in range(0, len(flag), 2)])*

Giải thích đoạn code này: 

- *flag* được giả định là input string

- *for i in range(0, len(flag),2)*: Lặp qua các cặp ký tự (2 ký tự 1 lần) trong chuỗi flag

- *ord(flag[i])* và *ord(flag[i+1]*: ord() sẽ chuyển ký tự tại vị trí i và i + 1 trong flag thành giá trị số nguyên (mã Unicode của ký tự đó)

- *(ord(flag[i]) << 8>>) + ord(flag[i+1])*: Dịch trái mã Unicode của ký tự đầu tiên trong cặp 8 bit (tức là nhân với 256). Sau đó cộng với mã Unicode của ký tự thứ hai để ghép thành 1 số nguyên 16 bit

- *chr(...)*: chuyển số nguyên vừa tính được thành ký tự Unicode.

- *''.join(...)*: nối tát cả các ký tự lại thành 1 chuỗi kết quả

Ví dụ: 

Nếu flag = "ABCD" thì: 

- Cặp ký tự: ['AB', 'CD']

- Chuyển đổi: 'AB': (ord('A') << 8) + ord('B') = (65 << 8) + 66 = 16706. Ký tự Unicode là chr(16706) = '愀'. 'CD': (ord('C') << 8) + ord('D') = (67 << 8) + 68 = 17220. Ký tự Unicode là chr(17220) = '搀'

--> Kết quả: '愀搀'

Từ đó viết 1 đoạn mã python để decode nội dung file enc: 

![img](https://imgur.com/EKxMqS5.png)

Run code và tìm ra chuỗi đã được decode: 

![img](https://imgur.com/GixPGPH.png)

### Flag: picoCTF{16_bits_inst34d_of_8_26684c20}


# BÁO CÁO THỰC TẬP 1/7/2024 #

**sentiment_sarcasm** là một dự án được xây dựng theo hướng dẫn của anh Bá Ngọc trên kênh Youtube ProtonX.

Để chạy được dự án ta sử dụng câu lệnh chạy trên terminal:

`!python train.py`

Sử dụng câu lệnh trên sẽ mặc định các chỉ số học tập như batch size, epochs, learning rate,...như đã setting trong code `train.py`.

Để có thể thay đổi các chỉ số học tập của học máy ta dùng lệnh:

`!python train.py --batch-size x --epochs y --units z`

Với x, y, z là các tham số có thể thay đổi được để phù hợp với nhu cầu training.

(File `sentiment_sarcasm.ipynb` minh hoạ việc triển khai lệnh trên)

Dự án được anh Ngọc hướng dẫn sử dụng OOP để có thể chia các nhiệm vụ khác nhau như loading data, training,...thành từng class nhỏ, giúp việc triển khai, fix bug và bảo trì trở nên dễ dàng hơn bên cạnh lợi ích của 4 thuộc tính (kế thừa, đóng gói, đa hình, trừu tượng). 


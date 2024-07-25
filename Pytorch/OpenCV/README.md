## OpenCV ##

### OpenCV là gì ###
OpenCV được bắt đầu từ Intel năm 1999 bởi Gary Bradsky. OpenCV viết tắt cho Open Source Computer Vision Library. OpenCV là thư viện nguồn mở hàng đầu cho Computer Vision và Machine Learning, và hiện có thêm tính năng tăng tốc GPU cho các hoạt động theo real-time.

### Ứng dụng của OpenCV ###
OpenCV được sử dụng cho đa dạng nhiều mục đích và ứng dụng khác nhau bao gồm:
* Hình ảnh street view
* Kiểm tra và giám sát tự động
* Robot và xe hơi tự lái
* Phân tích hình ảnh y học
* Tìm kiếm và phục hồi hình ảnh/video
* Phim – cấu trúc 3D từ chuyển động

### OpenCV và Pytorch ###
Thư viện OpenCV và PyTorch là hai công cụ mạnh mẽ thường được sử dụng trong lĩnh vực thị giác máy tính và học sâu. Khi kết hợp, OpenCV có thể hỗ trợ PyTorch theo nhiều cách, đặc biệt trong việc xử lý và chuẩn bị dữ liệu ảnh.

#### 1. Thay đổi kênh màu ####
Thao tác chuyển đổi hệ kênh màu trong thư viện OpenCV. 
```
#Khai báo thư viện
import cv2
#Nhập vào dữ liệu là 1 bức ảnh
bgr_img=cv2.imread(r"Đường\dẫn\đến\ảnh.png")
#đổi sang kênh màu HSV
hsv_img = cv2.cvtColor(bgr_img, cv2.COLOR_BGR2HSV)
```
**Lưu ý:** Trong thư viện OpenCV, mặc định khi load ảnh từ file hoặc video sẽ là kênh màu Blue-Red-Green(BRG). Do đó tham số chuyển màu là `cv2.COLOR_BGR2HSV` chứ không phải `cv2.COLOR_RGV2HSV`.

Các tham số:
* **cvtColor:** hàm chuyển đổi kênh màu. 
* **bgr_img:** kiểu dữ liệu numpy.array lưu ảnh đầu vào ở không gian màu BGR.
* **hsv_img:** kiểu numpy.array lưu kết quả trả về.
* **COLOR_BGR2HSV:** Đổi từ kênh màu BGR sang HSV. Ngoài macro này ta còn có một số giá trị khác tương ứng với việc chuyển đổi giữa các kênh khác như: `COLOR_BGR2RGB`, `COLOR_BGR2GRAY`,...

#### 2. Hiển thị ảnh ####
Đầu tiên ta tạo một đối tượng chứa thông tin ảnh được tải lên từ file. Sau đó hiện thị hình ảnh lên cửa sổ giao diện.
```
img = cv2.imread('D:/duong/dan/den/file/anh.png',0)
print(type(img))
print(img.shape)
plt.imshow(img, cmap='gray')
plt.show()
```
Trong Jupyter Notebook, hàm `cv2.imshow()` không hoạt động do nó cần một giao diện đồ họa để hiển thị cửa sổ, điều mà Colab không hỗ trợ. Thay vào đó, ta sử dụng matplotlib để hiển thị ảnh.
Các tham số:
* **imshow():** Cho phép hiển thị dữ liệu dưới dạng hình ảnh.
* **show():** In, xuất ra màn hình ảnh ở địa chỉ vừa lấy.

#### 3. Lấy kích thước của ảnh ####
Lệnh img.shape để lấy ra kích thước của mảng này với h, w, d lần lượt là chiều cao, chiều rộng, độ sâu của bức ảnh.
```
(h, w, d) = img.shape
print("width={}, height={}, depth={}".format(w, h, d))
```

#### 4. Ghi ảnh ####
Sau khi biến đổi ảnh xong, ta muốn lưu ảnh thì sử dụng hàm `cv2.imwrite` với tham số đầu vào là đường dẫn đến file cần lưu (hỗ trợ các định dạng BMP, PNG, JPEG,...) và biến chứa ma trận điểm ảnh cần lưu.

```
import cv2
# Đọc ảnh đầu vào với tên là pandas.png
# Kết quả trả về lưu vào biến img kiểu numpy.array
img = cv2.imread('pandas.png')
# Thực hiện biến đổi trên ma trận img
...
# Hàm imwrite hỗ trợ lưu các định dạng phổ biến như bmp, png, jpeg
cv2.imwrite('/path/to/image/output.bmp', img)
```

#### 5. Lấy giá trị màu ở một điểm ảnh ####
```
#Ta lấy pixel/điểm ảnh tại vị trí w=50, h=50, d=0
(B, G, R) = img[50, 50]
print("R={}, G={}, B={}".format(R, G, B))
```

#### 6. Xoay ảnh theo chiều dọc ####
```
img = cv2.imread('D:/duong/dan/den/file/anh.png',0)
result = img[:, ::-1]
plt.imshow(result, cmap='gray')
plt.show()
```

#### 7. Xoay ảnh theo đường chéo chính ####
Ta dùng hàm transpose() Cú pháp và hình ảnh hiển thị như sau:
```
result = img.transpose()
plt.imshow(result,cmap='gray')
plt.show()
```

#### 8. Xoay ảnh theo chiều ngang ####
```
result = img[::-1, :]
plt.imshow(result,cmap='gray')
plt.show()
```

#### 9. Điều chỉnh độ sáng tối của ảnh ####
`Ta dùng cú pháp : Tên biến ảnh = Tên biến ảnh +/- độ sáng`

**Lưu ý:** Nên copy lại ảnh gốc trước khi chỉnh sửa Giá trị của một pixel là từ 0->255, khi giá trị x vượt quá 255 thì giá trị x mới sẽ bằng: x = x - 255, khi giá trị x nhỏ hơn 0 thì giá trị x mới sẽ bằng: x = 255 + x Ví dụ: Với 1 điểm ảnh có giá trị 275 thì điểm ảnh đó có giá trị thực là x = 275 - 255 = 25.

```
# Copy lại ảnh gốc ( tránh mất ảnh sau khi chỉnh sửa xong)
result=img.copy
# Tăng độ sáng ảnh lên 50 đơn vị
result=result +50
# In ảnh đã qua chỉnh sửa.
plt.show()
```

#### 10. Đổi màu một vùng ảnh ####
Để đổi màu một vùng ảnh ta lấy vị trí của vùng ảnh đó và thay đổi bằng giá trị màu mà ta muốn. Để thuận tiện cho việc lưu trữ ảnh gốc ta nên tạo nên vùng nhớ mới chứa dữ liệu ảnh ban đầu.

```
biến_tạm = biến_gốc.copy()
Cú pháp đổi màu: biến_tạm[vùng hàng, vùng của cột] = giá_trị_màu
```
```
img = cv2.imread('D:/duong/dan/den/file/anh.png',0)
result = img.copy()
result[100:250, 300:450] = 255
plt.imshow(result,cmap='gray')
plt.show()
```

### Hiệu ứng ảnh ###
#### Cách thực hiện ####
Quy ước: X là tọa độ chiều rộng Y là tọa độ chiều cao Z là tọa độ chiều sâu.
```
Tọa độ có thể bằng một khoảng [a:b]
VD: Image=[0:255,:,:] ([:] là lấy toàn bộ)
```

Để **Tạo hiệu ứng ảnh chuyển động**, ta thay thế giá trị điểm ảnh tại tọa độ a của ảnh 1 bằng giá trị điểm ảnh tại tọa độ b của ảnh 2 theo một vị trí chuyển động nhất định (Tịnh tiến, Quay, Ghi đè,…) mà người lập trình muốn bằng cách chạy vòng lặp.
```
VD: Image1[a:b,:,:] = Image2[c:d,:,:] với [a:b] = [c:d])
(Ex: Image1[0:10,:,:] = Image2[10:20,:,:])
```
Xuất những tấm ảnh ra màn hình sau mỗi vòng lặp, như vậy ta sẽ cảm thấy như chúng đang chuyện động. Để nâng cấp hiệu ứng hơn, việc giới hạn chiều ngang hoặc chiều cao để ghi đè hoặc tịnh tiến theo nhiều hướng, thì ta có thể tạo ra nhiều hiệu ứng khác.

Bằng cách thay đổi cách chọn tọa độ của điểm ảnh mà ta có thể thực hiện hiệu ứng trình diễn theo nhiều cách khác nhau. Sau đây là một cách thực hiện một số hiệu ứng đơn giản trong PowerPoint như Cover, Comb, Push ,...
```
#vì range(0,w) nó chỉ lấy giá trị từ 0->w-1
#nếu muốn hiệu ứng diễn ra nhanh hơn thì có thể thay:
# - range(0,w+1)->range(0,w+1,Speed),
# - Speed càng lớn thì ảnh hiện càng nhanh
results=[]
Speed = 6
for D in range(0,w+1,Speed):
    result=img1.copy()
    #Code trình diễn ảnh
    result[:,0:w-D,:] = img1[:,D:w,:]
    result[:,w-D:w,:] = img2[:,0:D,:]
    #Tạo gif
    results.append(result)
#Luu gif
imageio.mimsave('Name.gif', results)
```

### Pha trộn ảnh - Image Blending ###
Có rất nhiều cách thức pha trộn ảnh với nhau. Bài viết này tiến hành pha trộn ảnh từ ba dữ kiện đầu vào như sau:
* Ảnh foreground (tiền cảnh): chứa đối tượng chính cần tạo hiệu ứng lên. Trong ví dụ trên, tiền cảnh là người.
* Ảnh mask (mặt nạ): cho biết phạm vi áp dụng và phạm vi không áp dụng hiệu ứng. Trên ảnh mask có hai loại vùng điểm ảnh: vùng điểm nằm ngoài hiệu ứng và vùng điểm nằm trong cần thực hiện hiệu ứng. Các loại vùng điểm này lần lượt được minh họa bằng điểm màu xanh và màu đỏ trong ảnh dưới đây.
* Ảnh effect (hiệu ứng): chứa hiệu ứng cần áp dụng lên đối tượng tiền cảnh.
#### Cách thực hiện ####
Công thức tổng quát khi trộn ảnh như sau:
$$ g(x,y) = \alpha I_{fg}(x,y) + (1 - \alpha) I_{eff}(x,y) $$

Trong đó:
* $\alpha$: trọng số pha trộn ảnh giữa foreground và effect
* $I_{fg}(x)$: ảnh foreground chứa đối tượng chính
* $I_{eff}(x)$: ảnh effect chứa hiệu ứng
* $g(x,y)$: ảnh kết quả sau pha trộn

Những điểm ảnh cần pha trộn trên ảnh mask có giá trị kênh alpha bằng 255. Ngược lại, những điểm không được sử dụng để pha trộn thì giá trị kênh alpha bằng 0. Do đó khi duyệt qua các điểm ảnh ta sẽ kiểm tra xem giá trị kênh alpha của ảnh mask có khác 0 hay không.

Dưới đây là mã nguồn thuật toán pha trộn ảnh:
```
#Sao chép ảnh qua biến mới
result = fg.copy()
alpha = 0.6
for x in range(mask.shape[0]): # result.shape[0]: chiều cao ảnh
    for y in range(mask.shape[1]): # result.shape[1]: chiều rộng ảnh
        if (mask[x,y,3] != 0): # Kiểm tra điểm ảnh
            result[x,y] = (alpha * fg[x,y] + (1 - alpha) * eff[x,y])
          
cv2.imshow('Result', result)
cv2.waitKey(0)
```
Cách lập trình trên sử dụng hai vòng `for` lồng nhau nên **tốc độ rất chậm**. Ta sẽ thay vòng lặp trên với một dòng code duy nhất như dưới đây.
```
result = fg.copy()
alpha = 0.6
result[mask[:,:,3] != 0] = fg[mask[:,:,3] != 0] * alpha \
    + eff[mask[:,:,3] != 0] * (1 - alpha)

cv2.imshow('Result', result)
cv2.waitKey(0)
```
## Thực nghiệm ##
Code và kết quả thực nghiệm được triển khai trong file `ipynb`.
Giải thích lab3_exercise.ipynb

Câu 1: 
Công nghệ sử dụng: ngôn ngữ python, numpy để xử lý mảng,thư viện scipy.ndimage để xử lý hình ảnh, thư viện matplotlib để vẽ đồ thị và hiển thị ảnh

Thuật toán sử dụng và cách hoạt động:

data = iio.imread('exercise/colorful-ripe-tropical-fruits.jpg')

print("Shape of image:", data.shape)

Dùng để đọc ảnh từ folder exercise
Sau khi ước tính vị trí của quả kiwi ( Tọa độ x1 bắt đầu theo chiều ngang bên trái và kết thúc theo chiều ngang bên phải(x2), Tọa độ y1 bắt đầu theo chiều dọc ở trên và kết thúc theo chiều dọc ở dưới(y2) )

kiwi_region = data[y1:y2, x1:x2]

Chọn vùng ảnh có chứa quả kiwi theo tọa độ đã được xác định

shifted_kiwi = nd.shift(kiwi_region, (0, 30, 0))  # tinh tien 30px sang phai

hàm shift cho phép điều chỉnh vị trí của hình ảnh mà hình ảnh vẫn không bị ảnh hưởng 
Tham số ( 0, 30, 0) được hiểu là chiều dọc Y, chiều ngang X (sang phải 30px), màu

plt.savefig('img/shifted_kiwi.jpg')  

Sau đó sẽ lưu hình ảnh vào img


Câu 2:
Công nghệ sử dụng: ngôn ngữ python, numpy để xử lý mảng,thư viện imageio dùng để đọc và ghi ảnh, thư viện matplotlib để vẽ đồ thị và hiển thị ảnh

Thuật toán và cách hoạt động:

data = iio.imread('exercise/colorful-ripe-tropical-fruits.jpg')

Đọc ảnh từ file và xác định vị trí của đu đủ (x1 x2 y1 y2) và dưa hấu (x3 x4 y3 y4) 

x1, y1 = 120, 300
x2, y2 = 700, 850

x3, y3 = 1600, 300
x4, y4 = 2100, 1100

Vùng được xác định vị trí sẽ được thay đổi thành màu đỏ cho đu đủ và xanh lá cho dưa hấu

np.clip sẽ đảm bảo giá trị màu không vượt 255 tránh tình trạng lỗi màu sắc

papaya_region = data[y1:y2, x1:x2]
watermelon_region = data[y3:y4, x3:x4]

data[y1:y2, x1:x2] = np.clip(papaya_region * [1, 0, 0], 0, 255) #red
data[y3:y4, x3:x4] = np.clip(watermelon_region * [0, 1, 0], 0, 255) #green


Câu 3
Công nghệ sử dụng: ngôn ngữ python, numpy để xử lý mảng,thư viện imageio dùng để đọc và ghi ảnh, thư viện scipy.ndimage cho phép xoay ảnh, thư viện matplotlib để vẽ đồ thị và hiển thị ảnh

Thuật toán và cách hoạt động:

Đọc ảnh 

data = iio.imread('exercise/quang_ninh.jpg')

Xác định tọa độ và vùng cắt của núi (x1 x2 y1 y2) và thuyền (x3 x4 y3 y4)

x1, y1 = 380, 20
x2, y2 = 750, 330

x3, y3 = 500, 450
x4, y4 = 650, 550

mountain_region = data[y1:y2, x1:x2]
boat_region = data[y3:y4, x3:x4]

hàm nd.roate cho phép các vùng đã được chọn xoay 45 độ

mountain_region = nd.rotate(mountain_region, 45)
boat_region = nd.rotate(boat_region, 45)

Câu 4
Công nghệ sử dụng: ngôn ngữ python, numpy để xử lý mảng,thư viện imageio dùng để đọc và ghi ảnh, thư viện scipy.ndimage cho phép thay đổi kích thước ảnh (zoom), thư viện matplotlib để vẽ đồ thị và hiển thị ảnh

Thuật toán và cách hoạt động:

Đọc ảnh

data = iio.imread('exercise/pagoda.jpg')

Xác định tọa độ và vùng cắt của ngôi chùa 

x1, y1 = 200, 130
x2, y2 = 350, 200

pagoda_region = data[y1:y2, x1:x2]

Vùng được chọn sẽ phóng to lên 5 lần bằng hàm zoom

scale_factor = 5
resized_pagoda_region = zoom(pagoda_region, (scale_factor, scale_factor, 1))

Tham số (scale_factor, scale_factor, 1) ở đây scale_factor là chiều cao Y và chiều rộng X. Sau khi sử dụng hàm zoom sẽ nhân 5 với tham số này.

VD: Tính chiều rộng và chiều cao rồi nhân 5 sẽ có được kích thước mới sau khi phóng to

Chiều rộng (w) = x2 - x1
Chiều cao (h) = y2 - y1 




Câu 5:
Công nghệ sử dụng: ngôn ngữ python, numpy để xử lý mảng,thư viện os để tương tác với tệp ảnh, thư viện imageio dùng để đọc và ghi ảnh, thư viện scipy cho phép tịnh tiến và xoay ảnh, thư viện matplotlib để vẽ đồ thị và hiển thị ảnh

Thuật toán và cách hoạt động:

- Hàm display_menu hiển thị các phương pháp biến đổi ảnh 

- Hàm load_image sẽ lấy ảnh từ folder, người dùng sẽ chọn 1 ảnh muốn biến đổi

- Hàm shift_image để tính tiến ảnh 

x_shift = int(input("Nhập số pixel để tịnh tiến theo chiều ngang: "))
y_shift = int(input("Nhập số pixel để tịnh tiến theo chiều dọc: "))
        
x_shift và y_shift sẽ nhận giá trị px khi người dùng nhập vào

- Hàm rotate_image để xoay ảnh

  Trước khi xoay ảnh sẽ số góc xoay
  
angle = float(input("Nhập góc xoay (độ): "))
rotated_data = nd.rotate(data, angle)

- Hàm zoom để phóng to và thu nhỏ
  
 scale_factor = float(input("Nhập hệ số phóng to/thu nhỏ: ")) 

 Nếu nhập 0.5 ảnh sẽ thu nhỏ 1 nữa, còn 2 hoặc 3 ảnh sẽ tăng gấp 2 hoặc 3 lần


Nhấn Q sẽ ngừng chương trình




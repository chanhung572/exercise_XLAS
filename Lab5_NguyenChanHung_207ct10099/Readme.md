Giải thích lab5.ipynb

Câu 2.1:

Công nghệ sử dụng: thư viện PIL mở và đọc ảnh, numpy để xử lý mảng, ImageIO đọc và ghi hình ảnh, SciPy dùng để tính toán qua hàm, scikit-image đo lường thuộc tính của ảnh, Matplotlib tạo đồ họa

Thuật toán sử dụng:
-Thresholding: sử dụng phương pháp otsu dùng để phân loại ảnh
-Labeling: xác định các đối tượng trong ảnh nhị phân
-Region Properties: dùng hàm regionprops để tính toán đối tượng được gán nhãn

Cách hoạt động: 
- Mở ảnh và đổi ảnh sang màu xám. sau đó lưu vào biến a
  
  data = Image.open('geometric.png').convert('L')
  a = np.asarray(data)
  
- Ngưỡng otsu sẽ tạo mảng b, giá trị pixel lớn hơn ngưỡng sẽ là true, nhỏ hơn sẽ là false
  
  thres = threshold_otsu(a)
  b = a > thres

- sử dụng label để gán nhãn trong khu vực mảng b, và kết quả là giá trị c
  
  c = label(b)

- chuyển đổi giá trị c thành hình ảnh và lưu lại

c1 = Image.fromarray(c)
c1 = Image.fromarray(c.astype(np.uint8) * 255) 
iio.imsave('label_output.jpg', c1)

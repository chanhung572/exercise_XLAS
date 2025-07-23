Giải thích lab5.ipynb

Câu 2.1:

Công nghệ sử dụng: thư viện PIL mở và đọc ảnh, numpy để xử lý mảng, ImageIO đọc và ghi hình ảnh, SciPy dùng để tính toán qua hàm, scikit-image đo lường thuộc tính của ảnh, Matplotlib tạo đồ thị và hiển thị ảnh

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

Câu 2.2:
Công nghệ sử dụng: thư viện PIL mở và đọc ảnh, numpy để xử lý mảng, SciPy dùng để tính toán qua hàm, scikit-image đo lường thuộc tính của ảnh, Matplotlib tạo đồ thị và hiển thị ảnh

Thuật toán sử dụng và cách hoạt động:
- Đọc ảnh và chuyển ảnh thành ảnh xám
  
  data = Image.open('geometric.png').convert('L')

- Sử dụng nd.shift để dịch chuyển ảnh và tính toán độ chênh lệch giữa các pixel
  
  bmg = abs(data - nd.shift(data, (0, 1), order=0))

- Sử dụng matplotlib để hiển thị ảnh
  
  plt.imshow(bmg)
  
  plt.show()

Câu 2.3
Công nghệ sử dụng: thư viện PIL mở và đọc ảnh, opencv để xử lý ảnh, numpy để xử lý mảng, SciPy dùng để tính toán qua hàm, scikit-image đo lường thuộc tính của ảnh, Matplotlib tạo đồ thị và hiển thị ảnh

Thuật toán sử dụng:

- Bộ lọc sobel: sử dụng để phát hiện cạnh trong ảnh theo chiều ngang dọc
- Tính toán độ chênh lệch từ kết quả của 2 hướng được cộng lại để thay đổi độ sáng của ảnh

Cách hoạt động:

- Đọc ảnh 

  data = Image.open('geometric.png')

- Áp dụng bộ lọc sobel để tính toán độ dốc
  
  Tính độ dốc theo chiều dọc
  
  a = nd.sobel(data, axis=0)

  Tính độ dốc theo chiều ngang
  
  b = nd.sobel(data, axis=1)

- Giá trị tuyệt đối của hai chiều được cộng lại và tạo ra bản đồ chênh lệch

  bmg = abs(a) + abs(b)

Câu 2.4
Công nghệ sử dụng: thư viện PIL mở và đọc ảnh, opencv để xử lý ảnh, numpy để xử lý mảng, SciPy dùng để tính toán qua hàm, scikit-image đo lường thuộc tính của ảnh, Matplotlib tạo đồ thị và hiển thị ảnh

Thuật toán sử dụng:
- Harris phương pháp phát hiện góc dựa trên ma trận. Tính toán độ mạnh các góc bằng đạo hàm bậc nhất và bậc hai

Cách hoạt động:
- Đọc ảnh
  
  data = Image.open('geometric.png')

- Tính đạo hàm bậc nhất
  Tính theo chiều ngang (x)
  
  x = nd.sobel(indata, 0)

  Tính theo chiều dọc (y)
  
  y = nd.sobel(indata, 1)

- Tính ma trận C
  
  Tính bình phương của các đạo hàm: x1 = x**2 và y1 = y**2
  
  Tính toán tích của các đạo hàm: xy = abs(x * y)

- Sử dụng nd.gaussian_filter để làm mịn
  
- Tính toán định thức và tổng
  
  Tính định thức của ma trận C: detC = x1 * y1 - 2 * xy
  
  Tính tổng của ma trận C: trC = x1 + y1

- Tính giá trị R
  
  Tính giá trị R, đại diện cho độ mạnh của góc: R = detC - alpha * trC**2


Câu 2.5.1
Công nghệ sử dụng: thư viện PIL mở và đọc ảnh, opencv để xử lý ảnh, numpy để xử lý mảng, SciPy dùng để tính toán qua hàm, scikit-image đo lường thuộc tính của ảnh, Matplotlib tạo đồ thị và hiển thị ảnh

Thuật toán sử dụng:
- Hough: phương pháp cho phép phát hiện các đường thẳng trong hình ảnh

Cách hoạt động:
- Tạo ma trận có data 256x256 với một điểm sáng tại vị trí (128, 128)
  
  data = np.zeros((256,256))
  
  data[128, 128] = 1

- Tính bán kính R dựa trên chiều cao và rộng của data, sau đó tạo ma trận ho để lưu trữ biến đổi hough

R = int(np.sqrt(V*V + H*H))

ho = np.zeros((R, 90), float)

Câu 2.5.2
Công nghệ sử dụng: thư viện PIL mở và đọc ảnh, opencv để xử lý ảnh, numpy để xử lý mảng, SciPy dùng để tính toán qua hàm, scikit-image đo lường thuộc tính của ảnh, Matplotlib tạo đồ thị và hiển thị ảnh

Thuật toán sử dụng:
- Harris phương pháp phát hiện điểm góc trên ảnh, sử dụng rộng rãi trong nhận diện đối tượng và phân tích hình ảnh

Cách hoạt động:
- Đọc ảnh và chuyển đổi ảnh thành ảnh xám bằng rgb2gray
  
  data = iio.imread('bird.png')

  image_gray = rgb2gray(data)
  
- Phát hiện góc Harris với hàm corner_harris, ảnh xám và tham số k ( điều chỉnh độ nhạy của phát hiện góc )

Câu 2.6
Công nghệ sử dụng: thư viện opencv để xử lý ảnh, numpy để xử lý mảng, Matplotlib tạo đồ thị và hiển thị ảnh

Thuật toán sử dụng:
- Harris phương pháp phát hiện điểm góc trên ảnh, xác định các vùng thay đổi về độ sáng

- Đọc ảnh và chuyển đổi thành ảnh xám bằng cv2.IMREAD_GRAYSCALE
  
  img1 = cv2.imread('geometric.png', cv2.IMREAD_GRAYSCALE)
  
  img2 = cv2.imread('label_output.jpg', cv2.IMREAD_GRAYSCALE)

- Gọi hàm cv2.cornerHarris để tìm điểm góc cho từng hình ảnh với các tham số
  - 2: Kích thước của vùng lân cận
  - 3: Kích thước của Sobel kernel
  - 0.04: Tham số nhạy cảm cho việc phát hiện

  corners1 = cv2.cornerHarris(img1, 2, 3, 0.04)

  corners2 = cv2.cornerHarris(img2, 2, 3, 0.04)

- Các điểm góc được xác định bằng cách so sánh với ngưỡng
  
  corners1 > 0.01 * corners1.max()

  Nếu giá trị điểm góc lớn hơn 1% giá trị tối đa sẽ được gán giá trị 255(trắng) vào ma trận

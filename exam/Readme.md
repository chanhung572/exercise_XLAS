Giải thích

Câu 1
Công nghệ sử dụng: thư viện opencv để xử lý ảnh, numpy để xử lý mảng, random dùng để sinh số ngẫu nhiên

Thuật toán sử dụng và cách hoạt động:
- Mean filter (lọc ảnh) làm mịn ảnh bằng cách thay thế giá trị px, mảng kernel được đặt với giá trị 3, sau đó lưu ảnh mới thành a_mean_filtered.jpg

def mean_filter(image, kernel_size=3):
    return cv2.blur(image, (kernel_size, kernel_size))

mean_filtered_image = mean_filter(image)

cv2.imwrite('img_cau1/a_mean_filtered.jpg', mean_filtered_image)

- random color change ( thay đổi màu ảnh ngẫu nhiên ) qua các kênh màu BGR bằng các giá trị ngẫu nhiên
  np.random.randint dùng để tạo màu ngẫu nhiên, cv2.merge kết hợp màu mới thành ảnh mới

- cv2.cvtColor chuyển đổi màu BGR sang HSV, cv2.split dùng để tách ảnh thành 3 kênh Hue, Saturation, và Value

Câu 2
Công nghệ sử dụng: thư viện opencv để xử lý ảnh, numpy để xử lý mảng, random dùng để sinh số ngẫu nhiên, matlplotlib tạo đồ thị

Thuật toán sử dụng và cách hoạt động:
- Đọc ảnh images = [cv2.imread('NM-XLA/image1.jpg'), cv2.imread('NM-XLA/image2.jpg'), cv2.imread('NM-XLA/image3.jpg')]

- Biến đổi ảnh ngược (image inverse), giá trị 255 - ảnh gốc
  
  def image_inverse(image):
    return 255 - image

- Phép chỉnh gamma (Gamma Correction), sử dụng gamma để điều chỉnh độ sáng

  def gamma_correction(image, gamma):
    invGamma = 1.0 / gamma
    table = np.array([(i / 255.0) ** invGamma * 255 for i in range(256)]).astype("uint8")
    return cv2.LUT(image, table)

- Biến đổi log (Log Transformation), sử dụng log để tăng độ sáng cho ảnh có giá trị thấp

  def log_transformation(image, c):
    return c * np.log1p(image).astype(np.uint8)

- Cân bằng histogram (Histogram Equalization), cải thiện độ tương phản
  
  def histogram_equalization(image):
    if len(image.shape) == 3:  # Nếu là ảnh màu
        yuv = cv2.cvtColor(image, cv2.COLOR_BGR2YUV)
        yuv[:, :, 0] = cv2.equalizeHist(yuv[:, :, 0])
        return cv2.cvtColor(yuv, cv2.COLOR_YUV2BGR)
    else:  # Nếu là ảnh xám
        return cv2.equalizeHist(image)

- Kéo giãn độ tương phản (Contrast Stretching), kéo giãn các giá trị min max được chỉ định

  def contrast_stretching(image, min_val, max_val):
    return cv2.normalize(image, None, alpha=min_val, beta=max_val, norm_type=cv2.NORM_MINMAX)

- Cân bằng histogram thích ứng (Adaptive Histogram Equalization), cải thiện độ tương phản của các vùng trong ảnh

- Lưu ảnh sau khi biến đổi với định dạng image_method( phương pháp biến đổi, vd histogram)_index(stt).jpg. VD 1 ảnh sau khi lưu có định dạng image_histogram_1.jpg

  def save_image(image, method, index):
    filename = f'img_cau2/output_{method}_{index}.jpg'
    cv2.imwrite(filename, image)

- Hàm def process_images(method): sẽ xử lý ảnh dựa trên các phím sẽ chọn để thực hiện biến đổi ảnh


Câu 3
Công nghệ sử dụng: thư viện opencv để xử lý ảnh, numpy để xử lý mảng, random dùng để sinh số ngẫu nhiên, matlplotlib tạo đồ thị

Thuật toán sử dụng và cách hoạt động:
- imread để đọc ảnh, resized để tăng kích thước ảnh lên 30px ở chiều rộng và cao ( chiều rộng và cao + 30 )
  
colorful_image = cv2.imread('NM-XLA/colorful-ripe-tropical-fruits.jpg')
colorful_image_resized = cv2.resize(colorful_image, (colorful_image.shape[1] + 30, colorful_image.shape[0] + 30))

- imread đọc ảnh, (h, w) lấy chiều cao và rộng của ảnh, getRotationMatrix2D tạo ma trận với tâm giữa ảnh, warpAffine áp dụng ma trận lên ảnh, flip lật ảnh đã xoay

quang_ninh_image = cv2.imread('NM-XLA/quang_ninh.jpg')
(h, w) = quang_ninh_image.shape[:2]
M = cv2.getRotationMatrix2D((w / 2, h / 2), 45, 1.0)  # Rotate 45 degrees
quang_ninh_rotated = cv2.warpAffine(quang_ninh_image, M, (w, h))
quang_ninh_flipped = cv2.flip(quang_ninh_rotated, 1)  # Flip horizontally

- imread đọc ảnh, resized tăng kích thước ảnh ( chiều rộng và cao * 5 ), sử dụng GaussianBlur để làm mờ ảnh với kích thước 7x7 

pagoda_image = cv2.imread('NM-XLA/pagoda.jpg')
pagoda_image_resized = cv2.resize(pagoda_image, (pagoda_image.shape[1] * 5, pagoda_image.shape[0] * 5))
pagoda_image_blurred = cv2.GaussianBlur(pagoda_image_resized, (7, 7), 0)
display_image(pagoda_image_blurred, 'Resized and Blurred Pagoda')


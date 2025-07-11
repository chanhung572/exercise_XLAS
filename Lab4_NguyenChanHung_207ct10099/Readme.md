Giải thích lab4_exercise.ipynb

Câu 1:
Công nghệ sử dụng: thư viện opencv, numpy để xử lý mảng

Thuật toán sử dụng và cách hoạt động: 
- cv2.imread: Đọc ảnh
- x1 y1 ( tọa độ góc trên bên trái ) x2 y2 ( tọa độ góc dưới bên phải )
- sử dụng shifted để tịnh tiến ảnh
- cv2.cvtColor: chuyển sang ảnh xám (gray)
- giá trị pixel của ảnh xám * 0.3 để làm tối ảnh từ đó sử dụng phương pháp otsu để xác định ngưỡng tối ưu cho việc phân loại pixel và cải thiện độ tương phản, phân tách các đối tượng
- cv2.imwrite: lưu kết quả 


Câu 2:
Công nghệ sử dụng: thư viện opencv, numpy để xử lý mảng

Thuật toán sử dụng và cách hoạt động: 
- cv2.imread: Đọc ảnh
- x1 y1 ( tọa độ góc trên bên trái ) x2 y2 ( tọa độ góc dưới bên phải )
- cv2.getRotationMatrix2D: dùng để tạo ma trận xoay. Sau đó sử dụng cv2.warpAffine để áp dụng lên vùng chọn
- cv2.cvtColor: chuyển sang ảnh xám (gray)
- cv2.adaptiveThreshold: phân tách đối tượng dựa trên độ sáng
- cv2.imwrite: lưu kết quả


Câu 3:
Công nghệ sử dụng: thư viện opencv, numpy để xử lý mảng

Thuật toán sử dụng và cách hoạt động: 
- cv2.imread: Đọc ảnh
- x1 y1 ( tọa độ góc trên bên trái ) x2 y2 ( tọa độ góc dưới bên phải )
- cv2.cvtColor: chuyển sang ảnh xám (gray)
- cv2.resize: thay đổi kích thước
- áp dụng binary_closing
  - sử dụng cv2.morphologyEx với cv2.MORPH_CLOSE làm mịn và loại bỏ các lỗ hỏng
- cv2.imwrite: lưu kết quả

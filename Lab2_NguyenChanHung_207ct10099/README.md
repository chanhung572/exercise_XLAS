Giải thích lab2_exercise.ipynb

Câu 1 
xử dụng pip install opencv-python matplotlib để cài đặt thư viện opencv để xử lý ảnh




Công nghệ sử dụng: ngôn ngữ python, thư viện opencv, numpy để xử lý mảng, thư viện matplotlib để vẽ đồ thị và hiển thị ảnh



Thuật toán sử dụng: 
 - image inverse ( hàm đảo ảnh ) dùng để đảo ngược màu sắc của ảnh
   
   def image_inverse(image):
    return 255 - image

   nếu như image có giá trị là x thì sẽ trở thành 255 - x

- gamma correction hàm dùng để thay đổi độ sáng của ảnh dựa trên giá trị của gamma
  nếu gamma > 1 ( ảnh tối ), gamma < 1 ( ảnh sáng )

  
- log transformation sử dụng hàm logarit dùng để tăng độ tương phản của ảnh
- histogram equalization cân bằng màu cho cho ảnh xám hoặc ảnh màu, phân bố màu sắc đồng đều hơn
- contrast stretching dùng để kéo giãn độ tương phản

- show image dùng để hiển thị ảnh
- def main dùng để lấy các ảnh từ foler exercise ( các ảnh có thể là .png .jpg .. )
  
  def main():
    folder_path = 'exercise'
    images = [f for f in os.listdir(folder_path) if f.endswith(('pagoda.jpg'))]

- break ngưng chương trình, nhập Q để ngưng.
   
  if choice == 'Q'
    break






Cách hoạt động:
 - sau khi chạy chương trình sẽ in ra các phương pháp biến đổi ảnh, người dùng sẽ nhấn các phím I G L H C và Q ( ngưng chương trình ) để in ra các ảnh mới đã qua xử lý
  I - Image Inverse Transformation
  G - Gamma Correction
  L - Log Transformation
  H - Histogram Equalization
  C - Contrast Stretching
  Q - Thoát
  


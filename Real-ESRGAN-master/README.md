##Cấu trúc mã nguồn

**Real-ESRGAN**:

### 1. **Cấu trúc thư mục**
Dự án được tổ chức thành các thư mục chính sau:

- **`realesrgan/`**: Chứa các module chính của mô hình Real-ESRGAN.
  - **`archs/`**: Định nghĩa các kiến trúc mạng.
  - **`data/`**: Xử lý dữ liệu, bao gồm các lớp dataset.
  - **`models/`**: Định nghĩa các mô hình huấn luyện.
  - **`utils/`**: Các hàm tiện ích hỗ trợ.
- **`scripts/`**: Các script hỗ trợ như tạo meta-info cho dữ liệu.
- **`options/`**: Các tệp cấu hình huấn luyện.
- **`experiments/`**: Lưu trữ các mô hình đã huấn luyện, log, v.v.
- **`docs/`**: Tài liệu hướng dẫn sử dụng và huấn luyện.
- **`results/`**: Lưu trữ kết quả dự đoán.
- **`requirements.txt`**: Các thư viện cần thiết.
- **`README.md`**: Giới thiệu tổng quan về dự án.

### 2. **Các module chính**

#### **a. `archs/`**
Chứa các kiến trúc mạng được sử dụng trong mô hình Real-ESRGAN.

- **`srvgg_arch.py`**: Định nghĩa lớp `SRVGGNetCompact`, một mạng VGG-style nhỏ gọn cho siêu phân giải.
- **`discriminator_arch.py`**: Định nghĩa lớp `UNetDiscriminatorSN`, một bộ phân biệt U-Net với chuẩn hóa phổ.


#### **b. `data/`**
Chứa các lớp dataset để xử lý dữ liệu huấn luyện và kiểm thử.

- **`realesrgan_paired_dataset.py`**: Định nghĩa lớp `RealESRGANPairedDataset` để xử lý dữ liệu cặp (ảnh thấp phân giải và cao phân giải).

#### **c. `models/`**
Chứa các mô hình huấn luyện.

- **`realesrnet_model.py`**: Định nghĩa lớp `RealESRNetModel`, mô hình chính của Real-ESRGAN.

#### **d. `utils/`**
Chứa các hàm tiện ích hỗ trợ.

- **`utils.py`**: Chứa lớp `RealESRGANer` để thực hiện quá trình nâng cấp độ phân giải ảnh, cũng như các hàm hỗ trợ khác như `PrefetchReader` và `IOConsumer`.

### 3. **Các tệp cấu hình**
- **`options/`**: Chứa các tệp cấu hình YAML để huấn luyện mô hình, ví dụ: `finetune_realesrgan_x4plus.yml`.

### 4. **Các script hỗ trợ**
- **`scripts/`**: Chứa các script hỗ trợ như tạo meta-info cho dữ liệu.
  - **`generate_meta_info_pairdata.py`**: Tạo tệp meta-info từ các thư mục ảnh.

### 5. **Tài liệu**
- **`docs/`**: Chứa các tài liệu hướng dẫn sử dụng và huấn luyện mô hình.
  - **`Training.md`**: Hướng dẫn chi tiết về quá trình huấn luyện mô hình.

### 6. **Kết quả**
- **`results/`**: Lưu trữ các kết quả dự đoán từ mô hình.

### 7. **Yêu cầu**
- **`requirements.txt`**: Liệt kê các thư viện cần thiết để chạy dự án.

### 8. **Giới thiệu**
- **`README.md`**: Giới thiệu tổng quan về dự án, cách cài đặt, sử dụng và các tính năng chính.


######################################################################
###data : sử dụng bộ data ảnh chất lượng cao và chất lượng thấp là: #DIV2K_train_HR
#Flickr2K_HR
#Link: 

######################################################################
###Kết quả đạt được
###Thu được các model sau(tùy tham số):
#realesrgan-x4plus (default)
#realesrnet-x4plus (faster realesrgan-x4plus but low quality )
#realesrgan-x4plus-anime (optimized for anime images, small model size)
#realesr-animevideov3 (animation video)

#######################################################################Requirement:
#pip install basicsr
#pip install facexlib
#pip install gfpgan
#pip install -r requirements.txt
#python setup.py develop

###Lưu ý: chương trình có thể không chạy hoặc báo lỗi conflict/not found version torch. tùy vào máy anh phải tải 2 phiên bản torch và torchvision không xung đột nhau. máy e thì
pip install torch==1.21.1 torchvision==0.13.1
khi thử trên máy bạn khác cấu hình này không chạy mà phải up lên torch và torchvison mới nhất. torch và torchvision mới nhất thì máy em lại không chạy!

######################################################################
###CÁCH CHẠY

#di chuyển vào folder chứa mã nguồn 
#cd Real-ESRGAN-master

#set up package:

#pip install basicsr
#pip install facexlib
#pip install gfpgan
#pip install -r requirements.txt
#python setup.py develop
#pip install torch==1.21.1 torchvision==0.13.1

#Download pre-trained models: RealESRGAN_x4plus.pth
#curl -L -o weights\RealESRGAN_x4plus.pth https://github.com/xinntao/Real-ESRGAN/releases/download/v0.1.0/RealESRGAN_x4plus.pth

#model tải xong sẽ ở trong folder weights. Anh có thể chọn 1 trong 4 model. model RealESRGAN_x4plus.pth có chất lượng cao nhất với ảnh.

#dùng scripts sau để chạy chương trình:

#tải 1 ảnh mờ rồi đặt ảnh vào folder inputs. hoặc dùng ảnh có sẵn của nhóm.

#python inference_realesrgan.py -n RealESRGAN_x4plus -i inputs/input.jpg -o results --outscale 4 --face_enhance --fp32

#sau -n anh điền tên model mong muốn
#sau -i anh điền inputs/tên ảnh
#sau -o results không cần đổi
#sau --outscale điền 1 2 4 8 tùy anh muốn chất lượng ảnh cao cỡ đâu và tùy máy nữa.
#nếu trong ảnh có mặt người thì anh thêm --face_enhance để nâng cao chất lượng khuôn mặt
#nếu sử dụng để upscale video thì điền thêm --fp32 

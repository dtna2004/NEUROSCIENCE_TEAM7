# Real-ESRGAN

## Giới thiệu

**Real-ESRGAN** là một mô hình siêu phân giải ảnh (Super-Resolution) tiên tiến, được xây dựng dựa trên kiến trúc ESRGAN và được tối ưu hóa để cung cấp chất lượng hình ảnh cao. Dự án này bao gồm các module chính, các tệp cấu hình, các script hỗ trợ, tài liệu hướng dẫn và các kết quả dự đoán từ mô hình.

## Cấu trúc mã nguồn

### 1. Cấu trúc thư mục

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

### 2. Các module chính

#### a. `archs/`
Chứa các kiến trúc mạng được sử dụng trong mô hình Real-ESRGAN.

- **`srvgg_arch.py`**: Định nghĩa lớp `SRVGGNetCompact`, một mạng VGG-style nhỏ gọn cho siêu phân giải.
- **`discriminator_arch.py`**: Định nghĩa lớp `UNetDiscriminatorSN`, một bộ phân biệt U-Net với chuẩn hóa phổ.

#### b. `data/`
Chứa các lớp dataset để xử lý dữ liệu huấn luyện và kiểm thử.

- **`realesrgan_paired_dataset.py`**: Định nghĩa lớp `RealESRGANPairedDataset` để xử lý dữ liệu cặp (ảnh thấp phân giải và cao phân giải).

#### c. `models/`
Chứa các mô hình huấn luyện.

- **`realesrnet_model.py`**: Định nghĩa lớp `RealESRNetModel`, mô hình chính của Real-ESRGAN.

#### d. `utils/`
Chứa các hàm tiện ích hỗ trợ.

- **`utils.py`**: Chứa lớp `RealESRGANer` để thực hiện quá trình nâng cấp độ phân giải ảnh, cũng như các hàm hỗ trợ khác như `PrefetchReader` và `IOConsumer`.

### 3. Các tệp cấu hình
- **`options/`**: Chứa các tệp cấu hình YAML để huấn luyện mô hình, ví dụ: `finetune_realesrgan_x4plus.yml`.

### 4. Các script hỗ trợ
- **`scripts/`**: Chứa các script hỗ trợ như tạo meta-info cho dữ liệu.
  - **`generate_meta_info_pairdata.py`**: Tạo tệp meta-info từ các thư mục ảnh.

### 5. Tài liệu
- **`docs/`**: Chứa các tài liệu hướng dẫn sử dụng và huấn luyện mô hình.
  - **`Training.md`**: Hướng dẫn chi tiết về quá trình huấn luyện mô hình.

### 6. Kết quả
- **`results/`**: Lưu trữ các kết quả dự đoán từ mô hình.

### 7. Yêu cầu
- **`requirements.txt`**: Liệt kê các thư viện cần thiết để chạy dự án.

### 8. Giới thiệu
- **`README.md`**: Giới thiệu tổng quan về dự án, cách cài đặt, sử dụng và các tính năng chính.

## Dữ liệu

Dự án sử dụng các bộ dữ liệu ảnh chất lượng cao và thấp như sau:

- **DIV2K_train_HR**
- **Flickr2K_HR**

Liên kết tải dữ liệu: [https://drive.google.com/drive/u/1/folders/1p-72dwX5oAumZglD6eAYjFoNBByAtwTj]

## Kết quả đạt được

Dự án đã thu được các mô hình sau (tùy tham số):

- **realesrgan-x4plus** (mặc định)
- **realesrnet-x4plus** (nhanh hơn realesrgan-x4plus nhưng chất lượng thấp hơn)
- **realesrgan-x4plus-anime** (được tối ưu hóa cho hình ảnh anime, kích thước mô hình nhỏ)
- **realesr-animevideov3** (đối với video hoạt hình)

## Yêu cầu cài đặt

Để chạy dự án, bạn cần cài đặt các thư viện sau:
```bash
pip install basicsr
pip install facexlib
pip install gfpgan
pip install -r requirements.txt
python setup.py develop
```

**Lưu ý:** Chương trình có thể không chạy hoặc báo lỗi về xung đột phiên bản torch. Hãy đảm bảo rằng bạn cài đặt các phiên bản thích hợp của torch và torchvision. Ví dụ:

- Trên máy của tôi, tôi sử dụng:

  ```bash
  pip install torch==1.21.1 torchvision==0.13.1
  ```

- Trên máy bạn có thể cần sử dụng các phiên bản mới hơn của torch và torchvision.

## Cách chạy

1. **Di chuyển vào thư mục chứa mã nguồn:**

    ```bash
    cd Real-ESRGAN-master
    ```

2. **Cài đặt các gói phụ thuộc:**

    ```bash
    pip install basicsr
    pip install facexlib
    pip install gfpgan
    pip install -r requirements.txt
    python setup.py develop
    pip install torch==1.21.1 torchvision==0.13.1
    ```

3. **Tải các mô hình đã huấn luyện:**

    ```bash
    curl -L -o weights/RealESRGAN_x4plus.pth https://github.com/xinntao/Real-ESRGAN/releases/download/v0.1.0/RealESRGAN_x4plus.pth
    ```

    Mô hình tải xuống sẽ được lưu trong thư mục `weights`. Bạn có thể chọn một trong các mô hình sau:

    - **RealESRGAN_x4plus.pth**: Chất lượng cao nhất với ảnh.

4. **Chạy chương trình:**

    ```bash
    python inference_realesrgan.py -n RealESRGAN_x4plus -i inputs/input.jpg -o results --outscale 4 --face_enhance --fp32
    ```

    Giải thích các tham số:

    - `-n`: Tên mô hình mong muốn.
    - `-i`: Đường dẫn đến ảnh đầu vào.
    - `-o`: Thư mục lưu kết quả (không cần đổi).
    - `--outscale`: Tỷ lệ phóng to ảnh (có thể là 1, 2, 4, 8 tùy theo yêu cầu và cấu hình máy).
    - `--face_enhance`: Tăng cường chất lượng khuôn mặt (nếu có mặt người trong ảnh).
    - `--fp32`: Sử dụng chế độ fp32 (nếu sử dụng để upscale video).

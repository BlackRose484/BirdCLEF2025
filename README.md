## Giới thiệu cuộc thi ##
Ngày nay việc biến đổi khí hậu cùng với nạn săn bắt trái phép đã khiến cho vấn đề về sụt giảm đa dạng sinh học trở nên cấp thiết. Từ đó, việc nghiên cứu và giám sát số lượng các loài cần được thực hiện thường xuyên và liên tục. Tuy nhiên với các động vật di trú như các loài chim, việc theo dõi, giám sát số lượng loài di trú với các phương pháp thủ công là một bài toán khó và tốn kém với các nhà nghiên cứu. \n
Trong cuộc thi này, các nhà nghiên cứu tại Cornell Lab of Ornithology mong muốn có thể áp dụng giám sát âm thanh thụ động (PAM) kết hợp cùng các mô hình học máy để từ đó xác định được các loài đang trong diện nghiên cứu dựa vào âm học đặc trưng của chúng. Từ đó, các nhà khoa học có thể xác định được số lượng loài, cũng như sự hiện diện của chúng tại các khu vực đặt PAM (các khu vực cần nghiên cứu).
## Phương pháp tiếp cận cơ bản ##
Tổng quan về phương pháp tiếp cận vấn đề trên của nhóm chúng tôi gồm các bước như sau:
### Xử lý dữ liệu và đánh nhãn ###
- Cắt các file âm thanh (.ogg) thành các đoạn âm thanh nhỏ (10s đầu tiên của file).
- Chuyển đổi file âm thanh đã cắt (.ogg) sang biểu diễn dưới dạng tần số mel (Melspectrogram) và lưu dưới dạng ma trận ảnh.
- Đánh nhãn cho các ảnh, mỗi ảnh có vector nhãn 206 chiều, và mỗi ảnh sẽ có nhiều hơn 1 nhãn dán (primary label và secondary labels).
### Mô hình ###
- Sử dụng backbone là backbone của các mô hình CNNs (EfficientNetB0 - pretrained) để trích xuất đặc trưng không gian của các Melspectrogram, từ đó tìm ra pattern riêng cho từng loài.
- Đầu ra của mô hình là layer classifier 206 đầu ra, dự đoán xác suất từng lớp.
### Huấn luyện ###
- Thực hiện huấn luyện với tập dữ liệu đề bài đã cho.
- Hàm loss Binary Cross-entropy Loss.
- Optimizer được sử dụng là ADAM
## Cải tiến giữa các phiên bản ##
- Version 1.0: Unfreeze backbone
- Version 2.0: Sử dụng hybrid loss: Sử dụng hàm loss có trọng số giữa Focal Loss và BCE
- Version 3.0: Sử dụng kĩ thuật mixup: Mixup dữ liệu để tăng cường số lượng bản ghi, cũng như độ khó của tập huấn luyện
- Version 4.0: Human voice detection: Loại bỏ tiếng người ra khỏi file âm học
- Version 5.0: Bổ sung dữ liệu: Tăng cường thêm các dữ liệu của cuộc thi từ các năm trước đó
- Version 6.0 (Finally): Ensemble models: Thực hiện ensemble các phiên bản mô hình CNNs lại


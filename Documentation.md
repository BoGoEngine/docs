# Tài liệu dự án IBus BoGoEngine #

## 1. Hoàn cảnh ra đời dự án: ##

Trong hoàn cảnh phần mềm tự do nguồn mở (FOSS) đang phát triển mạnh và tạo nên những giá trị mới về kinh tế, an ninh và giáo dục của Việt Nam, 
việc có một bộ gõ tiếng Việt hoàn chỉnh và tuân theo các tiêu chuẩn và triết lý của FOSS là vô cùng cần thiết. Phần mềm ibus-unikey của tác giả
 Lê Quốc Tuấn (mr.lequoctuan@gmail.com) và Lê Kiến Trúc (afterlastangel@ubuntu-vn.org) đã đáp ứng khá tốt về tính năng sử dụng của người dùng FOSS Việt.
 Tuy vậy phần mềm này gặp phải một số vấn đề về kĩ thuật cũng như triết lý phần mềm tự do nguồn mở:
 
 * Sử dụng kĩ thuật preeedit gây ra các phiền phức cho người dùng như: xuất hiện gạch chân khi gõ tiếng Việt, hiển thị kí tự khi gõ mật khẩu khi gõ ở terminal
 và đặc biệt nhảy kí tự cần gõ khi di duyển giữa các cửa sổ đang sử dụng ibus-unikey
 
 * Mã nguồn không được có quy tắc (convention), chú thích, không có tài liệu (documentation) cho người phát triển. Đây là một điều rất xấu trong cộng đồng FOSS, 
 khi mà sự kế thừa và và phát triển được đề cao và được xem là sự sống còn cho phần mềm.
 
IBus BoGoEngine được tạo ra để khắc phục các nhược điểm trên. Việc khắc phục lỗi preeedit string được coi là tính năng đáng chú ý của IBus BoGoEngine.
Ngoài ra, nhóm phát triển còn muốn tạo ra một phần mềm theo đúng tinh thần FOSS bằng cách cung cấp documentation, viết code cẩn thận, có quy tắc và chú thích, 
phân phối dưới giấy phép GNU GPL version 3. Nhóm phát triển hi vọng rằng, phần mềm này luôn được hoàn thiện.
 
## 2. Thiết kế của IBus BoGoEngine: ##
 
IBus BoGoEngine gồm 2 thành phần:
 
 - BoGoEngine: engine xử lý tiếng Việt do Nguyễn Hà Dương (cmpitg@gmail.com) viết. Engine này được viết bằng C đồng thời cung cấp các phương thức để gọi 
 các hàm của engine từ nhiều ngôn ngữ C, Python, Vala... Engine này hiện này vẫn được tiếp túc phát triển.
 - IBus Engine: engine của IBus, để xử lý các phím nhập vào. Dựa trên các hàm sẵn có của thư viện ibus, engine này xử lý các phím do người dùng nhập 
 và gọi hàm của BoGoEngine để xử lý tiếng Việt, tạo ra các xâu tiếng Việt cho người dùng.

Tài liệu phát triển của IBus BoGoEngine được ghi trong file API.html đi kèm với mã nguồn của phần mềm.
   
## 3. Các yêu cầu về biên dịch và phát triển: ##

 - cmake: Công cụ tạo Makefiles (cmake >= 2.6)
 - gcc: trình biên dịch C/C++ của GNU (gcc)
 - Thư viện gtkmm dành cho nhà phát triển (libgtkmm-dev >= 2.4)
 - Thư viện ibus dành cho nhà phát triển (libibus-1.0-dev, libibus-qt-dev, python-ibus)
 - python: trình biên dịch python (python-2.7.3)
 - gir1.2-ibus
 
 _Lưu ý_:
 
  - Tên thư viện có thể khác nhau tùy theo bản phân phối linux.
  - Nên sử dụng các bản phân phối linux mới nhất.
  
## 4. Các yêu cầu về việc sử dụng: ##
  
  - ibus
  
  - ibus-qt
  
## 5. Hướng dẫn thiết lập môi trường sử dụng và phát triển: ##

Sau khi cài đặt các gói trên, thêm các dòng sau vào file $HOME/.profile:

    export GTK_IM_MODULE=ibus
    export XMODIFIERS=@im=ibus
    export QT_IM_MODULE=xim

## Biên dịch BoGoEngine: ##

Tải mã nguồn của phần mềm về, giải nén ra thư mục BoGoEngine. Việc biên dịch yêu cầu cái trước các thư viện và công cụ được đề cập ở trên.

### Biên dịch BoGoEngine: ###

  Tại thư mục BoGoEngine thực hiện lệnh sau:

    cd bogo
    mkdir build
    cd build
    cmake ..
    make
    sudo make install

### Biên dịch engine cho IBus: ###
  
  Tại thư mục BoGoEngine thực hiện lệnh sau:

    cd ibus-bogo-python/
    mkdir build
    cd build
    cmake ..
    make
    sudo make install

### Chạy IBus BoGoEngine để test hoặc sử dụng luôn: ###
  
  Tại thư mục BoGoEngine thực hiện lệnh sau:
  
    ibus-daemon -xdr
    python ibus-bogo-python/engine/BoGoMain.py

 
 
 

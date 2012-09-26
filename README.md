# Tài liệu dự án IBus BoGoEngine #

## 1. Hoàn cảnh ra đời dự án: ##

Trong hoàn cảnh phần mềm tự do nguồn mở (FOSS) đang phát triển mạnh và tạo nên 
những giá trị mới về kinh tế, an ninh và giáo dục của Việt Nam thì việc có một 
bộ gõ tiếng Việt hoàn chỉnh và tuân theo các tiêu chuẩn và triết lý của FOSS
là vô cùng cần thiết. Phần mềm ibus-unikey của tác giả Lê Quốc Tuấn (mr.lequoctuan@gmail.com)
và Lê Kiến Trúc (afterlastangel@ubuntu-vn.org) đã đáp ứng khá tốt về tính năng
sử dụng của người dùng FOSS Việt. Tuy vậy phần mềm này gặp phải một số vấn đề 
về kỹ thuật cũng như triết lý phần mềm tự do nguồn mở:
 
 * Sử dụng kỹ thuật preeedit gây ra các phiền phức cho người dùng như: xuất hiện
 gạch chân khi gõ tiếng Việt, hiển thị kí tự khi gõ mật khẩu khi gõ ở terminal
 và đặc biệt nhảy kí tự cần gõ khi di duyển giữa các cửa sổ đang sử dụng ibus-unikey
 
 * Mã nguồn không được có quy tắc (convention), chú thích, không có tài liệu 
 (documentation) cho người phát triển. Đây là một điều rất xấu trong cộng đồng FOSS, 
 khi mà sự kế thừa và và phát triển được đề cao và được xem là sự sống còn cho phần mềm.
 
IBus BoGoEngine được tạo ra để khắc phục các nhược điểm trên. Việc khắc phục lỗi
preeedit string được coi là tính năng đáng chú ý của IBus BoGoEngine.
Ngoài ra, nhóm phát triển còn muốn tạo ra một phần mềm theo đúng tinh thần FOSS
bằng cách cung cấp documentation, viết code cẩn thận, có quy tắc và chú thích, 
phân phối dưới giấy phép GNU GPL version 3. 

Nhóm phát triển hi vọng rằng phần mềm này sẽ được cộng đồng đón nhận và tiếp tục hoàn thiện.
 
## 2. Thiết kế của IBus BoGoEngine: ##
 
IBus BoGoEngine gồm 2 thành phần:
 
 - BoGoEngine: engine lõi xử lý tiếng Việt do Nguyễn Hà Dương (cmpitg@gmail.com)
viết. Engine này được viết bằng C++ đồng thời cung cấp các phương thức để gọi 
các hàm của engine từ nhiều ngôn ngữ C, Python, Vala... Engine này hiện nay vẫn
được tiếp tục phát triển.
 - IBus Engine: engine giao tiếp trực tiếp với IBus để xử lý các phím nhập vào.
Dựa trên các hàm sẵn có của thư viện IBus, engine này xử lý các phím do người dùng
nhập và gọi hàm của BoGoEngine để xử lý tiếng Việt, tạo ra các xâu tiếng Việt cho người dùng.

Tài liệu phát triển của IBus BoGoEngine được ghi trong file API.html đi kèm với 
mã nguồn của phần mềm.
   
## 3. Biên dịch: ##

### Các yêu cầu khi biên dịch ###
 - cmake: Công cụ tạo Makefiles (cmake >= 2.6)
 - gcc: trình biên dịch C/C++ của GNU (gcc)
 - Thư viện glibmm dành cho nhà phát triển (libglibmm-dev >= 2.4)
 - Thư viện ibus dành cho nhà phát triển (libibus-1.0-dev, libibus-qt-dev, python-ibus)
 - python: trình biên dịch python (python-2.7.3)
 - gir1.2-ibus
 
_Lưu ý_:
 
- Tên thư viện có thể khác nhau tùy theo bản phân phối Linux.
- Nên sử dụng các bản phân phối Linux mới nhất.

Với Ubuntu/Debian thì có thể sử dụng lệnh sau để tải tất cả các gói cần cho việc build:

    sudo apt-get install build-essential cmake libglibmm-2.4-dev

Cho việc sử dụng:

    sudo apt-get install gir1.2-ibus-1.0 python-xlib
  
Sau khi cài đặt các gói trên, thêm các dòng sau vào file $HOME/.profile và logout, login
để cập nhật thay đổi:

    export GTK_IM_MODULE=ibus
    export XMODIFIERS=@im=ibus
    export QT_IM_MODULE=xim

Nếu bạn bị lỗi khi gõ trong các ứng dụng Qt kiểu "haf" => "haà" thì hãy thử gỡ
cài đặt gói ibus-qt4.

### Hướng dẫn biên dịch ###

Tải mã nguồn mới nhất về sử dụng các lệnh sau (cần có phần mềm git):

    mkdir BoGoEngine
    cd BoGoEngine
    git clone https://github.com/BoGoEngine/bogo.git
    git clone https://github.com/BoGoEngine/ibus-bogo-python.git

#### Biên dịch BoGoEngine: ####

Tại thư mục BoGoEngine, thực hiện lệnh sau:

    cd bogo
    mkdir build
    cd build
    cmake ..
    make
    sudo make install
    sudo ldconfig

_Lưu ý_:

Nếu bạn sử dụng các HĐH dòng Fedora/Redhat/Centos thì cần phải thêm dòng "/usr/local/lib"
vào file /etc/ld.so.conf trước khi chạy ldconfig.

Để gỡ cài đặt:
    
    cd bogo/build
    sudo make uninstall

#### Biên dịch engine cho IBus: ####
  
Tại thư mục BoGoEngine, thực hiện lệnh sau:

    cd ibus-bogo-python/
    mkdir build
    cd build
    cmake ..
    make
    sudo make install

Sau đó trong trang Tùy thích > Kiểu gõ của IBus sẽ xuất hiện engine "BOGO" trong
ngôn ngữ Tiếng Việt.

Để gỡ cài đặt:
    
    cd ibus-bogo-python/build
    sudo make uninstall

#### Chạy IBus BoGoEngine để test hoặc sử dụng luôn: ####
  
Tuy nhiên, bạn cũng có thể test nhanh BoGo mà không cần cài đặt gói ibus-bogo-python.

Trước hết cần cài bogo như hướng dẫn ở mục "Biên dịch BoGoEngine".
Trong một của sổ dòng lệnh bất kỳ, chạy lệnh:

    $ ibus-daemon -xvr

    -x : Xim (đóng giả phương thức nhập liệu của X)
    -v : verbose (in ra các đoạn debug)
    -r : replace (thay thế ibus-daemon hiện tại)

Sau đó, tại thư mục BoGoEngine thực hiện lệnh sau:
  
    python ibus-bogo-python/engine/BoGoMain.py

Engine "BOGO" sẽ đang là engine được lựa chọn trong IBus và bạn có thể gõ tiếng Việt bằng BoGo.
Nếu bạn có thể thấy những đoạn debug được in ra trong cửa sổ terminal khi gõ tiếng Việt
tức là mọi thứ đang chạy tốt.

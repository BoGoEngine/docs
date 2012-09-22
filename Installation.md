# Tài liệu hướng dẫn cài đặt ibus-bogo #

## Tải mã nguồn từ git ##
 - Yêu cầu: git
 - Sử dụng lệnh sau để tải mã nguồn dự án:
    git clone git://github.com/haqduong/ibus-bogo.git

## Biên dịch và cài đặt ##

** Yêu cầu để biên dịch **

 - cmake: Công cụ tạo Makefiles (cmake >= 2.6)
 - gcc: trình biên dịch C/C++ của GNU (gcc)
 - Thư viện gtkmm dành cho nhà phát triển (libgtkmm-dev >= 2.4)
 - Thư viện ibus dành cho nhà phát triển (libibus-1.0-dev, libibus-qt-dev, python-ibus)
 - python: trình biên dịch python (python-2.7.3)

** Yêu cầu để sử dụng **

 - ibus >= 1.4
 - ibus-qt
 - gir1.2-ibus1.0 (tên package trong Ubuntu)

_Lưu ý_:

- Tên thư viện có thể khác nhau tùy theo bản phân phối linux.
- Nên sử dụng các bản phân phối linux mới nhất.

### Cách 1: sử dụng script tự động hóa ở thư mục gốc của dự án ###
Sử dụng lệnh:
    chmod u+x easy-install.sh
    ./easy-install.sh

### Cách 2: biên dịch thủ công ###

#### Biên dịch BoGoEngine: ####

  Tại thư mục BoGoEngine thực hiện lệnh sau:

    cd bogo
    git submodule init
    git submodule update
    mkdir build
    cd build
    cmake ..
    make
    sudo make install

#### Biên dịch engine cho IBus: ####
  
  Tại thư mục BoGoEngine thực hiện lệnh sau:

    cd ibus-bogo-python/
    mkdir build
    cd build
    cmake ..
    make
    sudo make install

#### Chạy IBus BoGoEngine để test hoặc sử dụng luôn: ####
  
  Tại thư mục BoGoEngine thực hiện lệnh sau:
  
    ibus-daemon -xdr
    python ibus-bogo-python/engine/BoGoMain.py

## Thiết lập môi trường để sử dụng và phát triển ##

Sau khi cài đặt các gói trên, thêm các dòng sau vào file $HOME/.profile:

    export GTK_IM_MODULE=ibus
    export XMODIFIERS=@im=ibus
    export QT_IM_MODULE=xim

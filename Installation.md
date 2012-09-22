# Tài liệu hướng dẫn cài đặt ibus-bogo #

## Tải mã nguồn từ git ##
 - Yêu cầu: git
 - Sử dụng lệnh sau để tải mã nguồn dự án:
    git clone git://github.com/haqduong/ibus-bogo.git

## Biên dịch và cài đặt ##

### Cách 1: sử dụng script tự động hóa ở thư mục gốc của dự án ###
Sử dụng lệnh:
    chmod u+x easy-install.sh
    ./easy-install.sh

### Cách 2: biên dịch thủ công ###

#### Biên dịch BoGoEngine: ####

  Tại thư mục BoGoEngine thực hiện lệnh sau:

    cd bogo
    mkdir build
    git submodule init
    git submodule update
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

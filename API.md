# Tài liệu phát triển IBus BoGoEngine #

## Giới thiệu chung: ##

Phần quan trọng nhất của của IBus BoGoEngine (gọi tắt là engine) là class Engine tại file **BoGoEngine.py**. 
Class engine là kế thừa của class IBus.Engine được thiết kế bởi nhà phát triển IBus.
Nhiệm vụ của người phát triển engine cho IBus là triển khai các phương thức (method) 
của class IBus.Engine và đưa thêm các thành phần thuộc tính (property)
và phương thức mới nhằm tạo ra các chức năng cần thiết. 
Dưới đây là các phương thức và thuộc tính của class Engine trong IBusBoGoEngine.

## Một số khái niệm:##

*client*: cửa sổ tại đó IBus xử lý kí tự.

*engine*: engine xử lý kí tự của IBus

*BoGoEngine*: engine xử lý tiếng Việt được xử dụng. Engine này được viết bằng C và cung cấp các hàm để gọi từ Python.

## class Engine(IBus.Engine) ##

### Instance Variables: ###

- `__charset_list` : Danh sách các bảng mã. Tạm thời IBus BoGoEngine hỗ trợ 2 bảng mã: UTF8 và TCVN3

- `__prop_list` : Danh sách các thuộc tính. Danh sách này dùng để tạo giao diện người dùng. Tạm thời, người dùng có thể chọn giữa UTF8 và TCVN3

- `__charset_prop_menu` : Danh sách thuộc tính bảng mã

- `is_faking_backspace` : Biến boolean, giá trị True nếu đang thực hiện tạo backspace giả. False nếu ngược lại.

- `number_fake_backspace` : Số lượng backspace giả cần tạo. Giá trị này được tính bằng cách gọi hàm `get_nbackspace_and_string_to_commit(self):`

### Methods: ###

* `__init__(self)` : Khởi tạo engine

* `__init_charset_prop_menu(self)` : Khởi tạo danh sách thuộc tính bảng mã
      
* `__init_props(self)` : Khởi tạo danh sách thuộc tính

* `reset_engine(self)` : Reset engine

* `do_process_key_event(self, keyval, keycode, state)`: Xử lý phím được nhập vào từ người dùng.

  * Tham số: 

    * _keyval_: giá trị của phím. Được định nghĩa trong tài liệu của IBus
    * _keycode_: mã của phím 
    * _state_: có giữ các phím control, shift,... hay không

  * Giá trị trả lại: `True` nếu muốn việc xử lý chỉ dừng lại ở engine. `False` nếu muốn phím gõ vào được xử lý bởi hệ thống (x-server)

* `commit_utf8(self, string)`: In ra client xâu UTF8 `string`
 
* `commit_tcvn3(self, string)`: In ra client xâu TCVN3 `string`

* `commit_result(self, string)`: In ra client xâu `string`. Hàm này được gán là một trong hai hàm `commit_utf8(self, string)` hoặc `commit_tcvn3(self, string)`
tuỳ thuộc vào thuộc tính bảng mã được chọn.
  
* `get_nbackspace_and_string_to_commit(self):` Trả về hai giá trị: Giá trị đầu tiên là số backspace giả cần tạo. Giá trị thứ hai là xâu sau khi được xử lý tiếng Việt.

* `is_character(self, keyval)`: Kiểm tra xem phím gõ vào có phải là ký tự không.

* `do_focus_in(self)`: Các thao tác khi client được chọn
   
* `do_focus_out(self)`: Các thao tác khi chuyển từ client được chọn ra chỗ khác
    
* `do_property_activate(self, prop_name, state)`: Thay đổi thuộc tính của engine trong `__prop_list`
     
* `forward_key_event(keysym, keycode, state)`: Tạo 1 key event giả với keycode, keysym, state như định nghịa trong `do_process_key_event`

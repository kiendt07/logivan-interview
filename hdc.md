
Mình gọi người sử dụng logivan để chuyển hàng là: client
Công ty/cá nhân nhận chở hàng là: driver

Thì theo bài toán trên, ta có các dữ liệu sau:

1) Vị trí của đơn hàng cần vận chuyển (nơi lấy hàng và nơi dỡ hàng). Tất cả đều là dữ liệu người dùng tự nhập. ví dụ: "Số 59, Đường số 6, Khu Phố 2, Hiệp Bình Chánh, Thủ đức" là nơi client muốn bốc hàng.

2) Một danh sách các driver, mỗi driver lại có 1 mảng các vị trí mà họ có thể chuyển hàng. 

Với dữ liệu như trên, để có thể cho ra kết quả những đơn hàng phù hợp (phù hợp về địa điểm nhận và giao hàng) cho những driver

Thì phương án mình nghĩ được duy nhất là: vét cạn dữ liệu.

Bước 1: lấy giá trị chuỗi "address" của vị trí bốc hàng (do người dùng nhập) đi so khớp với từng phần tử vị trí bốc hàng trong mảng location của từng driver ==> nếu driver nào khớp thì note lại để chuyển qua bước 2.

Bước 2: lấy giá trị chuỗi "address" của vị trĩ dỡ hàng (do người dùng nhập) đi so khớp với từng phần tử vị trí dỡ hàng trong mảng location của những driver đã pass bước 1.


Bước 3: Trả về kết quả những driver tìm được cho người dùng.

NOTE 1: 
+) Có 1 điểm không ổn mình thấy đó là khi để người dùng nhập dữ liệu thô cho vị trí họ muốn bốc hàng và dỡ hàng, thì sẽ dễ gây nhầm lẫn (họ có thể nhập sai, thiếu dấu...) hoặc nếu họ có nhập đúng thì những địa chỉ quá chi tiết như trên ví dụ trên thì cũng làm thuật toán phức tạp đi rất nhiều.

+) Nếu so khớp chuỗi thô như trên thì theo mình còn nhớ khi học, mình đề xuất sử dụng thuật toán tìm kiếm so khớp chuỗi KMP, đây là giải thuật tìm khớp chuỗi có độ phức tạp thấp nhất mà mình từng được học.


############################


Nếu được đề xuất thêm hướng giải quyết bài toán thì mình sẽ đề xuất theo hướng sau:

1) Khi client tiến hành đặt vận chuyển trên ứng dụng, ta yêu cầu client lựa chọn "vận chuyển nội tỉnh" hoặc "vận chuyển ngoại tỉnh":

vận chuyển nội tỉnh là: điểm bốc hàng và dỡ hàng cùng nằm trong 1 tỉnh.
vận chuyển ngoại tỉnh là: điẻm bốc hàng và dỡ hàng nằm ở 2 tỉnh khác nhau.

2) Khi một driver tiến hành đăng ký tài khoản thì yêu cầu lựa chọn option về vị trí họ có thể nhận và chuyển hàng:

i) chỉ vận chuyển trong một tỉnh (ví dụ: driver_a có thể lựa chọn chỉ chuyển hàng trong tỉnh Lạng Sơn, driver_b lựa chọn chỉ chuyển hàng trong tình Bắc Can và Quảng Ninh ==> có thể lựa chọn nhiều tỉnh)

ii) chỉ vẩn chuyển ngoại tỉnh (ví dụ: driver_c lựa chọn chuyển hàng: lấy hàng ở Nam Định và dỡ hàng ở Thái Bình ==> đây là tuyến Nam Đinh - Thái Bình)

iii) cả vận chuyển nội tỉnh và ngoại tỉnh (gồm cả 2 trường hợp trên)

NOTE 2:

+) Khi driver đăng ký trường hợp 1 là chỉ chọn nội tỉnh thì yêu cầu họ select vào tỉnh đó. (dữ liệu do logivan cung cấp, chỉ cung câp giao diện để driver lựa chọn qua click chuột).

+) Khi driver đăng ký trường hợp 2 là "giao hàng ngoại tỉnh" ==> yêu cầu họ CHỌN điểm đi và đến.

+) Khi driver đăng ký trường hợp 3 là giao hàng cả nội tỉnh và ngoại tỉnh thì yêu cầu họ tiến hàng 2 bước bên trên.


Logic:

Client A: Chọn muốn chuyển hàng nội tỉnh và tỉnh đó là Hà Nội --> Hệ thống query tất cả những driver đang trong trạng thái sẵn sàng vận chuyển trong tỉnh Hà Nội ra....

Client B: Chọn muốn chuyển hàng ngoại tỉnh và tỉnh đi là Đồng Nai, tỉnh đến là Bình Dương --> Hệ thống query tất cả những driver loại ii và iii có tỉnh đi là Đồng Nai --> trong những driver đã query đượch hệ thống sẽ search tiếp và cho ra kết quả là các driver có tỉnh đến là Bình Dương


NOTE 3: 

+) Trong trường hợp logivan phát triển lớn hơn nữa và trong khu vực giới hạn như trên vẫn ra quá nhiều tài xế thì ta có thể phát triển theo hướng phân nhỏ ra tiếp --> ví dụ như: Hà Nội phân rã ra tiếp thành các quận thuộc Hà Nội --> Khi driver đăng ký và khi client đặt hàng thì đều select tỉnh trước rồi select quận sau ==> từ đó tiếp tục chia nhỏ làm giảm quy mô driver.


+) Theo mình thì nên phân chia nhỏ đến một mức nhất định, còn vị trí chính xác bốc và dỡ hàng thì nên để cho driver và client thương lượng và trao đổi (vì địa chỉ thành phố khá dễ miêu tả trong khi nhiều vùng ngoại ô thì rất khó để biểu đạt bằng dữ liệu thô, nên để cho 2 bên tự thương thảo về vị trí chính xác nhận và trả hàng.).

+) Ngoài ra cũng có thể các thuật toán tìm kiếm đường đi ngắn nhất như Dijkstra (mình không có nêu trong phần hướng giải quyết vì mình chưa biết cách lấy trọng số độ dài ở đâu và như thế nào nên chỉ đê xuất được cách bên trên).













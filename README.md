# Memory in JavaScript 🤔

*Các ngôn ngữ khác (VD như C) có các nguyên hàm quản lí bộ nhớ cấp thấp như `malloc()` , `free()` <br>
JS cấp phát bộ nhớ khi mọi thứ (đối tượng, chuỗi.. ) được tạo ra và tự động giải phóng bộ nhớ khi chúng không dùng nữa -> quá trình như vậy gọi là `garbage collection`<br>
Kể cả khi làm việc với các ngôn ngữ bậc cao thì các nhà phát triển cũng nên tìm hiểu về quản lí bộ nhớ (dù đang là quản lí bộ nhớ tự động*

## Bộ nhớ là gì ? 🤷‍♀️
Ở cấp độ phần cứng, bộ nhớ máy tính gồm 1 lượng lớn các **flip flop**. Mỗi flip flop chứa 1 vài bóng bán dẫn có khả nắng lưu trữ 1 bit (được đánh địa chỉ bằng 1 mã định danh)

Những thứ được lưu trữ trong bộ nhớ 
1. Tất cả biến và dữ liệu (được sử dụng bởi tất cả các chương trình máy tính)
2. Mã chương trình (bao gồm cả hệ điều hành)

Khi `trình biên dịch` và `hệ điều hành (chương trình)` phối hợp với nhau sẽ đảm nhiệm hầu hết việc quản lí bộ nhớ

Khi biên dịch mã, `trình biên dịch` sẽ kiểm tra dữ liệu nguyên thuỷ và tính toán số lượng bộ nhớ cần thiết và sữ được cấp phát trong `chương trình` trong không gian `call stack` (không gian mà các biến được cấp phát - không gian ngăn xếp vì khi có hàm được gọi bộ nhớ của chúng sẽ được thêm vào trên bộ nhớ hiện có và khi kết thúc sẽ xoá theo thứ tự LIFO )

## Vòng đời bộ nhớ 🏝️
Allocate -> Use -> Release 
1. Cấp phát: Bộ nhớ được cấp phát bởi hệ điều hành -> cho phép các chương trình sử dụng (tự động bởi ngôn ngữ bậc cao)
2. Sử dụng: Các hoạt động đọc và ghi diễn ra khi các biến được sử dụng
3. Giải phóng: Khi không còn dùng đến nữa

## Cấp phát động ✨
Thật không may, khi tại thời điểm biên dịch chúng ta không biết 1 biến cần bao nhiêu bộ nhớ

Do đó không thể cấp phát bộ nhớ biến cho ngăn xếp ngay được, thay vào đó bộ nhớ được gán từ `heap` space -> cấp phát động 

- Kích thước có thể không biết tại thời điểm biên dịch
- Thực thi tại thời điểm chạy
- Được giao cho heap
- Không có thứ tự cụ thể

Ngược lại ta có cấp phát tĩnh: 

- Kích thước phải biết tại thời điểm biên dịch
-  Thực thi tại thời điểm biên dịch
-  Được giao cho stack
-  LIFO
  
## Cấp phát bộ nhớ trong JS
VD 
```swift
  var n = 374; // cấp phát bộ nhớ cho 1 số

  var s = 'sessionstack'; // cấp phát bộ nhớ cho một chuỗi

  var o = {
    a: 1,
    b: null
  };
  // cấp phát bộ nhớ cho một đối tượng và giá trị mà nó chứa.

  var a = [1, null, 'str'];
  // cấp phát bộ nhớ cho một mảng và các giá trị trong nó

  function f(a) {
    return a + 3;
  } // cấp phát một hàm
```

## Sử dụng bộ nhớ trong JS 
VD Đọc và ghi giá trị của 1 biến, thuộc tính của 1 đối tượng hay kể cả truyền 1 biến vào 1 hàm 

## Giải phóng bộ nhớ 
Đây là nhiệm vụ khó nhất, tìm ra khi nào bộ nhớ không còn cần thiết nữa. Việc này yêu cầu developer xác định nơi nào trong chương trình không cần 1 phần bộ nhớ như vậy nữa và giải phóng nó

Các ngôn ngữ cấp cao nhúng 1 phần mềm gọi là `garbage collector` (theo dõi việc cấp phát và sử dụng bộ nhớ - xác định khi 1 phần bộ nhớ đã cấp phát không được sử dụng trong mọi trường hợp nữa sẽ tự động giải phóng)



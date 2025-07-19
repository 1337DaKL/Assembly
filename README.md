<h1>ASSEMBLY x86(32 bit)- Hợp ngữ cho kiến trúc CPU Intel 32bit<\h1>
  
<h2>1. Giới thiệu</h2>

Hợp ngữ là gì? 
- Là ngôn ngữ bậc thấp để viết các chương trình
- Mỗi kiến trúc CPU sẽ có một loại hợp ngữ khác nhau

Mục tiêu để học asm là gì?
- Dùng để phân tích một file thực thi( exe) mà không cần mã nguồn gốc để tiến hành xem thuật toán, hành vi, crack, ... Hay còn gọi là dịch ngược( reverse engineering), một nhiệm vụ trong chuyên viên phân tích mã độc.
- Hiểu sâu về hệ thống, virus.

Gợi ý:
- Code Editer: RadASM
- Assembler: Masm
- Debugger: OllyDbg

<h2>2. Kiến thức</h2>

2.1 Các hệ số

- Hệ nhị phân: Trong máy tính mã máy sẽ được biểu diễn dưới dạng các bit, và các bit sẽ bao gồm số nhị phân tức là chỉ gồm số 1 và số 0. Và tất nhiên con người bình thường sẽ không hiểu được nội dung của nó là gì. Ví dụ như: 010101
- Hệ thập lục phân: Đây là hệ đếm có 16 kí tự. Tương tự như thập phân sẽ gồm các số từ 0 - 9. Tuy nhiên hệ số có 16 kí tự tức là còn thiếu 6 kí tự và được thay bằng các kí tự chữ cái như: A( 10) , B( 11), C( 12), D( 13), E( 14), F( 15). Ví dụ như: A96, B57, ...
- Hệ thập phân: Đây là kiểu số mà con người hay dùng nhất. Ví dụ như 56, 57, ...
- Hệ bát phân: Đây là hệ đếm có 8 kí tự chỉ bao gồm các kí tự từ 0 - 7. Ví dụ như 0 , 5 , 675, ...

Vậy làm sao để chuyển đổi giữa các hệ số?

Để chuyển giữa các hệ thì cánh đơn giản nhất mà mình biết đó chính là chuyển sang hệ nhị phân rồi sau đó chuyển sang các hệ còn lại. Ví dụ như muốn chuyển từ hệ thập lục phân sang hệ bát phân. Thì hãy chuyển từ hệ thập lục phân sang nhị phân rồi chuyển từ hệ nhị phân sang bát phân. Vì hệ nhị phân chuyển sang các hệ khác cực kì đơn giản. Cách chuyển chi tiết có thể lên internet search.

Ngoài ra còn phải học các phép toán and, or, not, ...
Học các phương pháp biểu diễn các số có dấu trong hệ nhị phân.

2.2 Các kiểu dữ liệu và kích thước của chúng.

- bit là đơn vị dữ liệu nhỏ nhất trong máy tính.
- 1 byte = 8 bit
- 1 word = 2 byte
- 1 doubleword = 2 word
- 1 quarwword = 2 doubleword

2.3 Cấu trúc của CPU

Thanh ghi dữ liệu
- EAX: 32 bit trong đó có thanh ghi AX 16 bit trong thanh ghi AX gồm 8 bit cao là thanh ghi AH và 8 bit thấp là thanh ghi AL. Là thanh ghi tích lũy: Dùng trong nhập xuất và các lệnh tính toán số học như nhân chia.
<img width="707" height="352" alt="image" src="https://github.com/user-attachments/assets/fa4fed8e-1086-4014-8a53-090b587b6457" />
- EBX: Cấu tạo như EAX. Là thanh ghi cơ sở. Dùng trong đánh dấu địa chỉ, lưu địa chỉ bắt đầu của 1 mảng.
- ECX: Cấu tạo như EAX. Là thanh ghi đếm . Thường dùng trong vòng lặp, đếm số vòng lặp.
- EDX: Cấu tạo như EAX. Là thanh ghi dữ liệu. Có nhiệm vụ tương tự thanh ghi EAX

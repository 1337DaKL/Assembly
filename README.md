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

<h3>2.1 Các hệ số</h3>

- Hệ nhị phân: Trong máy tính mã máy sẽ được biểu diễn dưới dạng các bit, và các bit sẽ bao gồm số nhị phân tức là chỉ gồm số 1 và số 0. Và tất nhiên con người bình thường sẽ không hiểu được nội dung của nó là gì. Ví dụ như: 010101
- Hệ thập lục phân: Đây là hệ đếm có 16 kí tự. Tương tự như thập phân sẽ gồm các số từ 0 - 9. Tuy nhiên hệ số có 16 kí tự tức là còn thiếu 6 kí tự và được thay bằng các kí tự chữ cái như: A( 10) , B( 11), C( 12), D( 13), E( 14), F( 15). Ví dụ như: A96, B57, ...
- Hệ thập phân: Đây là kiểu số mà con người hay dùng nhất. Ví dụ như 56, 57, ...
- Hệ bát phân: Đây là hệ đếm có 8 kí tự chỉ bao gồm các kí tự từ 0 - 7. Ví dụ như 0 , 5 , 675, ...

Vậy làm sao để chuyển đổi giữa các hệ số?

Để chuyển giữa các hệ thì cánh đơn giản nhất mà mình biết đó chính là chuyển sang hệ nhị phân rồi sau đó chuyển sang các hệ còn lại. Ví dụ như muốn chuyển từ hệ thập lục phân sang hệ bát phân. Thì hãy chuyển từ hệ thập lục phân sang nhị phân rồi chuyển từ hệ nhị phân sang bát phân. Vì hệ nhị phân chuyển sang các hệ khác cực kì đơn giản. Cách chuyển chi tiết có thể lên internet search.

Ngoài ra còn phải học các phép toán and, or, not, ...
Học các phương pháp biểu diễn các số có dấu trong hệ nhị phân.

<h3>2.2 Các kiểu dữ liệu và kích thước của chúng.</h3>

- bit là đơn vị dữ liệu nhỏ nhất trong máy tính.
- 1 byte = 8 bit
- 1 word = 2 byte
- 1 doubleword = 2 word
- 1 quarwword = 2 doubleword

<h3>2.3 Cấu trúc của CPU</h3>

<h4>Thanh ghi dữ liệu</h4>

- EAX: 32 bit trong đó có thanh ghi AX 16 bit trong thanh ghi AX gồm 8 bit cao là thanh ghi AH và 8 bit thấp là thanh ghi AL. Là thanh ghi tích lũy: Dùng trong nhập xuất và các lệnh tính toán số học như nhân chia.

<img width="707" height="352" alt="image" src="https://github.com/user-attachments/assets/17a846c6-6f0e-4d2b-8bdf-1c60b7255c96" />


- EBX: Cấu tạo như EAX. Là thanh ghi cơ sở. Dùng trong đánh dấu địa chỉ, lưu địa chỉ bắt đầu của 1 mảng.
- ECX: Cấu tạo như EAX. Là thanh ghi đếm . Thường dùng trong vòng lặp, đếm số vòng lặp.
- EDX: Cấu tạo như EAX. Là thanh ghi dữ liệu. Có nhiệm vụ tương tự thanh ghi EAX

<h4>Thanh ghi con trỏ</h4>

- ESP : gồm 32 bit 16 bit thấp là thanh ghi SP. Thanh ghi con trỏ stack trỏ tới đỉnh hiện thời của stack.
- EBP : Cấu tạo tượng tự ESP. Thanh ghi con trỏ cơ sở tham chiếu  đến các biến tham số sử dụng chương trình con.

<h4>Thanh ghi chỉ số</h4>

- ESI: gồm 32 bit, 16 bí thấp là thanh ghi SI. Thanh ghi địa chỉ nguồn được sử dụng làm địa chỉ nguồn cho các phép toán với xâu.
- EDI: tương tự như ESI. Thanh ghi địa chỉ đích được sử dụng làm địa chỉ đích cho các phép toán với xâu.

<h4>Thanh ghi cờ</h4>

Gồm 16 bit: Mỗi bit sẽ là 1 cờ tuy nhiên không phải bit nào cũng là cờ.

<img width="825" height="144" alt="image" src="https://github.com/user-attachments/assets/380f3e22-7b86-4abe-bee5-5259cf8aa1b5" />

- Cờ tràn (Overflow Flag - OF) bằng 1 khi kết quả của phép toán có dấu lớn hơn so với kích thước của địa chỉ đích.
- Cờ hướng (Direction Flag - DF) xác định hướng trái hay phải cho việc di chuyển hoặc so sánh chuỗi dữ liệu. Khi giá trị DF bằng 0, chuỗi hoạt động lấy từ trái qua phải và ngược lại khi DF bằng 1.
- Cờ ngắt (Interupt Flag - IF) xác định khi nào các ngắt ngoài như nhập dữ liệu từ bàn phím được xử lý. Khi IF bằng 1 thì tín hiệu ngắt sẽ được xử lý, ngược lại thì bỏ qua.
- Cờ dừng (Trap Flag - TF ) hỗ trợ thực thi chương trình theo Single-step mode. Trình Debug chúng ta thường sử dụng sẽ đặt giá trị cho TF, nhờ đó chúng ta có thể thực thi từng lệnh một.
- Cờ dấu (Sign Flag - SF) cho biết kết quả của phép toán số học là âm hay dương. Giá trị của SF tùy thuộc vào giá trị của bit ngoài cùng bên trái (High order bit - Most significant bit). SF bằng 1 nếu kết quả của phép toán số học là một giá trị âm.
- Cờ không (Zero Flag - ZF) thể hiện kết quả của phép toán số học hoặc phép so sánh. Cờ dấu có giá trị bằng 1 khi kết quả của phép toán bằng 0, hoặc phép so sánh cho kết quả bằng nhau. Ngược lại, khi kết quả khác không hoặc so sánh cho kết quả là khác nhau thì ZF bằng 0.
- Cờ nhớ (Carry Flag - CF) chứa giá trị nhớ (nhớ 0, hoặc nhớ 1) của MSB sau khi thực hiện phép toán số học. Ngoài ra, khi thực hiện lệnh dịch bit (shift) hoặc quay (rotate) thì giá trị của bit bị đẩy ra cuối cùng sẽ được lưu tại CF.
- Cờ nhớ phụ trợ (Auxiliary Carry Flag - AF) chứa giá trị nhớ khi chuyển từ bit có trọng số 3 lên bit có trọng số 4 (nhớ từ lower nibble sang high nibble) khi thực hiện phép toán số học.
- Cờ chẵn lẻ (Parity Flag - PF) bằng 0 khi số lượng bit 1 trong trong kết quả của phép toán số học là một số chẵn, và bằng 1 khi số lượng bit 1 là một số lẻ. Trong một số trường hợp, PF còn được dùng để kiểm tra lỗi.

<h4>Thanh ghi đoạn</h4>

- CS: Chứa địa chỉ bắt đầu của Code segment.
- DS: Chứa địa chỉ bắt đầu của Data segment.
- SS: Chứa địa chỉ bắt đầu của Stack segment.
- ES, FS, GS: cung cấp các phân đoạn bổ sung cho việc lưu trữ dữ liệu.

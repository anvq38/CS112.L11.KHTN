# BOT   
BOT (Built-Operation-Transfer, có nghĩa: Xây dựng-Vận hành-Chuyển giao) là hình thức Chính phủ kêu gọi các công ty bỏ vốn xây dựng trước (Built) thông qua đấu thầu, sau đó khai thác vận hành một thời gian (Operation) và sau cùng là chuyển giao ( Transfer) lại cho nhà nước sở tại. Đường cao tốc xuyên quốc gia được xây dựng theo hình thức BOT. Công ty Đa quốc gia Modern Highway trúng thầu, chia toàn bộ con đường thành n đoạn. Theo tính toán của Công ty sau khi chuyển giao con đường cho chính phủ sở tại quản lý thì lãi thu được ở đoạn đường thứ i là ai, ai có thể dương, âm hoặc bằng 0, tức là với từng đoạn con có thể lãi, lỗ hoặc hòa vốn. Từng nhóm các đoạn đường liên tiếp nhau (gọi tắt là khoảng) được chia cho các công ty con thực hiện. Công ty con ASEAM Highway hiện đang có trụ sở ở nước sở tại được quyền chọn trước khoảng tùy ý (có thể là cả con đường). Dĩ nhiên Ban Giám đốc ASEAM Highway muốn chọn khoảng bắt đầu từ đoạn p đến hết đoạn q mang lại
lợi nhuận cao nhất hoặc lỗ ít nhất nếu không có khoảng nào cho lãi. Hãy chỉ ra khoảng cần chọn và lãi thu được. Nếu có nhiều cách chọn thì chỉ ra cách chọn có p nhỏ nhất.


Dữ liệu: Vào từ thiết bị nhập chuẩn:  
- Dòng đầu tiên chứa số nguyên n (1 ≤ n ≤ 106)
- Dòng thứ 2 chứa n số nguyên a1, a2, . . ., an (0 ≤ |ai| ≤ 109 , i = 1 ÷ n)

Kết quả: Đưa ra thiết bị xuất chuẩn trên một dòng 2 số nguyên p, q và lãi thu được.  

Ví dụ:

|INPUT                                   |OUTPUT       |
|----------------------------------------|-------------|
|16                                      |5 15 12      |
|2 -4 5 -8 4 -1 -1 1 1 1 -2 2 4 -6 9 -4  |             |
<script src='https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.5/MathJax.js?config=TeX-MML-AM_CHTML' async></script>

# 1.Abstraction
Tìm vị trí p, q và tổng các phần tử từ vị trí p đến q của dãy a sao cho tổng đó là lớn nhất.   
Toán học: Tìm $p,q \text{ }(1 \le p \le q \le n)$ và $\sum_{i=p}^{q}a_{i}$ sao cho $\sum_{i=p}^{q}a_{i}$ lớn nhất. Nếu có nhiều cách chọn thì chọn $p$ nhỏ nhất.

## Constraint 
- Máy tính để kiểm tra thuật toán là core i3 ($10^7$ operation per second)
- Độ dài dãy $a$ ($n$) không được nhiều hơn $10^6$ ( $0 \le n\le 10^6$ )
- Mỗi phần tử thứ $i$ của dãy $a$ không được vượt quá $10^9$ ( $0 \le a_i \le 10^9$ )

# 2. Pattern Recognition: 
Thuật toán Kadane(thuật toán tìm dãy con lớn nhất). Ý tưởng của thuật toán là quét qua các phần tử của mảng, tính tại từng vị trí tổng lớn nhất có thể của các mảng con kết thúc tại vị trí đó. Mảng con này có thể rỗng khi tổng của các phần tử bằng 0 hoặc có thể chứa nhiều hơn một phần tử so với mảng con lớn nhất tại vị trí trước đó. Đồng thời mảng con lớn nhất kết thúc tại vị trí i được tính dựa trên mảng con lớn nhất kết thúc tại vị trí i-1 -> Bài toán quy hoạch động 

# 3. Algorithm designed: Mã giả

max_sum_present = 0 (dùng để gán tổng lớn nhất cần tìm)

max_ending_at = 0 (dùng để gán giá trị kết thúc của mảng con cần tìm)

start_index = 0 (dùng để gán giá trị bắt đầu của mảng con cần tìm)

start_temp = -1 (biến này có 2 mục đích dùng. Mục đích thứ nhất, là dùng để kiểm tra chuỗi con kết thúc tại vị trí i-1 có âm hay không. Vì nếu chuỗi con kết thúc tại i-1 âm thì chuỗi con kết lớn nhất kết thúc tại vị trí i sẽ là chính phần tử tại i. Mục đích thứ 2 là lưu tạm thời vị trí bắt đầu của mảng con cần tìm)

ending_index = 0 (dùng để gán giá tị kết thúc của mảng con cần tìm))

for i in (0, len(a)):

    max_ending_at <- max_ending_at + a[i]  (tính mảng con lớn nhất kết thúc tại vị trí đang xét)

    if (max_ending_at<0): (kiểm tra mảng con kết thúc tại i này có âm hay không)

        max_ending_at <- 0 (nếu là âm thì max_ending_at trở về 0)

        start_temp <- -1 (đồng thời start_temp trở về -1)

    else:

        if start_temp==-1: (tức là nếu chuỗi con lớn nhất tại i-1 nhỏ hơn 0)

            start_temp <- i (thì mảng con lớn nhất kết thúc tại i sẽ là a[i])

        if max_sum_present < max_ending_at: (kiếm tra tổng mảng con lớn nhất đang xét có lớn hơn giá trị cũ hay không)

            max_sum_present <- max_ending_at (nếu lớn hơn thì update giá trị mảng con lớn nhất)

            start_index <- start_temp (GÁN giá trị bắt đầu)

            ending_index <- i (UPDATE giá trị kết thúc))
            
    return start_index, ending_index, max_sum_present (trả về kết quả)
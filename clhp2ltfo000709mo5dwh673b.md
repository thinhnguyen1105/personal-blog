---
title: "[Day 1/100] Khám phá fibonacci và tam giác số nguyên"
datePublished: Mon May 15 2023 16:39:37 GMT+0000 (Coordinated Universal Time)
cuid: clhp2ltfo000709mo5dwh673b
slug: day-1100-kham-pha-fibonacci-va-tam-giac-so-nguyen
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/YfCVCPMNd38/upload/85749be97ee00d784fe1525baea5bc90.jpeg
tags: algorithms, python

---

Hôm nay là ngày đầu tiên nên có lẽ nên nhẹ nhàng một chút =)) để con đường này còn đi được dài và nhiều chông gai. Mình sẽ bắt tay code 2 thuật toán siêu đơn giản

### Bài 1: Vẽ tam giác số nguyên

Đề bài: Lập trình hàm nhận vào một số nguyên dương và in một tam giác như hình dưới, hàm này không trả về

* **Đầu vào là một số nguyên n**
    
* **Nếu số nguyên này không nằm trong khoảng \[1,9\]:**
    
    * **In ra n phải nằm trong khoảng \[1, 9\]**
        
* **Nếu điều kiện trên thỏa mãn, in ra một tam giác số, được tạo bởi các số từ 1 đến n, giữa các số có duy nhất một khoảng trắng**
    

---

Oke đọc đề bài xong thì sẽ phân tích 1 chút, mình nghĩ cái quan trọng nhất của một bài toán sẽ là **flow,** đại loại là mình phải tưởng tượng ra từng bước triển khai để có thể ra được kết quả cuối cùng.

Tưởng tượng chúng ta có **một đầu vào và một đầu ra.** Việc của chúng ta là xác định function ( hộp màu đen ) có cấu tạo như thế nào

![What is "black-box code" and why it's important - ThatSoftwareDude.com](https://www.thatsoftwaredude.com/images/post/166952a8-ac94-4d24-9b42-22f982096e4e.png align="center")

Áp dụng với bài toán trên ta có ( nghe giống toán cấp 3 ghê ):

Đầu vào: số nguyên n

Ràng buộc: **n phải nằm trong khoảng \[1, 9\]**

Đầu ra: tam giác số

```plaintext
1
2 2
3 3 3
4 4 4 4
5 5 5 5 5
```

Phần điều kiện ràng buộc thì dễ rồi, chỉ cần if else là có thể in ra những số hợp lệ

Với phần in ra tam giác, mình nhận thấy là các số này có sự lặp lại vậy ta nghĩ ngay đến vòng lặp.

```python
# đầu tiên xử lý điều kiện ràng buộc
if n >= 1 and n <= 9:
    # cần vẽ tam giác ở đây 
else: print("n phải nằm trong khoảng [1, 9]")
```

Để vẽ được tam giác thì nếu mình chỉ dùng 1 vòng lặp thì lúc in ra thì chỉ có 1,2,3,4...

mà như hình thì mình thấy mỗi dòng có các chữ số giống nhau nên chỉ cần 1 vòng lặp nữa là có thể in ra được như vậy. Kết luận lại là dùng 2 vòng lặp

```python
if n >= 1 and n <= 9:
        i = 1
        # vòng lặp đầu tiên tạo ra các dòng
        while i <= n:
            res = ''
            j = 1
            # vòng lặp thứ 2 tạo ra nột dung của 1 dòng 
            while j <= i:
                res = res + str(i) + ' '
                j += 1
            print(res)
            i += 1
    else:
        print("n phải nằm trong khoảng [1, 9]")
```

Oke vậy là mình đã in được ra tam giác số nguyên. Tiếp theo là đến fibonaci

---

### Bài 2: Hàm tính số fibonacci

Dãy số Fibonacci có đặc điểm sau:

* **Từ phần tử ở vị trí thứ n = 2 trở đi, giá trị của phần tử này bằng tổng giá trị 2 phần tử liền kề trước nó**
    
    * **Ví dụ 1: Phần tử ở vị trí n = 2 sẽ bằng tổng giá trị của 2 vị trí n = 1 và vị trí n = 0 tức là 1 = 1+0**
        
    * **Ví dụ 2: Phần tử ở vị trí n = 11 sẽ bằng tổng giá trị của 2 vị trí n = 10 và vị trí n = 9 tức là 89 = 55 + 34**
        

| **Vị trí (n)** | **0** | **1** | **2** | **3** | **4** | **5** | **6** | **7** | **8** | **9** | **10** | **11** |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| **Giá trị (x)** | **0** | **1** | **1** | **2** | **3** | **5** | **8** | **13** | **21** | **34** | **55** | **89** |

Lập trình hàm nhận vào một số nguyên **n** - vị trí trong dãy Fibonacci sao cho n ⩾ 0.

* **Nếu n &lt; 0:**
    
    * **In ra n phải lớn hơn hoặc bằng 0. Hàm trả về giá trị -1**
        
* **Nếu n ⩾ 0:**
    
    * **Hàm trả về giá trị thứ n trong dãy Fibonacci.**
        

---

Cũng như bài toán trước, mình sẽ xác định đầu vào, đầu ra và ràng buộc

```python
Đầu vào: số nguyên n
Ràng buộc: n >= 0
Đầu ra: Một số nguyên theo công thức fibonaci
```

Đầu tiên vẫn là xử lý điều kiện ràng buộc trước

```python
if(n < 0):
  print("n phải lớn hơn hoặc bằng 0")
else:
  # tính số theo fibonaci
```

Vì fibonaci chỉ áp dụng cho số thứ 2 trở đi nên mình sẽ chia thành 2 phần, số trước số 2 và số sau số 2

```python
if(n < 0):
  print("n phải lớn hơn hoặc bằng 0")
else:
  if n < 2:
    x = n
  else:
    # tính số theo fibonaci, giá trị của phần tử này bằng tổng giá trị 2 phần tử liền kề trước nó
```

Vì giá trị bằng tổng giá trị 2 phần tử liền kề trước nó nên mình sẽ đặt ra 3 biến `first`, `second` và `result`

```python
# vì fibonaci bắt đầu từ 2 nên 2 số đầu tiên sẽ là [0,1], tổng của 2 số này là 1 nên đặt first là 0, second là 1 và result = first + second = 1
first = 0
second = 1
result = 1

# lặp qua một mảng từ 2 đến n, ví dụ n = 5 thì mảng là [2,3,4] và gán các giá trị như này ta sẽ được kết quả fibonaci
for i in range(2, n):
   first = second
   second = result
   result = first + second
```

Vậy là mình đã có thể viết một hàm thuật toán cơ bản với fibonacci, ứng dụng của fibonacci có thể thấy trong đầu tư phân tích kỹ thuật =)) tạo điểm chốt lời , thoát lỗ

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684168511628/5c1c5519-a82b-4049-aff1-9c97e889bf11.png align="center")

Vậy là ngày đầu tiên mình đã ôn lại đc 2 thuật toán cơ bản 🤣🤣 dù không có gì khó nhưng mọi thứ căn bản sẽ là tiền đề cho nền tảng vững chắc sau này. Cheers 🥂
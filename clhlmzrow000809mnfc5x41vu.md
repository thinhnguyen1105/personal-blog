---
title: "Để không phải nghĩ commit với WhatTheCommit"
datePublished: Sat May 13 2023 06:59:15 GMT+0000 (Coordinated Universal Time)
cuid: clhlmzrow000809mnfc5x41vu
slug: de-khong-phai-nghi-commit-voi-whatthecommit
tags: git

---

Chắc ai từng dùng đến git cũng đã từng nghĩ trong đầu **“mình nên commit gì cho đoạn code này nhỉ ?”.** Và WhatTheCommit sinh ra với mục đích giải quyết câu hỏi đó, nó tạo ra những đoạn commit ngẫu nhiên, giúp cho lập trình viên tiết kiệm thời gian và không phải nghĩ về commit mesage. 😀

* Lưu ý: Mình chỉ khuyên nên dùng khi bạn muốn commit gì đó fun hoặc những commit không quan trọng nếu bạn không muốn người review code sẽ đấm vào mồm bạn vì ko biết bạn commit cho chức năng gì 😂
    

## Cài đặt và sử dụng

Chúng ta có thể dùng `curl` để lấy nội dung ngẫu nhiên từ trang web này về khi commit như sau:

```bash
git commit -m "$(curl -s whatthecommit.com/index.txt)"
```

Kết quả là cho ra những commit message để đời mà ai đọc vào cũng cười như

**“fixed shit that havent been fixed in last commit” :))**

Để tiết kiệm thời gian hơn nữa thì có thể tạo alias để thực hiện nhanh việc này trong .zshrc hoặc .bash\_profile trong thư mục root

```bash
// 1. mở .zshrc để edit
sudo nano ~/.zshrc

// 2. thêm dòng code này vào file 
alias yo='git add -A && git commit -m "$(curl -s whatthecommit.com/index.txt)"'

// 3. Ngoài ra tạo thêm một alias cho lệnh push như sau
alias push="git push"

// 4. lưu file lại và reset cấu hình bằng lệnh
source ~/.zshrc
```

Ok xong 😎 vậy là mỗi khi cần push code nhanh thì chỉ việc gõ lệnh `yo` theo sau đó là lệnh `push`. Kết quả sẽ được như sau. Chúc các bạn thành công 🥺
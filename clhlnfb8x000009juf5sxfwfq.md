---
title: "Code Bot Auto Trade trên Binance với Python"
datePublished: Sat May 13 2023 07:11:21 GMT+0000 (Coordinated Universal Time)
cuid: clhlnfb8x000009juf5sxfwfq
slug: code-bot-auto-trade-tren-binance-voi-python
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/iGYiBhdNTpE/upload/8b6ec48f84cad79c814a71ddc1378881.jpeg
tags: blockchain, tradingbot

---

Chắc hẳn mọi người không ít thì nhiều cũng đã từng nghe về tiền điện tử mang tên *Bitcoin*. Và cũng có nhiều người đã đu đỉnh ở nơi gọi là sàn **Binance – sàn giao dịch tiền điện tử lớn nhất thế giới**. Mình cũng là một người đã có 1 khoảng thời gian dài gắn bó với nó, cũng rút được kinh nghiệm qua các lệnh trade và dần dần có ý tưởng tạo ra con bot để trade thay mình. Trải qua quá trình làm và tìm hiểu, mình học được rất nhiều thứ, không chỉ về công nghệ mà còn rất nhiều kiến thức về đầu tư và quản lý vốn. Chuỗi series này mình sẽ chia sẻ cách làm ra một con Bot Trade trên sàn Binance kết hợp chia sẻ các khái niệm về trading và đầu tư tiền điện tử. Let’s go

Trước tiên để bắt đầu, mình sẽ nói về cách mà con bot này hoạt động. 😎

## 1\. How it works – Bot hoạt động thế nào ?

Khi bạn trading trên Binance – 1 sàn CEX hay còn gọi là sàn tập trung. Tức là bạn đang giao dịch trên một nơi đang được quản lý bởi một công ty hay một tổ chức và họ có thể thay đổi dữ liệu, mua và bán bitcoin hay những đồng coin khác dựa trên dữ liệu họ thu thập được, nhằm mục đích thu về lợi nhuận cho sàn. Nó giống như bạn xem trên những bộ phim Mỹ có các sòng bạc như Las Vegas, sẽ có một đội ngũ đằng sau chi phối việc hoạt động của sòng bạc và đội ngũ này có nhiệm vụ là đảm bảo phần lớn người chơi sẽ thua. Với Binance đội ngũ này được gọi với một cái tên mỹ miều mà nghe đã thấy sợ MM – hay còn gọi là Market Maker (đội làm giá)

Vậy làm thế nào để trading kiếm được tiền ? Một câu hỏi rất hay và chắc hẳn ai trading cũng sẽ nghĩ đến =)). Phần lớn traders hiện nay sử dụng cho mình các **chỉ báo kỹ thuật** – những công cụ phân tích đường giá, hay phân tích kinh tế vi mô, vĩ mô. Với trải nghiệm của mình, tất cả những chỉ báo đó chỉ mang tính tương đối và việc giá chạy như nào không thể dự đoán trước được. Việc giá chạy theo các vùng cung cầu, giá chạy theo pattern có thể tăng xác suất thắng nhưng cũng không thể chính xác 100%. Để việc trading có lợi nhuận bạn cần đảm bảo được yếu tố xác suất thắng lớn hơn 50% và số tiền lỗ phải ít hơn số tiền lãi

Về cơ bản, trading là mua tài sản khi ở giá thấp và bán khi ở giá cao, phần chênh lệch chính là lợi nhuận của bạn. Cách đây vài năm, Binance đã cho ra mắt 1 tính năng là Binance Futures, với tính năng này bạn có thể mua một vị thế long khi bạn kỳ vọng giá lên cao, và short khi kì vọng giá đi xuống. Ở trường hợp nào, nếu giá chạy theo kì vọng thì bạn đều có lãi. Như mình đã nói ở trên, đội MM có nhiệm vụ thanh lý các vị thế long hoặc short khi quá lệch về một bên. Vì nếu không thanh lý, thì sàn sẽ lỗ và đội làm giá sẽ bị trách mắng vì làm giảm doanh thu của công ty. Ý tưởng của mình là sử dụng dữ liệu liquidation để có thể đi theo hướng của đội MM, như vậy tỷ lệ chiến thắng sẽ cao hơn.

Ở đây, mình sẽ không sử dụng chỉ báo kỹ thuật hay bất kì mô hình nào. Mình sẽ sử dụng dữ liệu liquidation – số tiền thanh khoản tại một thời điểm giá

( Ví dụ: tại 3:00AM có 150k$ lệnh long được mở tại giá 23000$ với cặp BTCUSDT ). Tại thời điểm này, hoặc sau đó khả năng giá sẽ có xu hướng giảm vì nếu giá tiếp tục tăng hoặc tăng mạnh thì sàn sẽ lỗ.

Dựa trên yếu tố đó, trước mắt mình sẽ chứng minh bằng cách gắn những điểm có thanh khoản cao vào đồ thị bitcoin và cùng xem xác suất nếu mình sử dụng dữ liệu này là bao nhiêu nhé 🤣

(2 tháng sau) …

Mình đã cố gắng triển khai một application hình thành từ 3 phần chính

1. Front-End: Sử dụng VueChartJS để hiển thị đồ thị giá bitcoin và các điểm liquidation
    
2. Python Bot Binance để lấy dữ liệu giá bitcoin, đồng thời với thư viện này có thể đặt các lệnh order theo điều kiện
    
3. Server Nodejs + MongoDB để lưu lại dữ liệu liquidation
    

Sau khi hoàn thiện và đánh giá độ khả thi thì mình quyết định dừng project này tại đây vì khi quan sát dữ liệu liquidation mình không tìm thấy được quy luật. Tuy vậy sau khi làm xong đc application này thì mình cũng học được rất nhiều thứ. Mình sẽ chia sẻ chi tiết hơn cho các bạn trong các bài tiếp theo.

Đây là trang demo dữ liệu liquidation long và short từ [https://t.me/BinanceLiquidations](https://t.me/BinanceLiquidations) , mình đã kết hợp với đường giá bitcoin chạy trong khung 5m. Tuy không kiếm được tiền nhưng đây là một trải nghiệm mang lại nhiều kiến thức và sự thú vị 🤩🤩🤩

[https://chart.nickyicet.com/](https://chart.nickyicet.com/)
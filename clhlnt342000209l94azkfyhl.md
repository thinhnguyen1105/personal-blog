---
title: "Tối ưu hoá hệ thống VueJS (Phần 1)"
datePublished: Sat May 13 2023 07:22:03 GMT+0000 (Coordinated Universal Time)
cuid: clhlnt342000209l94azkfyhl
slug: toi-uu-hoa-he-thong-vuejs-phan-1
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/HUJDz6CJEaM/upload/d0d2227b3d67e1b3d2a311f4b2123961.jpeg
tags: javascript, web-development, vuejs

---

Sau một thời gian làm việc với hệ thống web, đặc biệt là 2 năm qua với VueJs mình nhận thấy để có thể chạy được 1 PWA ( Progressive web app ) tốt thì cần một cái template project 🧑‍💻 thật chuẩn trước khi bắt tay vào xây dựng dự án. Ý mình **template** ở đây là một bộ **source code** chứa tất cả những practice tối ưu giúp cho **dev code nhanh hơn**, hệ thống chạy **ổn định hơn, nhẹ hơn** và sử dụng được hết những điểm mạnh của framework mình đang dùng ( có đồ trong tay phải biết dùng đúng k các bác =)) ). Sẽ có một số bạn bảo rằng *template tối ưu thì có đầy trên mạng, sao không lên đấy lấy mà dùng cho nhanh.* Đúng và sai, template trên mạng có rất nhiều, nhưng nếu không hiểu cách người ta setup hệ thống như nào thì đến lúc hệ thống chạy chậm hay xảy ra vấn đề thì bó tay 😧. Không biết fix kiểu gì và khi đó hệ thống đã quá to rồi, nhận ra phải đập đi làm lại thì quả là một vấn đề lớn. Vậy nên hôm nay mình sẽ chia sẻ vài tips để xây dựng hệ thống có thể grow up một cách dễ dàng với VueJS nhé 😙😙😙

Sau đây mình sẽ hướng dẫn cách để làm ra một template của chính bạn và hiểu sâu đến từng dòng code trong project đó nhé. Vậy nên nếu có máy tính thì mở ra thực hành ngay thuii 😆😆😆

## Bước 1: Clone project VueJS

Đúng vậy, dùng framework thì phải lấy từ chỗ nhà sản xuất cung cấp. Trong ví dụ này mình sẽ dùng Vue2 để làm template nhé

Đầu tiên các bạn sẽ cài vue bằng cách gõ lệnh

<table><tbody><tr><td colspan="1" rowspan="1"><p><code>npm install vue &amp;&amp; vue init</code></p></td></tr></tbody></table>

Các bạn cứ cài theo hướng dẫn của vue, sau khi cài xong sẽ được một project khá thô sơ, và nhiệm vụ của mình bây giờ là đắp da đắp thịt cho nó để trở thành một người có ích cho xã hội 😄

## Bước 2: Tối ưu cách gọi API bằng factory design pattern

Vâng đúng vậy, một project chạy bằng Vue ở phía client sẽ phải gọi API đến server để có thể thêm, sửa, xoá và lấy dữ liệu. Để client gọi được request một cách tối ưu nhất thì ta cần đến một cái gọi là factory design pattern. Nôm na là một cái nhà máy chuyên sản xuất ra các request API, mà đã là nhà máy thì tất nhiên là phải nhanh hơn và tự động hơn rồi

Để tạo ra được trái tim của nhà máy thì mình sẽ tạo ra một file theo đường dẫn như sau src/api/core/index.js. File này có mục đích là tạo ra tất cả các request theo chuẩn Restful API. Từ đó có thể tái sử dụng được API ở mỗi đối tượng mà mình cần gọi dữ liệu.

```javascript
count: (params, option) =>
        axios.get(
            BASE_URL + '-count',
            {
                params: {...params},
            },
            option
        ),
    fetch: (params, option) =>
        axios.get(
            BASE_URL,
            {
                params: {...params},
            },
            option
        ),
    fetchOne: (id, option) =>
        axios.get(
            BASE_URL + '/' + id,
            option
        ),
    create: (params, options) =>
        axios.post(
            BASE_URL,
            {...params},
            options
        ),
    createMany: (params, options) =>
        axios.post(
            BASE_URL + '/create-many',
            {...params},
            options
        ),
    update: (id, params, option) =>
        axios.put(
            BASE_URL + `/${id}`,
            params,
            option
        ),
    delete: (id, option) =>
        axios.delete(
            BASE_URL + `/${id}`,
            option
        )
```

Để dùng được core thì mình sẽ tạo ra 1 repository để sử dụng core trong đó

src/api/repository/vendorRepository. Sau khi tạo xong vendorRepository thì mình chỉ cần gọi ra core và thay vào url và params tương ứng và từ nay về sau, mỗi khi mình cần gọi fetch mình chỉ cần gọi ra CoreRepository là nó sẽ xử lý hết cho mình, nhanh phải k nào hehe 😎

```javascript
const fetch = params => {
    return CoreRepository(baseURL).fetch(params)
}
```

## Bước 3: Tự động tạo store khi thêm file

Nếu như bạn nào đã từng code vue r thì chắc hẳn sẽ biết đến vuex, một thư viện quản lý state tương tự redux ở react. Sẽ thật phiền nếu như mỗi khi chúng ta thêm một đối tượng mới mà lại phải đi khai báo lại store, vì vậy mình có sử dụng 1 trick để có thể tự động khai báo store cho vuex nếu một file mới được thêm vào bằng cách như sau

Tạo 1 file như sau /src/store/modules/index.js

```javascript
const requireModule = require.context('.', false, /\.js$/)
const modules = {}
 
requireModule.keys().forEach(fileName => {
  if (fileName === './index.js') return
  const moduleName = fileName.replace(/(\.\/|\.js)/g, '')
  modules[moduleName] = requireModule(fileName).default
})
export default modules
```

Nhìn vào code trên thì ta thấy file này sẽ chạy một vòng lặp qua tất cả các file js đang ở thư mục modules. Nếu fileName là index.js thì bỏ qua còn lại thì sẽ truyền hết vào biến modules để vuex tạo ra store. Đơn giản nhưng hiệu quả phải không nào =)) , từ bây giờ chỉ cần thêm file vào project mà không cần quan tâm khai báo store nữa luôn, cứ thế mà dùng hehe 🐥

## Bước 4: Tạo global components trong Vue gọi ở khắp mọi nơi

Chắc hẳn bạn đã từng gặp trường hợp muốn dùng một component nào đó như cái nút thì phải gọi ra component mình đã code trước đấy là hoặc nếu bạn custom thêm thì phải gọi ra và cứ mỗi lần gọi bạn sẽ phải import components đấy, khai báo components rồi với được sử dụng. Nhưng với kiểu import dưới dây, bạn đơn giản chỉ cần gọi thẻ trong vue mà không cần phải import thêm bất cứ dòng code nào

Cách làm:

tạo một file /src/global/index.js

```javascript
import Vue from 'vue'
const requireComponent = require.context('.', false, /[\w-]+\.vue$/)
 
const global = {
  import() {
    requireComponent.keys().forEach(fileName => {
      const componentConfig = requireComponent(fileName)
      const componentName = fileName.replace(/^\.\//, '').replace(/\.\w+$/, '')
      Vue.component(componentName, componentConfig.default || componentConfig)
    })
  }
}
 
export default global
```

File này có nhiệm vụ đọc hết tất cả các file trong folder global, và **tự động import vào vue component**, từ đó bạn có thể sử dụng ở bất kì nơi nào trong project mà không cần phải import. Lại tiện thêm một phát nữa

(…. còn tiếp)
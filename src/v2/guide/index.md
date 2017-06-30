---
title: Giới thiệu
type: guide
order: 2
---

## What is Vue.js?

Vue (phát âm /vjuː/, giống như **view**) là một **progressive framework** để xây dựng giao diện người dùng. Không giống như các frameworks khác, Vue được thiết kế từ đầu và được nâng cấp dần dần. Thư viện lõi chỉ tập trung vào tầng View, và rất dễ để tiếp cận hay tích hợp với các thư viện hoặc dự án hiện hiện tại. Mặt khác, Vue hoàn toàn có thể cung cấp sức mạnh cho các ứng dụng Single-Page khi được kết hợp với [modern tooling](single-file-components.html) and [supporting libraries](https://github.com/vuejs/awesome-vue#components--libraries).

Nếu bạn là một lập trình viên Front-end giàu kinh nghiệm và muốn biết hiệu năng của Vue so với các thư viện/framework khác, hãy xem tại [So sánh với các Framework khác](comparison.html).

## Bắt đầu

<p class="tip">Hướng dẫn này yêu cầu bạn đã nắm bắt cơ bản về HTML, CSS và Javascript. Nếu bạn là một lập trình viên frontend mới, Hãy bắt đầu với những điều cơ bản trước và sau đó quay lại hướng dẫn này. Có kinh nghiệm với các framework là một ưu điểm, nhưng không bắt buộc.</p>

Một cách dễ dàng để thử Vue.js là sử dụng [JSFiddle Hello World example](https://jsfiddle.net/chrisvfritz/50wL7mdz/). Hãy thoải mái mở nó trong một tab khác và thực hành theo khi chúng tôi làm một số ví dụ cơ bản. Hoặc bạn có thể <a href="https://gist.githubusercontent.com/chrisvfritz/7f8d7d63000b48493c336e48b3db3e52/raw/ed60c4e5d5c6fec48b0921edaed0cb60be30e87c/index.html" target="_blank" download="index.html">tạo một trang <code>index.html</code></a> và tích hợp Vue bằng lệnh:

``` html
<script src="https://unpkg.com/vue"></script>
```

Trang [Cài đặt](installation.html) cung cấp thêm các tùy chọn khác để cài đặt Vue. Chú ý rằng chúng tôi **không** khuyến cáo các beginners bắt đầu với `vue-cli`, đặc biệt khi các bạn chưa quen thuộc với các công cụ xây dựng trên nền Node.js.

## Khai báo ban đầu

Phần core của Vue.js là một hệ thống cho phép dễ dàng khai báo hiển thị dữ liệu cho DOM bằng cú pháp đơn giản như sau:

``` html
<div id="app">
  {{ message }}
</div>
```
``` js
var app = new Vue({
  el: '#app',
  data: {
    message: 'Xin chào Vue!'
  }
})
```
{% raw %}
<div id="app" class="demo">
  {{ message }}
</div>
<script>
var app = new Vue({
  el: '#app',
  data: {
    message: 'Xin chào Vue!'
  }
})
</script>
{% endraw %}

Chúng ta vừa hoàn thành xong ứng dụng Vue đầu tiên của mình! Điều này trông giống như hiển thị một string, nhưng thật ra Vue đã làm rất nhiều việc ở phía sau. Hiện tại, dữ liệu và DOM đã được liên kết, và mọi thứ nay đã **reactive**. Làm thế nào chúng ta biết được? Hãy mở trình điều khiển Javascript của trình duyệt (JavaScript console F12 | Ctrl+Shift+I) và gán `app.message` một giá trị khác. Bạn sẽ thấy giá trị trong ví dụ ở trên sẽ được cập nhật theo.

Ngoài việc nội suy văn bản, chúng ta có thể gắn thuộc tính của phần tử như sau:

``` html
<div id="app-2">
  <span v-bind:title="message">
    Di chuột qua tôi một vài giây
    để thấy tiêu đề ràng buộc!
  </span>
</div>
```
``` js
var app2 = new Vue({
  el: '#app-2',
  data: {
    message: 'Bạn đã tải trang này lúc ' + new Date()
  }
})
```
{% raw %}
<div id="app-2" class="demo">
  <span v-bind:title="message">
    Di chuột qua tôi một vài giây để thấy tiêu đề ràng buộc!
  </span>
</div>
<script>
var app2 = new Vue({
  el: '#app-2',
  data: {
    message: 'You loaded this page on ' + new Date()
  }
})
</script>
{% endraw %}

Ở đây chúng ta gặp một điểm mới. Thuộc tính `v-bind` bạn đang thấy được gọi là một **chỉ thị**. Các chỉ thị có tiền tố là `v-` để chỉ ra rằng chúng là các thuộc tính đặc biệt của Vue, và bạn có thể đoán rằng, chúng áp dụng cho các hành vi để hiển thị DOM. Ở đây, nó có thể được hiểu là "giữ thuộc tính `title` của phần tử này được cập nhật với thuộc tính `message` được khai báo trong Vue."

Nếu bạn mở lại trình quản lý Javascript và gõ `app2.message = 'some new message'`, Bạn sẽ thấy một lần nữa sự ràng buộc HTML - trong trường hợp này là thuộc tính `title` đã được cập nhật.

## Điều kiện and Vòng lặp

Thật đơn giản để bật/tắt sự hiển thị của một phần tử:

``` html
<div id="app-3">
  <p v-if="seen">Bây giờ, Bạn thấy tôi.</p>
</div>
```

``` js
var app3 = new Vue({
  el: '#app-3',
  data: {
    seen: true
  }
})
```

{% raw %}
<div id="app-3" class="demo">
  <span v-if="seen">Bây giờ, Bạn thấy tôi.</span>
</div>
<script>
var app3 = new Vue({
  el: '#app-3',
  data: {
    seen: true
  }
})
</script>
{% endraw %}

Mở trình quản lý Javascript và gõ `app3.seen = false`. Bạn sẽ thấy dòng tin biến mất.

Ví dụ này chứng minh rằng chúng ta có thể liên kết dữ liệu không chỉ với văn bản và thuộc tính, mà còn đối với **cấu trúc** của DOM. Thêm nữa, Vue cũng cung cấp một hệ thống chuyển đổi mạnh mẽ để có thể tự động áp dụng các [hiệu ứng chuyển tiếp](transitions.html) giữa các phần tử khi được chèn/sửa/xóa bởi Vue.

Có một số chỉ thị khác, mỗi loại sở hữu các chức năng riêng biệt. Ví dụ, Chỉ thị `v-for` có thể sử dụng để hiển thị một danh sách của các phần tử của một Mảng:

``` html
<div id="app-4">
  <ol>
    <li v-for="todo in todos">
      {{ todo.text }}
    </li>
  </ol>
</div>
```
``` js
var app4 = new Vue({
  el: '#app-4',
  data: {
    todos: [
      { text: 'Học JavaScript' },
      { text: 'Học Vue' },
      { text: 'Xây dựng một ứng dụng tuyệt vời' }
    ]
  }
})
```
{% raw %}
<div id="app-4" class="demo">
  <ol>
    <li v-for="todo in todos">
      {{ todo.text }}
    </li>
  </ol>
</div>
<script>
var app4 = new Vue({
  el: '#app-4',
  data: {
    todos: [
      { text: 'Học JavaScript' },
      { text: 'Học Vue' },
      { text: 'Xây dựng một ứng dụng tuyệt vời' }
    ]
  }
})
</script>
{% endraw %}

Mở console và gõ `app4.todos.push({ text: 'New item' })`. Bạn sẽ thấy phần tử mới xuất hiện trong danh sách.

## Xử lý User Input

Để người dùng tương tác với ứng dụng của bạn, Bạn có thể dùng chỉ thị `v-on` để gắn trình xử lý sự kiện gọi các phương thức được cung cấp trong Vue của chúng ta:

``` html
<div id="app-5">
  <p>{{ message }}</p>
  <button v-on:click="reverseMessage">Đảo ngược nội dung</button>
</div>
```
``` js
var app5 = new Vue({
  el: '#app-5',
  data: {
    message: 'Xin chào Vue.js!'
  },
  methods: {
    reverseMessage: function () {
      this.message = this.message.split('').reverse().join('')
    }
  }
})
```
{% raw %}
<div id="app-5" class="demo">
  <p>{{ message }}</p>
  <button v-on:click="reverseMessage">Đảo ngược nội dung</button>
</div>
<script>
var app5 = new Vue({
  el: '#app-5',
  data: {
    message: 'Hello Vue.js!'
  },
  methods: {
    reverseMessage: function () {
      this.message = this.message.split('').reverse().join('')
    }
  }
})
</script>
{% endraw %}

Note in the method we simply update the state of our app without touching the DOM - all DOM manipulations are handled by Vue, and the code you write is focused on the underlying logic.

Vue also provides the `v-model` directive that makes two-way binding between form input and app state a breeze:

``` html
<div id="app-6">
  <p>{{ message }}</p>
  <input v-model="message">
</div>
```
``` js
var app6 = new Vue({
  el: '#app-6',
  data: {
    message: 'Hello Vue!'
  }
})
```
{% raw %}
<div id="app-6" class="demo">
  <p>{{ message }}</p>
  <input v-model="message">
</div>
<script>
var app6 = new Vue({
  el: '#app-6',
  data: {
    message: 'Hello Vue!'
  }
})
</script>
{% endraw %}

## Composing with Components

Hệ thống Components là một khái niệm quan trọng trong Vue, bởi vì nó là một trừu tượng cho phép chúng ta xây dựng các ứng dụng quy mô lớn bao gồm các ứng dụng nhỏ, self-contained, và thường được tái sử dụng. Để hiểu rõ hơn thì gần như bất kì loại giao diện ứng dụng có thể được trừu tượng thành một cây phân nhánh các components:

![Component Tree](/images/components.png)

Trong Vue, một component là một thành phần tùy chọn của Vue instance được định nghĩa trước. Đăng ký một component trong Vue rất đơn giản:

``` js
// Define a new component called todo-item
Vue.component('todo-item', {
  template: '<li>This is a todo</li>'
})
```

Bây giờ, bạn hoàn toàn có thể sử dụng nó trong một component khác:

``` html
<ol>
  <!-- Create an instance of the todo-item component -->
  <todo-item></todo-item>
</ol>
```

Nhưng điều này sẽ làm cho một văn bản hiển thị trong mọi todo, điều đó thật không hay tí nào. Chúng ta có thể truyền dữ liệu từ component cha sang các component con. Hãy sửa đổi một chút để component nhận một [prop](components.html#Props):

``` js
Vue.component('todo-item', {
  // The todo-item component now accepts a
  // "prop", which is like a custom attribute.
  // This prop is called todo.
  props: ['todo'],
  template: '<li>{{ todo.text }}</li>'
})
```

Bây giờ, chúng ta có thể đưa todo vào mỗi component lặp lại bằng cách sử dụng `v-bind`:

``` html
<div id="app-7">
  <ol>
    <!--
      Now we provide each todo-item with the todo object
      it's representing, so that its content can be dynamic.
      We also need to provide each component with a "key",
      which will be explained later.
    -->
    <todo-item
      v-for="item in groceryList"
      v-bind:todo="item"
      v-bind:key="item.id">
    </todo-item>
  </ol>
</div>
```
``` js
Vue.component('todo-item', {
  props: ['todo'],
  template: '<li>{{ todo.text }}</li>'
})

var app7 = new Vue({
  el: '#app-7',
  data: {
    groceryList: [
      { id: 0, text: 'Vegetables' },
      { id: 1, text: 'Cheese' },
      { id: 2, text: 'Whatever else humans are supposed to eat' }
    ]
  }
})
```
{% raw %}
<div id="app-7" class="demo">
  <ol>
    <todo-item v-for="item in groceryList" v-bind:todo="item" :key="item.id"></todo-item>
  </ol>
</div>
<script>
Vue.component('todo-item', {
  props: ['todo'],
  template: '<li>{{ todo.text }}</li>'
})
var app7 = new Vue({
  el: '#app-7',
  data: {
    groceryList: [
      { id: 0, text: 'Vegetables' },
      { id: 1, text: 'Cheese' },
      { id: 2, text: 'Whatever else humans are supposed to eat' }
    ]
  }
})
</script>
{% endraw %}

Đây chỉ là một ví dụ mẫu, nhưng chúng ta đã quản lý để tách ứng dụng thành hai phần nhỏ hơn. Và component con sẽ được phân tách hợp lý từ cha mẹ thông qua props. Bây giờ chúng ta có thể cải tiến hơn nữa component`<todo-item>` với mẫu phức tạp và logic hơn mà không ảnh hưởng đến ứng dụng cha.

Trong một ứng dụng lớn, Nó là điều cẩn thiết để chia ứng dụng thành nhiều components, điều đó giúp việc phát triển dễ quản lý hơn. Chúng ta sẽ nói nhiều hơn về [component sau](components.html), but here's an (imaginary) example of what an app's template might look like with components:

``` html
<div id="app">
  <app-nav></app-nav>
  <app-view>
    <app-sidebar></app-sidebar>
    <app-content></app-content>
  </app-view>
</div>
```

### Liên quan đến việc tùy chỉnh các phần tử

Bạn có thể thấy rằng Vue Components rất giống như **Custom Elements**, chúng là một phần của [Web Components Spec](http://www.w3.org/wiki/WebComponents/). Đó là bởi vì Vue Component được mô phỏng theo nó. Ví dụ, Vue components bổ sung [Slot API](https://github.com/w3c/webcomponents/blob/gh-pages/proposals/Slots-Proposal.md) và thuộc tính `is`. Tuy nhiên, vẫn có một số điểm khác biệt:

1. The Web Components Spec vẫn đang trong giai đoạn soạn thảo, và chưa được triển khai trong mọi trình duyệt. Để so sánh, Vue component không yêu cầu bất kì polyfills và làm việc nhất quán trong tất cả các trình duyệt hỗ trợ(IE9 trở lên). Khi cần, Vue component có thể được gói bên trong một phần tử tùy chỉnh gốc.

2. Vue component cung cấp những tính năng quan trọng không có trong custom elements, đặc biệt là các luồng cross-component, tùy chỉnh sự kiện giao tiếp và tích hợp công cụ xây dựng.

## Sẵn sàng để tiếp tục?

Chúc tôi vừa giới thiệu ngắn gọn các tính năng cơ bản nhất của lõi Vue.js - Phần còn lại của hướng dẫn này sẽ giới thiệu các tính năng nâng cao khác với nhiều chi tiết hơn, do đó hãy chắc chắn bạn đã đọc qua tất cả.
## **Biên dịch Ahead-of-Time (AOT)**

![image](https://github.com/user-attachments/assets/86f7daeb-bb3d-42e4-8ba7-cfbf78889b85)

**Tại sao chúng ta lại cần AOT**

**Ahead-of-Time (AOT)** là một kỹ thuật biên dịch trong Angular, trong đó mã nguồn TypeScript bao gồm `Angular template` của bạn được biên dịch sang JavaScript ngay sau khi bạn chạy lệnh `run build`, và rồi bạn đẩy cái file dist này lên host (server) khi browser lấy `source code` của bạn từ server thì nó đã là JavaScript ko cần biên dịch lại sẽ giúp tăng hiệu quả performace lên.

Nếu không sử dụng `AOT` thì trong dự án angular chúng ta sẽ sử dụng **Just-in-Time (JIT)** và khi bạn run build nó sẽ ko biên dịch ra `JavaScript` mà là một đống hỗn hợp (bao gồm  `Angular template` như ` {{ variable }} hoặc *ngFor`) cho nên khi `browser` lấy `source code` về nó sẽ phải `Angular parse & compliles template` để biên dịch sang `JS` điều này làm giảm `performace`.


## **Angular Element**

**Angular Element** là cho phép bạn tạo ra các **custom elements** (thẻ HTML tự do) từ các component Angular. Các Angular Element này có thể được sử dụng giống như các thẻ HTML thông thường trong bất kỳ ứng dụng web nào, bao gồm cả các ứng dụng không phải Angular.

**1. Với file Html nằm trong Angular project**

<img width="693" alt="image" src="https://github.com/user-attachments/assets/67919d74-2a9f-4fad-afed-48f5a199a1e4" />

**2. Với file Html không nằm trong Angular project thì phải làm sao**

Build Angular project (dist) từ 1 file html sử dụng javascrript để trỏ vào file js trong dist.

<img width="693" alt="image" src="https://github.com/user-attachments/assets/3c15ebbe-66c9-4b14-a3d3-0fc890de0101" />


**3. Các đặc điểm chính của Angular Elements:**

1. **Custom Elements**: Angular Elements là một cách để tạo các custom elements (thẻ HTML tùy chỉnh). Custom elements là một phần của Web Components API, và Angular giúp bạn dễ dàng tạo ra chúng từ các component Angular.
  
2. **Web Components**: Các Angular Element tuân thủ các tiêu chuẩn của web components như Shadow DOM, Custom Elements, và HTML Templates. Điều này giúp bạn có thể sử dụng các Angular component mà không phụ thuộc vào Angular CLI hay Angular framework.

3. **Reusability**: Bạn có thể sử dụng các Angular Element ở bất kỳ nơi nào, bao gồm các ứng dụng không phải Angular. Đây là một cách tuyệt vời để tái sử dụng các thành phần của Angular trong các hệ sinh thái khác.


## **Directive**

**Directive** là một công cụ cho phép bạn thêm Add, update, delete trên DOM (Document Object Model) trong ứng dụng.


### **1. Structural Directives**  
- Thay đổi cấu trúc của DOM bằng cách thêm, xóa hoặc sửa đổi các phần tử HTML.
- Các directive này thường dùng dấu `*` ở phía trước tên directive.

**Ví dụ:** `*ngIf`, `*ngFor`, `*ngSwitch`
```html
<div *ngIf="isVisible">
  This is visible only if isVisible is true.
</div>

<ul>
  <li *ngFor="let item of items">{{ item }}</li>
</ul>
```

### **2. Attribute Directives**  
- Thay đổi hoặc thao tác với các thuộc tính (attributes) của phần tử HTML mà không thay đổi cấu trúc DOM.

**Ví dụ:** `ngClass`, `ngStyle`, directive tùy chỉnh
```html
<div [ngClass]="{ 'highlight': isActive }">
  This div will have 'highlight' class if isActive is true.
</div>

<div [ngStyle]="{ 'color': textColor }">
  This text will have dynamic color.
</div>
```
### **3. Custom Directives**  
- Bạn có thể tạo directive tùy chỉnh để thêm hành vi cho các phần tử HTML.

**Ví dụ tạo một Attribute Directive tùy chỉnh**
```typescript
import { Directive, ElementRef, Renderer2, HostListener } from '@angular/core';

@Directive({
  selector: '[appHighlight]'
})
export class HighlightDirective {
  constructor(private el: ElementRef, private renderer: Renderer2) {}

  @HostListener('mouseenter') onMouseEnter() {
    this.renderer.setStyle(this.el.nativeElement, 'backgroundColor', 'yellow');
  }

  @HostListener('mouseleave') onMouseLeave() {
    this.renderer.removeStyle(this.el.nativeElement, 'backgroundColor');
  }
}
```

Sử dụng directive này trong HTML:
```html
<p appHighlight>This text will be highlighted on hover.</p>
```

## **Binding**

**Binding** trong Angular là một cơ chế cho phép bạn liên kết dữ liệu giữa **component** và **view** (giao diện người dùng).

### **1. Interpolation (Interpolation Binding)**

**Định nghĩa:**  
Interpolation là cách đơn giản nhất để hiển thị giá trị dữ liệu từ component vào trong HTML. Nó sử dụng dấu ngoặc kép `{{ }}`.

**Cách sử dụng:**
```html
<p>{{ message }}</p>
```
**Component:**
```typescript
export class AppComponent {
  message: string = 'Hello, Angular!';
}
```
### **2. Property Binding**

**Định nghĩa:**  
Property binding giúp bạn liên kết dữ liệu từ component với thuộc tính của một phần tử HTML, ví dụ như thuộc tính `src`, `disabled`, `class`, v.v.

**Cách sử dụng:**
```html
<img [src]="imageUrl" alt="Image">
<button [disabled]="isDisabled">Click Me</button>
```
**Component:**
```typescript
export class AppComponent {
  imageUrl: string = 'https://example.com/image.jpg';
  isDisabled: boolean = false;
}
```

### **3. Event Binding**

**Định nghĩa:**  
Event binding cho phép bạn lắng nghe các sự kiện như `click`, `keyup`, v.v., và xử lý chúng trong component khi người dùng tương tác với giao diện.

**Cách sử dụng:**
```html
<button (click)="onClick()">Click Me</button>
```
**Component:**
```typescript
export class AppComponent {
  onClick() {
    console.log('Button clicked!');
  }
}
```


### **4. Two-way Data Binding (NgModel)**

**Định nghĩa:**  
Two-way data binding là một cơ chế cho phép đồng bộ hóa dữ liệu giữa component và view, nghĩa là thay đổi trong component sẽ cập nhật giao diện và ngược lại. Angular sử dụng `[(ngModel)]` để thực hiện two-way data binding.

**Cách sử dụng:**
```html
<input [(ngModel)]="username" placeholder="Enter your name">
<p>Your name is: {{ username }}</p>
```
**Component:**
```typescript
export class AppComponent {
  username: string = '';
}
```


| **Kiểu Binding**        | **Cách sử dụng**                      | **Giải thích**                                  |
|-------------------------|---------------------------------------|-------------------------------------------------|
| **Interpolation**        | `{{ expression }}`                    | Hiển thị giá trị dữ liệu trong HTML.            |
| **Property Binding**     | `[property]="expression"`            | Liên kết dữ liệu với thuộc tính của phần tử HTML.|
| **Event Binding**        | `(event)="expression"`                | Liên kết sự kiện từ HTML đến component.         |
| **Two-way Data Binding** | `[(ngModel)]="expression"`            | Đồng bộ hóa dữ liệu giữa component và view.     |


## **Bootstrapping**

**Angular Bootstrapping** là quá trình khởi tạo một ứng dụng angular. Angular cần biết module gốc và component chính để bắt đầu tạo UI.

**Sử dụng hàm `platformBrowserDynamic().bootstrapModule`**: Trong tập tin `main.ts`, Angular gọi hàm `platformBrowserDynamic().bootstrapModule(AppModule)` để khởi động ứng dụng bằng cách nạp `AppModule`.

**Chi tiết về các mảng trong @NgModule**
1. **declarations**:
   - Đây là nơi khai báo các component, directive, pipe trong module.
   - Mỗi component, directive, pipe phải được khai báo trong đúng một NgModule.
   - Các thành phần này chỉ có thể được sử dụng trong module nơi chúng được khai báo hoặc trong các module khác khi được **import**.

2. **imports**:
   - Làm rõ những NgModules mà module này cần để hoạt động.
   - Ví dụ: **BrowserModule**, **FormsModule**, **HttpClientModule** sẽ được khai báo ở đây nếu cần sử dụng trong ứng dụng.

3. **providers**:
   - Là nơi khai báo các dịch vụ (services) mà ứng dụng cần.
   - Dịch vụ này sẽ có phạm vi toàn ứng dụng (app-wide).

4. **bootstrap**:
   - Đây là nơi xác định các component được tạo và chèn vào **DOM** khi ứng dụng khởi động.
   - Thông thường, **AppComponent** sẽ được khai báo trong mảng **bootstrap**.


## **View**

### **1. Angular view là gì?**

<img width="425" alt="image" src="https://github.com/user-attachments/assets/d964a46c-d6f5-435e-ad5d-50346865b35d" />

`Angular View` là một lớp trừu tượng bên trên `DOM`, giúp quản lý giao diện người dùng bằng cách liên kết dữ liệu với template thông qua data binding và `change detection`. Angular không thao tác trực tiếp trên DOM mà thao tác trên `View` trước, sau đó mới cập nhật `DOM` tương ứng.

Có một số trường hợp bạn có thể thao tác trực tiếp với `DOM` vd: sử dụng `ElementRef`

### **2. Cơ chế hoạt động:**
Khi dữ liệu thay đổi,` Angular` sẽ chạy cơ chế `change detection`, phát hiện sự thay đổi và cập nhật `view` tương ứng, sau đó mới thao tác lên `DOM`. Điều này giúp tối ưu hiệu suất và giảm thiểu thao tác trực tiếp trên `DOM`.

### **3. View State**

Mỗi `View` có một số trạng thái đóng vai trò giúp `Angular` quyết định có chạy `Change Detection` cho `View` hay tất cả `View child component` của nó hoặc bỏ qua.

**Một số trạng thái quan trọng**
1. First Check
2. Check Enable
3. Errored
4. Destroyed 

Nếu `Check Enable` là `false` hoặc `View` ở trạng thái `Errored, Destroyed` thì sẽ bỏ qua `Change Detection`, mặc định  `Check Enable` là `true` trừ khi dùng `Onpush`.

Angular có nhiều khái niệm `high-level` để thao tác với view như `ViewContainerRef, TemplateRef, ViewChild, ElementRef, ViewRef`

`ViewRef` là một lớp trừu tượng đại diện cho một View được liên kết với một Change Detector. cụ thể bạn sử dụng khi bạn muốn một change detection thủ công.

## **Change Detection**

**Change Detection** là quá trình mà Angular kiểm tra xem có thay đổi dữ liệu nào trong ứng dụng cần được phản ánh lên giao diện người dùng (UI) hay không.

Khi có thay đổi, `Change Detection` sẽ cập nhật các `View` liên quan, và sau đó Angular sẽ cập nhật `DOM` dựa trên các thay đổi đó.

### **Change Detection hoạt động thế nào**



## **Data Binding**

Một quy trình cho phép các ứng dụng hiển thị các giá trị dữ liệu cho người dùng và phản hồi các hành động của người dùng. Các hành động của người dùng bao gồm nhấp chuột, chạm, nhấn phím, v.v.

Trong data binding, bạn khai báo mối quan hệ giữa một widget HTML và nguồn dữ liệu, và để framework xử lý chi tiết. Data binding là một sự thay thế cho việc đẩy các giá trị dữ liệu ứng dụng vào HTML thủ công, gắn kết các trình nghe sự kiện, kéo các giá trị thay đổi từ màn hình và cập nhật các giá trị dữ liệu ứng dụng.

Đọc về các kiểu binding trong Template Syntax trong Angular:

- Interpolation
- Property binding
- Event binding
- Attribute binding
- Class and style binding
- Two-way data binding với ngModel

---

**Declarable**

Một lớp mà bạn có thể thêm vào danh sách declarations của một NgModule. Bạn có thể khai báo các components, directives và pipes, trừ khi chúng có cờ standalone trong decorator được đặt là true, điều này làm cho chúng trở thành standalone. Lưu ý: các components/directives/pipes standalone không phải là declarables. Thêm thông tin về các lớp standalone có thể được tìm thấy dưới đây.

Không khai báo các đối tượng sau:

- Một lớp đã được khai báo là standalone.
- Một lớp đã được khai báo trong một NgModule khác.
- Một mảng các directives nhập từ một package khác. Ví dụ, không khai báo `FORMS_DIRECTIVES` từ `@angular/forms`.
- Các lớp NgModule.
- Các lớp service.
- Các lớp và đối tượng không phải của Angular, chẳng hạn như chuỗi, số, hàm, mô hình thực thể, cấu hình, logic doanh nghiệp và các lớp trợ giúp.
Lưu ý rằng các declarables cũng có thể được khai báo như standalone và chỉ cần được nhập vào trong các components standalone khác hoặc NgModules hiện có, để tìm hiểu thêm, xem hướng dẫn Standalone components.

---

**Decorator | Decoration**

Một hàm sửa đổi định nghĩa lớp hoặc thuộc tính. Decorators là một tính năng ngôn ngữ JavaScript thử nghiệm (giai đoạn 3). Một decorator cũng được gọi là annotation. TypeScript thêm hỗ trợ cho decorators.

Angular định nghĩa các decorators để gắn metadata cho các lớp hoặc thuộc tính để nó biết các lớp hoặc thuộc tính đó có ý nghĩa gì và cách chúng hoạt động.

Để tìm hiểu thêm, xem [Class decorator](#). Cũng xem [Class field decorator](#).

---

**Dependency Injection (DI)**

Một mẫu thiết kế và cơ chế để tạo ra và cung cấp một số phần của ứng dụng (dependencies) cho các phần khác của ứng dụng cần chúng.

Trong Angular, các dependencies thường là services, nhưng cũng có thể là các giá trị, chẳng hạn như chuỗi hoặc hàm. Một injector của ứng dụng (được tạo tự động trong quá trình bootstrap) khởi tạo các dependencies khi cần, sử dụng một provider được cấu hình của service hoặc giá trị. Đọc thêm trong [Dependency Injection in Angular](#).

---

**DI Token**

Một token tìm kiếm liên kết với một dependency provider, để sử dụng với hệ thống dependency injection.

---

**Directive**

Một lớp có thể sửa đổi cấu trúc của DOM hoặc sửa đổi các thuộc tính trong DOM và mô hình dữ liệu của component. Định nghĩa lớp directive ngay trước đó được theo sau bởi decorator `@Directive()` cung cấp metadata.

Một lớp directive thường liên kết với một phần tử HTML hoặc thuộc tính, và phần tử hoặc thuộc tính đó thường được gọi là directive. Khi Angular tìm thấy một directive trong một template HTML, nó tạo ra một instance lớp directive tương ứng và giao cho instance đó quyền điều khiển phần đó của DOM trình duyệt.

Angular có ba loại directive:

- Components sử dụng `@Component()` để liên kết một template với một lớp. `@Component()` là một phần mở rộng của `@Directive()`.
- Attribute directives sửa đổi hành vi và kiểu dáng của các phần tử trang.
- Structural directives sửa đổi cấu trúc của DOM.

Angular cung cấp một số directives tích hợp bắt đầu bằng tiền tố `ng`. Bạn cũng có thể tạo mới các directives để thực hiện chức năng riêng của mình. Bạn liên kết một selector với một custom directive; điều này mở rộng cú pháp template mà bạn có thể sử dụng trong ứng dụng của mình. Một selector là một thẻ HTML, ví dụ như `<my-directive>`.

UpperCamelCase, như `NgIf`, chỉ một lớp directive. Bạn có thể sử dụng UpperCamelCase khi mô tả các thuộc tính và hành vi của directive.

lowerCamelCase, như `ngIf`, chỉ tên thuộc tính của một directive. Bạn có thể sử dụng lowerCamelCase khi mô tả cách áp dụng directive cho một phần tử trong template HTML.

---

**Domain-Specific Language (DSL)**

Một thư viện hoặc API chuyên dụng. Để tìm hiểu thêm, xem [Domain-specific language](#). Angular mở rộng TypeScript với các ngôn ngữ chuyên dụng cho một số lĩnh vực liên quan đến ứng dụng Angular, được định nghĩa trong các NgModules như animations, forms, và routing và navigation.

---

**Dynamic Component Loading**

Một kỹ thuật để thêm một component vào DOM trong thời gian chạy. Yêu cầu bạn loại bỏ component khỏi quá trình biên dịch và sau đó kết nối nó với framework change-detection và event-handling của Angular khi bạn thêm nó vào DOM.

Cũng xem [Custom element](#), cung cấp một con đường dễ dàng hơn với cùng kết quả.

--- 

**Eager Loading**

Các NgModules hoặc components được tải khi khởi động được gọi là eager-loaded, để phân biệt với các module hoặc component được tải trong thời gian chạy, được gọi là lazy-loaded. Xem thêm về lazy loading.

---

**ECMAScript**

Chỉ dẫn chính thức của ngôn ngữ JavaScript.

Không phải tất cả trình duyệt đều hỗ trợ tiêu chuẩn ECMAScript mới nhất, nhưng bạn có thể sử dụng một transpiler để viết mã sử dụng các tính năng mới nhất, sau đó mã sẽ được biên dịch lại thành mã có thể chạy trên các phiên bản được trình duyệt hỗ trợ. Một ví dụ về transpiler là TypeScript. Để tìm hiểu thêm, xem [Browser Support](#).

---

**Element**

Angular định nghĩa một lớp `ElementRef` để bọc các phần tử UI gốc theo cách render-specific. Trong hầu hết các trường hợp, điều này cho phép bạn sử dụng các templates Angular và data binding để truy cập các phần tử DOM mà không cần tham chiếu đến phần tử gốc.

Tài liệu thường đề cập đến elements là khác biệt với DOM elements. Elements là các instance của lớp `ElementRef`. Các DOM elements có thể được truy cập trực tiếp, nếu cần.

Để tìm hiểu thêm, xem [Custom element](#).

**Entry Point**

Một module JavaScript được thiết kế để được nhập bởi người dùng của một npm package. Một entry-point module thường xuất khẩu lại các biểu tượng từ các module nội bộ khác. Một package có thể chứa nhiều entry points. Ví dụ, package `@angular/core` có hai entry-point modules, có thể được nhập bằng cách sử dụng tên module `@angular/core` và `@angular/core/testing`.

---

**Form Control**

Một instance của `FormControl`, là một phần quan trọng trong việc xây dựng forms trong Angular. Cùng với `FormGroup` và `FormArray`, theo dõi giá trị, validation và trạng thái của một phần tử nhập liệu trong form.

Đọc thêm về forms trong [Introduction to forms in Angular](#).

---

**Form Model**

Là "nguồn sự thật" cho giá trị và trạng thái xác thực của một phần tử nhập liệu trong form tại một thời điểm cụ thể. Khi sử dụng reactive forms, form model được tạo ra rõ ràng trong lớp component. Khi sử dụng template-driven forms, form model được tạo ra ngầm định bởi các directives.

Tìm hiểu thêm về reactive và template-driven forms trong [Introduction to forms in Angular](#).

---

**Form Validation**

Một quá trình kiểm tra diễn ra khi giá trị form thay đổi và báo cáo xem các giá trị đưa vào có chính xác và đầy đủ, theo các ràng buộc đã định nghĩa hay không. Reactive forms áp dụng các hàm validator. Template-driven forms sử dụng các validator directives.

Để tìm hiểu thêm, xem [Form Validation](#).

---

**Immutability**

Khả năng không thay đổi trạng thái của một giá trị sau khi nó được tạo ra. Reactive forms thực hiện các thay đổi bất biến, tức là mỗi thay đổi trong dữ liệu mô hình sẽ tạo ra một mô hình dữ liệu mới thay vì sửa đổi mô hình hiện tại. Template-driven forms thực hiện các thay đổi có thể thay đổi với `NgModel` và data binding hai chiều để sửa đổi mô hình dữ liệu hiện tại.

---

**Injectable**

Một lớp Angular hoặc định nghĩa khác cung cấp một dependency thông qua cơ chế dependency injection. Một lớp service injectable phải được đánh dấu bằng decorator `@Injectable()`. Các đối tượng khác, chẳng hạn như giá trị hằng, cũng có thể là injectable.

---

**Injector**

Một đối tượng trong hệ thống dependency injection của Angular có thể tìm kiếm một dependency theo tên trong bộ nhớ cache của nó hoặc tạo ra một dependency sử dụng một provider đã được cấu hình. Injectors được tạo tự động cho các NgModules trong quá trình bootstrap và được kế thừa qua hệ thống phân cấp component.

Một injector cung cấp một instance duy nhất của một dependency, và có thể tiêm (inject) instance này vào nhiều component.
Một hệ thống phân cấp injectors tại cấp NgModule và component có thể cung cấp các instance khác nhau của một dependency cho các component của chính nó và các component con.
Bạn có thể cấu hình injectors với các providers khác nhau để cung cấp các triển khai khác nhau của cùng một dependency.
Tìm hiểu thêm về hệ thống phân cấp injectors trong [Hierarchical Dependency Injectors](#).

---

**Input**

Khi định nghĩa một directive, decorator `@Input()` trên một thuộc tính của directive sẽ làm cho thuộc tính đó có sẵn như một mục tiêu của property binding. Giá trị dữ liệu chảy vào thuộc tính input từ nguồn dữ liệu được xác định trong biểu thức template bên phải dấu "=".

Để tìm hiểu thêm, xem các decorator `@Input()` và `@Output()`.

---

**Interpolation**

Một hình thức của property data binding trong đó một biểu thức template giữa dấu ngoặc nhọn kép `{{}}` được hiển thị dưới dạng văn bản. Văn bản đó có thể được nối với các văn bản xung quanh trước khi được gán cho một thuộc tính của phần tử hoặc hiển thị giữa các thẻ phần tử, như trong ví dụ này:

```html
<label>My current hero is {{hero.name}}</label>
```

Đọc thêm trong [Interpolation guide](#).

---

**Ivy**

Ivy là tên mã lịch sử cho pipeline biên dịch và render hiện tại trong Angular. Đây hiện là engine duy nhất được hỗ trợ, vì vậy tất cả mọi thứ đều sử dụng Ivy.

**JavaScript**

Để tìm hiểu thêm, xem [ECMAScript](#). Để tìm hiểu thêm, xem [TypeScript](#).

---

**Just-in-time (JIT) Compilation**

Trình biên dịch just-in-time (JIT) của Angular chuyển đổi mã HTML và TypeScript của Angular thành mã JavaScript hiệu quả trong thời gian chạy, là một phần của quá trình bootstrapping.

JIT là chế độ biên dịch mặc định cho đến Angular 8 (xem [Choosing a compiler](#) để tìm hiểu thêm). JIT không được khuyến khích sử dụng trong môi trường production vì nó tạo ra các payload ứng dụng lớn làm giảm hiệu suất khởi động.

So sánh với biên dịch ahead-of-time (AOT).

---

**Lazy Loading**

Một quá trình giúp tăng tốc thời gian tải ứng dụng bằng cách chia ứng dụng thành nhiều bundle và tải chúng khi cần. Ví dụ, các dependency có thể được lazy loaded khi cần. Cách này khác biệt so với các module được eager-loaded, cần thiết cho module gốc và được tải khi khởi chạy.

Router của Angular sử dụng lazy loading để tải các view con chỉ khi view cha được kích hoạt. Tương tự, bạn có thể xây dựng các custom elements có thể được tải vào ứng dụng Angular khi cần.

---

**Library**

Trong Angular, một project cung cấp các chức năng có thể được sử dụng trong các ứng dụng Angular khác. Một library không phải là một ứng dụng Angular hoàn chỉnh và không thể chạy độc lập.

Để thêm chức năng tái sử dụng Angular vào các ứng dụng web không phải Angular, sử dụng Angular custom elements.

Các nhà phát triển library có thể sử dụng Angular CLI để tạo scaffolding cho một library mới trong một workspace hiện có và có thể xuất bản library như một npm package.
Các nhà phát triển ứng dụng có thể sử dụng Angular CLI để thêm một library đã xuất bản để sử dụng với ứng dụng trong cùng một workspace.
Xem thêm về [schematic](#).

---

**Lifecycle Hook**

Một interface cho phép bạn tham gia vào vòng đời của các directives và components khi chúng được tạo, cập nhật và bị hủy.

Mỗi interface có một phương thức hook duy nhất, tên phương thức là tên của interface có thêm tiền tố `ng`. Ví dụ, interface `OnInit` có một phương thức hook tên là `ngOnInit`.

Angular chạy các phương thức hook này theo thứ tự sau:

| Phương thức hook | Chi tiết |
|------------------|----------|
| 1. `ngOnChanges` | Khi giá trị binding input hoặc output thay đổi. |
| 2. `ngOnInit` | Sau lần `ngOnChanges` đầu tiên. |
| 3. `ngDoCheck` | Kiểm tra thay đổi tùy chỉnh của developer. |
| 4. `ngAfterContentInit` | Sau khi nội dung của component được khởi tạo. |
| 5. `ngAfterContentChecked` | Sau mỗi lần kiểm tra nội dung của component. |
| 6. `ngAfterViewInit` | Sau khi các view của component được khởi tạo. |
| 7. `ngAfterViewChecked` | Sau mỗi lần kiểm tra các view của component. |
| 8. `ngOnDestroy` | Trước khi directive bị hủy. |

Để tìm hiểu thêm, xem [Lifecycle Hooks](#).

---

**Module**

Nói chung, một module tập hợp một khối mã dành riêng cho một mục đích cụ thể. Angular sử dụng các module JavaScript tiêu chuẩn và cũng định nghĩa một module Angular, NgModule.

Trong JavaScript (hoặc ECMAScript), mỗi file là một module và tất cả các đối tượng được định nghĩa trong file đó thuộc về module đó. Các đối tượng có thể được xuất khẩu, làm cho chúng công khai, và các đối tượng công khai có thể được nhập vào để sử dụng bởi các module khác.

Angular được phân phối dưới dạng một bộ các module JavaScript. Một bộ các module JavaScript cũng được gọi là một library. Mỗi tên library của Angular bắt đầu bằng tiền tố `@angular`. Cài đặt các library của Angular với trình quản lý gói npm và nhập các phần của chúng bằng các khai báo import trong JavaScript.

So sánh với NgModule.

---

**NgModule**

Một định nghĩa lớp được đi trước bởi decorator `@NgModule()`, khai báo và phục vụ như một manifest cho một khối mã dành cho một miền ứng dụng, một workflow, hoặc một tập hợp các khả năng có liên quan chặt chẽ.

Giống như một module JavaScript, một NgModule có thể xuất khẩu chức năng để sử dụng bởi các NgModule khác và nhập chức năng công khai từ các NgModule khác. Metadata của một lớp NgModule tập hợp các components, directives, và pipes mà ứng dụng sử dụng cùng với danh sách các imports và exports. Xem thêm về [declarable](#).

NgModules thường được đặt tên theo file mà chúng được định nghĩa. Ví dụ, lớp `DatePipe` của Angular thuộc về một feature module tên là `date_pipe` trong file `date_pipe.ts`. Bạn nhập chúng từ một package Angular có phạm vi như `@angular/core`.

Mỗi ứng dụng Angular có một root module. Theo quy ước, lớp này được gọi là `AppModule` và nằm trong file `app.module.ts`.

Để tìm hiểu thêm, xem [NgModules](#).

---

**npm Package**

Trình quản lý gói npm được sử dụng để phân phối và tải các module và libraries của Angular.

Tìm hiểu thêm về cách Angular sử dụng [Npm Packages](#).

**ngc**

`ngc` là một trình biên dịch TypeScript-to-JavaScript xử lý các decorators, metadata và templates của Angular, và xuất ra mã JavaScript. Triển khai gần đây nhất được gọi là `ngtsc`, vì đây là một wrapper tối giản của trình biên dịch TypeScript `tsc`, bổ sung thêm một transform để xử lý mã Angular.

---

**Observable**

Một producer của nhiều giá trị, mà nó đẩy đến các subscribers. Được sử dụng để xử lý các sự kiện bất đồng bộ trong Angular. Bạn thực thi một observable bằng cách đăng ký (subscribe) vào nó thông qua phương thức `subscribe()`, truyền các callback để nhận thông báo về các giá trị mới, lỗi hoặc hoàn thành.

Các Observables có thể phát đi một trong các cách sau:

- Đồng bộ như một hàm trả về giá trị cho requester.
- Được lập lịch.
- Một subscriber nhận thông báo về các giá trị mới khi chúng được tạo ra và thông báo về việc hoàn thành bình thường hoặc lỗi.

Angular sử dụng thư viện bên ngoài có tên **Reactive Extensions (RxJS)**. Để tìm hiểu thêm, xem [Observables](#).

---

**Observer**

Một đối tượng được truyền vào phương thức `subscribe()` của một observable. Đối tượng này định nghĩa các callback cho subscriber.

---

**Output**

Khi định nghĩa một directive, decorator `@Output{}` trên một thuộc tính directive làm cho thuộc tính đó có sẵn như một mục tiêu của event binding. Các sự kiện sẽ phát ra từ thuộc tính này đến receiver được xác định trong biểu thức template phía bên phải dấu "=".

Để tìm hiểu thêm, xem [@Input() và @Output() decorator functions](#).

---

**Pipe**

Một lớp được đi trước bởi decorator `@Pipe{}` và định nghĩa một hàm chuyển đổi các giá trị đầu vào thành các giá trị đầu ra để hiển thị trong view. Angular định nghĩa nhiều loại pipes, và bạn có thể định nghĩa các pipes mới.

Để tìm hiểu thêm, xem [Pipes](#).

---

**Platform**

Trong thuật ngữ Angular, một platform là ngữ cảnh mà ứng dụng Angular chạy. Platform phổ biến nhất cho các ứng dụng Angular là trình duyệt web, nhưng nó cũng có thể là hệ điều hành của một thiết bị di động, hoặc một máy chủ web.

Hỗ trợ cho các platform runtime khác nhau của Angular được cung cấp bởi các package `@angular/platform-*`. Các package này cho phép các ứng dụng sử dụng `@angular/core` và `@angular/common` thực thi trong các môi trường khác nhau bằng cách cung cấp các triển khai để thu thập đầu vào người dùng và hiển thị giao diện người dùng cho platform đã cho. Việc tách biệt các chức năng đặc thù của platform cho phép nhà phát triển sử dụng phần còn lại của framework mà không phụ thuộc vào platform.

Khi chạy trên trình duyệt web, `BrowserModule` được nhập từ package `platform-browser`, hỗ trợ các dịch vụ đơn giản hóa việc xử lý sự kiện và bảo mật, và cho phép ứng dụng truy cập các tính năng đặc thù của trình duyệt như xử lý đầu vào từ bàn phím và điều khiển tiêu đề của tài liệu đang được hiển thị. Tất cả các ứng dụng chạy trên trình duyệt đều sử dụng cùng một dịch vụ platform.

Khi sử dụng rendering phía server (SSR), package `platform-server` cung cấp các triển khai máy chủ web của DOM, XMLHttpRequest, và các tính năng cấp thấp khác không phụ thuộc vào trình duyệt.

---

**Polyfill**

Một npm package lấp đầy các khoảng trống trong việc triển khai JavaScript của một trình duyệt. Xem [Browser Support](#) để biết các polyfill hỗ trợ các chức năng cụ thể cho các platform cụ thể.

---

**Project**

Trong Angular CLI, một project là một ứng dụng hoặc thư viện độc lập có thể được tạo hoặc sửa đổi bởi một lệnh của Angular CLI.

Một project, khi được tạo bởi lệnh `ng new`, bao gồm bộ các file nguồn, tài nguyên và các file cấu hình mà bạn cần để phát triển và kiểm tra ứng dụng bằng Angular CLI. Các project cũng có thể được tạo với các lệnh `ng generate application` và `ng generate library`.

Để tìm hiểu thêm, xem [Project File Structure](#).

File `angular.json` cấu hình tất cả các project trong một workspace.

---

**Provider**

Một đối tượng triển khai một trong các interfaces của Provider. Một đối tượng provider định nghĩa cách thức lấy một dependency injectable liên quan đến một DI token. Một injector sử dụng provider để tạo ra một instance mới của dependency cho lớp yêu cầu nó.

Angular đăng ký các provider của riêng mình với mỗi injector cho các dịch vụ mà Angular định nghĩa. Bạn có thể đăng ký các provider của riêng mình cho các dịch vụ mà ứng dụng của bạn cần.

Xem thêm về [service](#). Xem thêm về [dependency injection](#).

Tìm hiểu thêm trong [Dependency Injection](#).

---

**Reactive Forms**

Một framework để xây dựng các forms trong Angular thông qua mã trong một component. Phương pháp thay thế là template-driven form.

Khi sử dụng reactive forms:

- "Nguồn sự thật", model form, được định nghĩa trong lớp component.
- Validation được thiết lập thông qua các hàm validation thay vì các directive validation.
- Mỗi control được tạo một cách rõ ràng trong lớp component bằng cách tạo một instance của `FormControl` thủ công hoặc sử dụng `FormBuilder`.
- Các input element trong template không sử dụng `ngModel`.
- Các directive Angular liên quan có tiền tố `form`, chẳng hạn như `formControl`, `formGroup`, và `formControlName`.

Phương pháp thay thế là template-driven form. Để tìm hiểu và so sánh cả hai phương pháp, xem [Introduction to Angular Forms](#).

---

**Resolver**

Một lớp triển khai interface `Resolve` mà bạn sử dụng để sản xuất hoặc lấy dữ liệu cần thiết trước khi điều hướng đến một route được yêu cầu có thể hoàn tất. Bạn có thể sử dụng một hàm có chữ ký tương tự như phương thức `resolve()` thay thế cho interface `Resolve`. Các resolvers chạy sau khi tất cả các route guards cho cây route đã được thực thi và thành công.

Xem ví dụ về việc sử dụng resolve guard để lấy dữ liệu động.

---

**Route Guard**

Một phương thức điều khiển việc điều hướng đến một route yêu cầu trong một ứng dụng routing. Guards xác định xem một route có thể được kích hoạt hay hủy kích hoạt, và liệu một module lazy-loaded có thể được tải hay không.

Tìm hiểu thêm trong [Routing and Navigation guide](#).

---

**Router**

Một công cụ cấu hình và triển khai điều hướng giữa các trạng thái và views trong một ứng dụng Angular.

Module Router là một NgModule cung cấp các service providers và directives cần thiết cho việc điều hướng qua các views của ứng dụng. Một routing component là một component nhập khẩu module Router và có template chứa một phần tử `RouterOutlet` nơi nó có thể hiển thị các view được tạo ra bởi router.

Router định nghĩa việc điều hướng giữa các views trong một trang, trái ngược với điều hướng giữa các trang. Nó giải thích các liên kết giống như URL để xác định view nào sẽ được tạo ra hoặc hủy bỏ, và component nào sẽ được tải hoặc dỡ bỏ. Nó cho phép bạn tận dụng tính năng lazy loading trong các ứng dụng Angular.

Tìm hiểu thêm trong [Routing and Navigation](#).

---

**Router Outlet**

Một directive hoạt động như một placeholder trong template của một routing component. Angular sẽ render động template dựa trên trạng thái hiện tại của router.

---

**Routing Component**

Một component Angular với directive `RouterOutlet` trong template của nó, hiển thị các views dựa trên các điều hướng router.

Tìm hiểu thêm trong [Routing and Navigation](#).

---

**Rule**

Trong schematics, một hàm hoạt động trên cây file để tạo, xóa hoặc thay đổi file theo một cách cụ thể.

---

**Schematic**

Một thư viện scaffolding định nghĩa cách tạo hoặc biến đổi một project lập trình bằng cách tạo, sửa đổi, tái cấu trúc hoặc di chuyển các file và mã. Một schematic định nghĩa các rule hoạt động trên một hệ thống file ảo được gọi là cây.

Angular CLI sử dụng schematics để tạo và sửa đổi các project Angular và các phần của chúng.

Angular cung cấp một bộ schematics để sử dụng với Angular CLI. Xem [Angular CLI command reference](#). Lệnh `ng add` trong Angular CLI chạy schematics như một phần của việc thêm một thư viện vào project. Lệnh `ng generate` trong Angular CLI chạy schematics để tạo các ứng dụng, thư viện, và các cấu trúc mã Angular.

Các nhà phát triển thư viện có thể tạo các schematics cho phép Angular CLI thêm và cập nhật các thư viện đã xuất bản của họ và tạo ra các artifacts mà thư viện định nghĩa. Thêm các schematics này vào npm package mà bạn sử dụng để xuất bản và chia sẻ thư viện của mình.

Tìm hiểu thêm về [Schematics](#). Tìm hiểu thêm về [Integrating Libraries with the CLI](#).

---

**Schematics CLI**

Schematics có công cụ dòng lệnh riêng của chúng. Sử dụng Node 6.9 trở lên để cài đặt Schematics CLI toàn cục.

```bash
npm install -g @angular-devkit/schematics-cli
```

Điều này cài đặt executable schematics, mà bạn có thể sử dụng để tạo một bộ schematics mới với một schematic được đặt tên ban đầu. Thư mục bộ sưu tập là một workspace cho các schematics. Bạn cũng có thể sử dụng lệnh `schematics` để thêm một schematic mới vào một bộ sưu tập hiện có, hoặc mở rộng một schematic hiện có.

### scoped package
Một cách để nhóm các gói npm có liên quan. Các đối tượng Angular được cung cấp từ các gói npm có tên bắt đầu với phạm vi Angular, ví dụ: `@angular/core`, `@angular/common`, `@angular/forms`, và `@angular/router`.

Bạn có thể nhập một scoped package theo cách giống như nhập một gói bình thường.

**Ví dụ (import):**
```typescript
import { Component } from '@angular/core';
```

### server-side rendering
Một kỹ thuật tạo các trang ứng dụng tĩnh trên server, có thể tạo và phục vụ những trang này khi nhận được yêu cầu từ trình duyệt. Kỹ thuật này cũng có thể tạo trước các trang dưới dạng các tệp HTML để phục vụ sau.

Kỹ thuật này có thể cải thiện hiệu suất trên các thiết bị di động và các thiết bị có công suất thấp, đồng thời cải thiện trải nghiệm người dùng bằng cách hiển thị trang đầu tĩnh nhanh chóng trong khi ứng dụng phía client đang tải. Phiên bản tĩnh cũng giúp ứng dụng của bạn dễ dàng được các công cụ tìm kiếm phát hiện hơn.

Bạn có thể dễ dàng chuẩn bị một ứng dụng cho server-side rendering bằng cách sử dụng lệnh Angular CLI `ng add @angular/ssr`.

### service
Trong Angular, service là một lớp với decorator `@Injectable()` bao bọc logic và mã không liên quan đến giao diện người dùng, có thể tái sử dụng trong toàn bộ ứng dụng. Angular phân biệt giữa các component và services để tăng tính mô-đun và khả năng tái sử dụng.

Metadata `@Injectable()` cho phép lớp service được sử dụng với cơ chế Dependency Injection (DI). Lớp injectable được khởi tạo bởi một provider. Các injector duy trì danh sách các provider và sử dụng chúng để cung cấp các instance của service khi chúng được yêu cầu bởi các component hoặc service khác.

### standalone
Một cấu hình của các component, directive, và pipe cho phép lớp này có thể được nhập trực tiếp mà không cần khai báo trong bất kỳ NgModule nào.

Các component, directive, và pipe độc lập khác với các thành phần không độc lập bởi:

- Trường `standalone` trong decorator của chúng được thiết lập thành `true`.
- Cho phép nhập khẩu trực tiếp mà không cần thông qua NgModules.
- Xác định các phụ thuộc trực tiếp trong decorator của chúng.

### structural directive
Một loại directive có nhiệm vụ tạo hình cho bố cục HTML bằng cách thay đổi DOM. Việc thay đổi DOM bao gồm thêm, xóa, hoặc thao tác các phần tử và các phần tử con liên quan.

### subscriber
Một hàm định nghĩa cách thức nhận hoặc tạo ra các giá trị hoặc thông điệp để công bố. Hàm này được thực thi khi một người tiêu dùng gọi phương thức `subscribe()` của một observable.

Hành động đăng ký (subscribe) vào một observable sẽ kích hoạt việc thực thi của nó, liên kết các callback với observable, và tạo ra một đối tượng Subscription cho phép bạn hủy đăng ký.

### target
Một phần của dự án có thể xây dựng hoặc chạy được, được cấu hình như một đối tượng trong tệp cấu hình workspace, và được thực thi bởi một builder của Architect.

Trong tệp `angular.json`, mỗi dự án có một phần "architect" chứa các target cấu hình các builder. Một số target này tương ứng với các lệnh Angular CLI như build, serve, test, và lint.

### template
Mã định nghĩa cách hiển thị của một component. Template kết hợp HTML thuần với cú pháp data-binding của Angular, các directive và biểu thức template (các cấu trúc logic).

Một template được liên kết với một lớp component thông qua decorator `@Component()`. Mã template có thể được cung cấp trực tiếp trong thuộc tính `template`, hoặc trong một tệp HTML riêng biệt thông qua `templateUrl`.

### template-driven forms
Một phương thức xây dựng form trong Angular sử dụng các form HTML và các phần tử input trong giao diện người dùng. Phương thức thay thế là sử dụng framework reactive forms.

Khi sử dụng template-driven forms:
- "Nguồn sự thật" là template. Kiểm tra dữ liệu được định nghĩa qua các thuộc tính trên các phần tử input riêng lẻ.
- Two-way binding với `ngModel` giữ cho mô hình component đồng bộ với giá trị nhập vào của người dùng.

### template reference variable
Một biến được định nghĩa trong template, tham chiếu đến một instance liên quan đến một phần tử, ví dụ như một instance của directive, component, template như `TemplateRef`, hoặc phần tử DOM.

### token
Một mã định danh mờ dùng cho việc tra cứu nhanh trong bảng. Trong Angular, một DI token được sử dụng để tìm các provider của các dependencies trong hệ thống dependency injection.

### transpile
Quá trình dịch mã biến đổi một phiên bản JavaScript thành phiên bản khác; ví dụ: chuyển từ ES2015 xuống phiên bản ES5 cũ hơn.

### tree
Trong schematics, một hệ thống tệp ảo được đại diện bởi lớp Tree. Các quy tắc schematic nhận một đối tượng tree làm đầu vào, thao tác trên nó, và trả về một đối tượng tree mới.

### TypeScript
Một ngôn ngữ lập trình dựa trên JavaScript, nổi bật với hệ thống kiểu dữ liệu tùy chọn. TypeScript cung cấp kiểm tra kiểu tại thời điểm biên dịch và hỗ trợ công cụ mạnh mẽ như tự động hoàn thành mã, tái cấu trúc, tài liệu trực tuyến, và tìm kiếm thông minh.

TypeScript là ngôn ngữ được ưu tiên trong phát triển Angular.

### unidirectional data flow
Một mô hình luồng dữ liệu trong đó cây component luôn được kiểm tra thay đổi theo một hướng duy nhất từ cha sang con, giúp tránh các chu kỳ trong đồ thị kiểm tra thay đổi.

Trong thực tế, điều này có nghĩa là dữ liệu trong Angular chảy xuống dưới trong quá trình kiểm tra thay đổi. Component cha có thể dễ dàng thay đổi giá trị trong các component con vì component cha được kiểm tra trước.

### Server-side rendering
Một công cụ để thực hiện server-side rendering cho một ứng dụng Angular. Khi tích hợp với ứng dụng, Universal tạo và phục vụ các trang tĩnh trên server để đáp ứng các yêu cầu từ trình duyệt. Trang tĩnh ban đầu phục vụ như một placeholder tải nhanh trong khi toàn bộ ứng dụng đang được chuẩn bị cho việc thực thi bình thường trong trình duyệt. Để tìm hiểu thêm, xem **Angular server-side rendering**.


### View Engine
Một pipeline biên dịch và render trước đây được sử dụng bởi Angular. Nó đã được thay thế bởi Ivy và không còn được sử dụng nữa. View Engine đã bị deprecated trong phiên bản 9 và bị loại bỏ trong phiên bản 13.

### view hierarchy
Một cây các view liên quan có thể được xử lý như một đơn vị. View gốc được tham chiếu là host view của một component. Một host view là gốc của một cây các view lồng, được gom vào một `ViewContainerRef` (container view) gắn liền với một phần tử anchor trong component hosting. Hierarchy view là một phần quan trọng trong quá trình kiểm tra thay đổi của Angular.

Hierarchy view không đồng nghĩa với hierarchy component. Các view lồng trong bối cảnh của một hierarchy cụ thể có thể là host view của các component khác. Những component này có thể thuộc cùng một NgModule với component hosting, hoặc thuộc các NgModule khác.

### web component
Xem **custom element**.

### workspace
Một tập hợp các dự án Angular (ví dụ: các ứng dụng và thư viện) được hỗ trợ bởi Angular CLI, thường được đặt chung trong một kho mã nguồn (như git).

Lệnh `ng new` của Angular CLI tạo một thư mục hệ thống tệp (gốc workspace). Trong thư mục gốc này, nó cũng tạo tệp cấu hình workspace (`angular.json`) và, theo mặc định, một dự án ứng dụng ban đầu với tên giống tên workspace.

Các lệnh tạo hoặc thao tác với ứng dụng và thư viện (chẳng hạn như `add` và `generate`) phải được thực thi từ trong thư mục workspace. Để tìm hiểu thêm, xem **Workspace Configuration**.

### workspace configuration
Một tệp có tên `angular.json` ở cấp gốc của workspace Angular cung cấp các cấu hình mặc định cho toàn bộ workspace và từng dự án cụ thể cho các công cụ build và phát triển được cung cấp hoặc tích hợp với Angular CLI. Để tìm hiểu thêm, xem **Workspace Configuration**.

Các tệp cấu hình cụ thể của từng dự án được các công cụ sử dụng, chẳng hạn như `package.json` cho trình quản lý gói npm, `tsconfig.json` cho việc biên dịch TypeScript, và `tslint.json` cho TSLint. Để tìm hiểu thêm, xem **Workspace and Project File Structure**.

### zone
Một ngữ cảnh thực thi cho một tập hợp các tác vụ bất đồng bộ. Hữu ích cho việc gỡ lỗi, profiling, và kiểm tra các ứng dụng có các tác vụ bất đồng bộ như xử lý sự kiện, promises, và các lệnh gọi đến các máy chủ từ xa.

Một ứng dụng Angular chạy trong một zone, nơi nó có thể phản ứng với các sự kiện bất đồng bộ bằng cách kiểm tra sự thay đổi dữ liệu và cập nhật thông tin hiển thị thông qua việc giải quyết các data bindings.

Một zone client có thể thực hiện hành động trước và sau khi một tác vụ bất đồng bộ hoàn thành.

Tìm hiểu thêm về zones trong video của Brian Ford.

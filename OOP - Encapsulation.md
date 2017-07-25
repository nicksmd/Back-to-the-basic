#### Encapsulation

1. Tại sao Encapsulation lại quan trọng?

    Một thứ là quan trọng nếu nó có lý do để tồn tại:

- Hiding the complexity:

    Nhắc lại về Abstraction: là cách con người deal with sự phức tạp bằng
    cách nhìn đối tượng 1 cách tổng quát thay vì nhìn các tiểu tiết bên dưới.

    Ví dụ: xe máy. Người sử dụng chỉ cần biết xe máy có: tay lái, pedal, đèn, phanh, còi...
    mà không cần hiểu rõ/ hay ko cần quan tâm cách thức hoạt động của động cơ, hệ thống đánh lửa ... để có
    thể lái 1 chiếc xe máy.

    => Encapsulation giúp chúng ta đạt được tính abstraction bằng cách đóng goi
    các chi tiết ko cần thiết cho user.

    => giúp đối tượng dễ hiểu và dễ sử dụng hơn.

- Hiding the Source of change:

    Tiếp tục phép loại suy với chiếc xe máy: khi nhà sản xuất cải tiến động cơ => cách sử dụng
    xe máy của người dùng không thay đổi (hoặc rất ít thay đổi).

    => Encapsulation giúp chúng ta đạt được tính chất này vì mọi thay đổi đã được đóng gói
    ỏ tầng dưới và dấu khỏi người sử dụng.

    => tác dụng của Encapsulation là giảm thiểu tối đa tác động của sự thay đổi bên dưới đối
    với cách thức user sử dụng phần mềm.

    Không những thế, nó còn giúp giảm thiểu tác động của việc thay đổi 1 bộ phận
    với các bộ phận khác của đối tượng. (Ví dụ, cải tiến động cơ không buộc nhà sản xuất phải
    thiết kế lại phanh xe) => tăng tốc độ phát triển vì các bộ phận riêng rẽ có thể được phát triển
    song song.

2. Tại sao lại cần get/set (C#) hay getter/setter(Java)? Tại sao không tạo 1
    trường public và access trực tiếp vào trường?

    Một câu hỏi ám ảnh bao thế hệ sinh viên cntt và cả nhiều kĩ sư non tay.

    Có sự khác biệt nào giữa:
    ```java
        public String foo;
    ```
    và
    ```java
        private String foo;
        public void setFoo(String foo) { this.foo = foo; }
        public String getFoo() { return foo; }
    ```

    Câu trả lời: Có, ko thứ gì tồn tại mà ko có lí do cả:

        - Khi bạn nhận ra bạn cần làm một số biến đổi trước khi set/get (ví dụ, nhận giá trị cần set/get với
        một hằng số) => ko cần phải thay đổi mọi đoạn code liên quan trong codebase. Chỉ cần thay đổi hàm get/set.
        - Validation data trước khi set.
        - Thay đổi giá trị được set.
        - Giấu quy trình logic bên dưới: ví dụ getInfo() có thể get nhiều trường trước khi return giá trị
        - Có thể code nhiều mức độ accessibility (public, private, protected) với hàm get/set
        - lazy loading.
        - ...

    Tóm lại là sử dụng get/set cho ban nhiều lựa chọn hơn, tránh lặp lại code, hạn chế tác động của việc thay đổi
    code.

    Cần hiểu răng Encapsulation không chỉ là việc sử dụng get/set. Nó còn bao gồm cách ban tổ chức class/interface để
    đóng gói data/logic.

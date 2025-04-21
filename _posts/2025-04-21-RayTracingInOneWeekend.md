---
title: Ray tracing chỉ với 2 ngày cuối tuần. (WIP)
---
## Nguồn sách: 
[_Ray Tracing in One Weekend_](https://raytracing.github.io/books/RayTracingInOneWeekend.html)

Dịch bởi [Meikumo]({% link about.md %}).

## Cảm nhận của người dịch:
Đây là sách hướng dẫn cơ bản về khái niệm ray tracing. Ưu điểm của sách này là rất dễ hiểu để làm theo vì nó không sử dụng API nào. Nhưng cũng vì vậy, hướng dẫn này chỉ mang tính lý thuyết.
Mình khuyến khích các bạn hãy thử áp dụng kiến thức này để làm một ray tracer đơn giản trên Unity, Godot, Unreal Engine, Shadertoy,...

Một số từ chuyên ngành như ray tracing mình không dịch trực tiếp ra tiếng Việt, các bạn tham khảo [page này (WIP)]() để xem chú thích kĩ hơn của những từ chuyên ngành đó.

Nếu bạn gặp vấn đề với code, có câu hỏi, hoặc muốn chia sẽ ý tưởng cũng như thành quả của bạn, đừng ngại ngừng liên hệ với mình qua mail. Mình dịch quyển sách này hoàn toàn phi lợi nhuận
nên sẽ rất vui nếu nhận được phản hồi.

# Ray tracing chỉ với 2 ngày cuối tuần

<!DOCTYPE html>
<meta charset="utf-8">
<link rel="icon" type="image/png" href="../favicon.png">
<!-- Markdeep: https://casual-effects.com/markdeep/ -->



                                   **Ray Tracing in One Weekend**
                   [Peter Shirley][], [Trevor David Black][], [Steve Hollasch][]
                                                <br>
                                     Version 4.0.1, 2024-08-31
                                                <br>
                      Copyright 2018-2024 Peter Shirley. All rights reserved.



Tổng quan
====================================================================================================
Tôi đã dạy rất nhiều lớp về đồ họa vi tính qua nhiều năm, và tôi thường tập trung dạy về Ray Tracing.
Dù không cần thông qua bất cứ API nào, sinh viên vẫn có thể tạo ra được những tấm ảnh đẹp. Tôi quyết 
định sẽ biến giáo án của mình thành một hướng dẫn nhỏ gọn, đủ để bạn có thể tự viết một phần mềm ray 
tracing nhanh nhất có thể. Nó sẽ ko đầy đủ chức năng như các phần mềm công nghiệp, nhưng nó sẽ có những
chức năng như ánh sáng gián tiếp, thứ đã khiến ray tracing một phần không thể thiếu trong phim ảnh. 
Theo những chỉ dẫn này, bạn có sẽ có một phần mềm với kiến trúc linh hoạt, có thể mở rộng thêm chức 
năng theo nhu cầu của bạn.

Khi nói về 'Ray Tracing', nó có thể mang nhiều ý nghĩa. Thứ tôi miêu tả dưới đây nó gần hơn với cấu trúc 
của một Path Tracer đơn giản. Dù phần code có thể khá đơn giản (hãy để máy tính bạn làm hết phần việc!), 
tôi tin rằng bạn vẫn sẽ hài lòng với hình ảnh mình đã tự tạo ra.

Tôi sẽ hướng dẫn bạn viết một ray tracer theo thứ tự tôi hay viết, cũng như một số mẹo để debug. Khi 
hoàn thành cuốn sách này, bạn sẽ có một ray tracer đủ khả năng tạo nên những bức ảnh đẹp. Bạn có thể 
hoàn thành hướng dẫn này trong vòng 2 ngày cuối tuần, nhưng bạn cũng đừng lo lắng nếu nó tốn nhiều 
thời gian hơn thế. Quyển sách này viết bằng C++, nhưng bạn không cần phải sử dụng nó. Tuy nhiên, tôi 
khuyến khích sử dụng C++ vì nó là một ngôn ngữ nhanh và dễ chuyển đổi, cũng như được dùng bởi phần lớn 
các renderer trong ngành game và phim. Quyển sách này hạn chế dử dụng các chức năng "hiện đại" của C++,
nhưng những chức năng như "kế thừa" (inheritance) hay "nạp chồng toán tử" (operator overload) rất hữu dụng
và tiện lợi khi thiết kế raytracer.

> Tôi không đăng phần code hoàn chỉnh lên mạng, nhưng nó tồn tại và tôi sẽ bao gồm phần lớn code trừ những
> thứ quá hiển nhiên như một số toán tử của class vec3. Tôi tin rằng trực tiếp viết những dòng code sẽ giúp
> bạn học tốt hơn, nhưng nếu chúng được bày ra sẵn thì chúng ta sẽ lỡ dùng và cuối cùng chỉ có thể thật sự
> luyện tập nếu chúng không có sẵn. Vì thế đừng nhắn tôi hỏi xin code.

Tôi vẫn chừa lại phần đề cập trên vì tôi thấy mắc cười cách tôi đã thay đổi góc nhìn đó 180 độ. Phần code
đối chiếu đã giúp vài người đọc sửa được những lỗi nhỏ trong phần mềm. Tôi vẫn rất khuyến khích bạn tự 
viết code, nhưng bạn có thể tìm thấy phần code hoàn chỉnh của quyển sách này tại [RayTracing project on GitHub](https://github.com/RayTracing/raytracing.github.io/).

Một ghi chú khác về những dòng code được đề cập trong quyển sách này -- đoạn code của chúng tôi ưu tiên những tiêu chí sau:

  - Đoạn code phải liên quan đến các khái niệm đề cập trong sách.

  - Chúng tôi sử dụng C++, nhưng cố gắng viết nó đơn giản hết mức. Cách chúng tôi viết code rất gần
    với C, nhưng chúng tôi vẫn sử dụng các tính năng hiện đại của C++ nếu nó làm code dễ dùng / hiểu hơn.

  - Cách chúng tôi code dựa trên nguyên tác gần nhất có thể để duy trì sự nối tiếp.

  - Mỗi dòng code bao gồm 96 kí tự nhằm bảo đảm tính nhất quán giữa đoạn code gốc và đoạn code được ghim trong sách.

Đoạn code sẽ cung cấp cứu trúc cơ bản, với sự linh hoạt đủ để người đọc phát triển thêm. Có vô vạn
cách để tối ưu hóa và hiện đại hóa code, tuy nhiên, chúng tôi ưu tiên những phương án đơn giản.

Chúng tôi mặc định bạn đã có kiến thức cơ bản về vector (như tích vô hướng và cộng trừ vector). Nếu
bạn không biết về chúng, hay cần ôn tập lại, bạn có thể xem thử  [_Graphics Codex_](https://graphicscodex.com/) 
bởi Morgan McGuire, _Fundamentals of Computer Graphics_ bởi Steve Marschner và Peter Shirley, hay _Computer Graphics: 
Principles and Practice_ bởi J.D. Foley Và Andy Van Dam.

Tham khảo [file README](https://raytracing.github.io/) để biết thêm thông tin về dự án này, link đến repository trên GitHub,
cấu trúc thư mục, cách xây và chạy phần mềm, cũng như cách để tham khảo và cống hiến thêm cho dự án.

Tham khảo [tài liệu bổ sung][https://github.com/RayTracing/raytracing.github.io/wiki/Further-Readings] 
nếu muốn tìm hiểu thêm những tài liệu liên quan đến dự án.

Quyển sách này đã được format để có thể đọc trực tiếp trên web. Chúng tôi cũng bao gồm file PDFs nếu bạn cần trong phần mục "Assets".

Nếu bạn muốn liên hệ với chúng tôi, hãy gửi mail đến:

  - Peter Shirley, ptrshrl@gmail.com
  - Steve Hollasch, steve@hollasch.net
  - Trevor David Black, trevordblack@trevord.black

Lời cuối cùng, nếu bạn gặp vấn đề với code, có câu hỏi, hoặc muốn chia sẽ ý tưởng cũng như thành quả của bạn, tham khảo 
mục Discussions trên GitHub của dự án.

Cảm ơn tất cả những thành viên đã giúp đỡ cho dự án. Tên của mọi người được đề cập ở mục ghi nhận ở cuối quyển sách này.

Hãy bắt đầu code thôi!


Xuất file ảnh
====================================================================================================

Format PPM cho ảnh
---------------------
Khi bạn chạy một renderer, bạn cần một cách để đọc ảnh. Cách đơn giản nhất là xuất trực tiếp ra file.
Tuy nhiên, có rất nhiều format khác nhau và rất nhiều trong số đó rất phức tạp. Tôi luôn bắt đầu với
format ppm đơn giản. Đây là một ví dụ lấy từ Wikipedia:

    P3
    # "P3" ám chỉ rằng đầy là ảnh RGB viết theo mã ASCII
    # "3 2" là chiều dày và chiều cao của ảnh theo đơn vị pixel
    # "255" là giá trị tối đa của màu
    # Từ đầu cho đến phần số 255 được tính là header.
    # Từ đó trở đi là phần data của ảnh: RGB triplet.
    # Theo đúng thứ tự: R(Đỏ), G(Xanh lá), B(Xanh dương)
    # Y(Vàng), W(Trắng), Bl(Đen)
    3 2
    255
    255   0   0
      0 255   0
      0   0 255
    255 255   0
    255 255 255
      0   0   0

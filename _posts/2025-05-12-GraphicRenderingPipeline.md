---
layout: post
title: The rendering pipeline: quá trình biến hóa dữ liệu số thành đồ họa trên máy tính
permalink: "/TheRenderingPipeline/"
hidden: true
---

Bài viết trước: (Kĩ sư đồ họa là gì? Lập trình viên hay là họa sĩ?)[https://darumeik.github.io/DaruMeikBlog/WhatIsGraphicsProgrammer/]

Nhiệm vụ chính của một kĩ sư đồ họa là biến đổi những dữ liệu số của thế giới 3D sang hình ảnh ta có thể thấy trên màn hình 2D của máy tính. Hôm nay mình sẽ giới thiệu về một công cụ không thể thiếu để hoàn thành nhiệm vụ này: Quy trình kết xuất đồ họa (Graphics Rendering Pipeline).

## Định nghĩa của graphics rendering pipeline
Quy trình kết xuất đồ họa là một chuỗi các bước xử lý của máy tính nhằm tạo ra một hình ảnh 2D trên màn hình dựa trên các dữ liệu như: máy quay, thế giới 3D, ánh sáng,... 

- Hình blender

Lí do chúng ta xây dựng nên một quy trình là vì chúng giúp tăng tốc độ xử lý. Để dễ hình dung, bạn hãy tưởng tượng về quy trình làm một ổ bánh mì. Với đủ số lượng người, chúng ta có thể sản xuất hàng loạt các ổ bánh mì bằng cách chia đều phần việc ra: người lo bánh, người lo thịt, người lo rau,... Khi xong việc, ta sẽ truyền thành quả của mình cho người tiếp theo trong chuỗi và bắt đầu phần việc mới. Việc thực hiện song song công việc này tăng nhanh tốc độ sản xuất bánh mì (tốc độ xử lý ảnh). Tuy nhiên, dù là song song, ta không thể tránh khỏi một khoảng delay nhỏ bắt nguồn từ việc bước này phụ thuộc vào kết quả của bước trước (bạn không thể xếp thịt nếu chưa được truyền phần bánh). Vì vậy, thời gian hoàn thành quy trình sẽ bằng với thời gian của bước xử lý chậm nhất.

- Hình chuỗi hamburger (maybe from overcook)

Trên thật tế, vì việc render hình ảnh phụ thuộc vào cấu hình máy (ví dụ: GPU của Intel sẽ khác với NVidia và AMD), cũng như nhu cầu (ưu tiên độ chính xác cho phim ảnh, hay ưu tiên tốc độ xử lý cho game), chúng ta không có một mô hình quy trình dùng được cho mọi trường hợp. Tuy nhiên, bản chất và trình tự của quy trình gần như là không thay đổi, nên nhằm đồng bộ hóa các bước, một số API (giao diện lập trình ứng dụng) đồ họa như OpenGL, DirectX hay Vulkan đã ra đời. 

- Hình graphics API

Bài viết này mình nhắm đến giải thích về mô hình quy trình được giới thiệu trong sách (Real-Time Rendering)[https://www.amazon.com/Real-Time-Rendering-Fourth-Tomas-Akenine-M%C3%B6ller/dp/1138627003?tag=realtimerenderin], một mô hình thường được dùng trong các phần mềm chạy thời gian thực. Mô hình này bao gồm các bước:

1. Application Stage: Bước xử lý phần mềm 
2. Geometry Processing Stage: Bước xử lý hình học
3. Rasterizatoin Stage: Bước tạo raster
4. Pixel Processing Stage: Bước xử lý pixel

## Bước xử lý phần mềm (Application stage):

Bước xử lý phần mềm là bước đầu tiên trong chuỗi xử lý. Bước này có tên như vậy vì đa phần code sẽ chạy dưới dạng trên CPU dưới dạng phần mềm như bao code khác. Cũng vì thế, đây là bước mà lập trình viên có sự kiểm soát tuyệt đối. Cụ thể hơn, bước này là bước viết script C# cho Unity, hoặc bước viết script C++/ bước blueprint của Unreal Engine (UE).

Nhiệm vụ của bước này là thực hiện các phép toán như: phát hiện va chạm (collision detection), chạy thuật toán tăng tốc độ xử lý (accelaration algorithms), thực hiện animation, xử lý vật lý (physics simulation,)... Vì nó là bước đầu tiên, nó cũng ảnh hưởng tới tốc độ của những bước sau trong quy trình (ví dụ: bạn có thể tăng tốc độ xử lý khi chạy thuật toán giảm số lượng polygon cần render tại bước này). Ngoài ra, bước này cũng có thể được tối ưu bằng cách chạy trên GPU thông qua một compute shader, một chương tình chạy trên GPU đặc biệt lợi dụng khả năng tính toán song song của GPU.

## Bước xử lý hình học (Geometry stage)
Bước tiếp theo trong quá trình là bước xử lý hình học. Bước này sẽ được thực thi hoàn toàn trên GPU. Lập trình viên có một tí kiểm soát ở bước này thông qua việc sử dụng vertex shader, một chương trình trên GPU có nhiệm vụ thực thi các câu lệnh trên từng điểm (vertex) hoặc trên từng polygon. Để lập trình vertex shader, bạn có thể tham khảo (HLSL)[https://docs.unity3d.com/6000.0/Documentation/Manual/writing-shader-writing-shader-programs-hlsl.html] hoặc (shader graph)[https://docs.unity3d.com/Manual/shader-graph.html] đối với Unity, hoặc (material)[https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engine-materials] đối với UE

Tại bước này, máy tính sẽ thực thi các phép toán liên quan đến hình học nhằm xác định cái gì sẽ được vẽ lên màn hình, vẽ như thế nào, vẽ tại đâu,... Cụ thể hơn, nó thường gồm các bước sau (không theo thứ tự và có thể thêm các bước phụ khác):
 - Vertex shading: tính cụ thể tọa độ của vertex cũng như những thông tin của vertex cần dùng cho những bước sau (ví dụ như giá trị của pháp tuyến, tọa độ UV,...)
 - Projection: Biến đổi vị trí tọa độ của từng điểm từ không gian vật thể (object space) sang không gian thế giới (world space). Mình sẽ có một bài viết cụ thể về quá trình này sau.
 - Clipping: Để tối ưu hóa, chỉ những gì nằm trong khung hình của camera mới được render. Những vật nằm hoàn toàn bên trong sẽ được gửi đầy đủ thông tin của vertex sang các bước sau, và những vật nằm hoàn toàn bên ngoài sẽ bị lượt đi. Đối với những vật chí nằm một phần bên trong khung hình, chúng sẽ bị cắt, tạo các vertex mới ngay tại giao điểm giữa vật thể với khung hình và lượt đi những vertex nằm phía bên ngoài.
 - Screen mapping:  Thường là bước cuối cùng. Bước này thực hiện phép chiếu không gian 3D lên khung hình, tạo ra một hình ảnh 2D để render trên màn hình vi tính.

## Bước tạo raster (Rasterization stage)

## Bước xử lý pixel (Fragment stage)

## Nguồn tham khảo:


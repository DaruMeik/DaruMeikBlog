---
title: Ray tracing chỉ với 2 ngày cuối tuần. (WIP)
permalink: "/RayTracingInOneWeekend/"
---
## Nguồn sách: 
[_Ray Tracing in One Weekend_](https://raytracing.github.io/books/RayTracingInOneWeekend.html)

Dịch bởi [Meikumo](https://darumeik.github.io/DaruMeikBlog/about.html).

## Cảm nhận của người dịch:
Đây là sách hướng dẫn cơ bản về khái niệm ray tracing. Ưu điểm của sách này là rất dễ hiểu để làm theo vì nó không sử dụng API nào. Nhưng cũng vì vậy, hướng dẫn này hơi mang tính lý thuyết.
Mình khuyến khích các bạn hãy thử áp dụng kiến thức này để làm một ray tracer đơn giản trên Unity, Godot, Unreal Engine, Shadertoy,...

Một số từ chuyên ngành như ray tracing mình không dịch trực tiếp ra tiếng Việt, các bạn tham khảo [page này (WIP)]() để xem chú thích kĩ hơn của những từ chuyên ngành đó.

Nếu bạn gặp vấn đề với code, có câu hỏi, hoặc muốn chia sẽ ý tưởng cũng như thành quả của bạn, đừng ngại ngừng liên hệ với mình qua mail. Mình dịch quyển sách này hoàn toàn phi lợi nhuận
nên sẽ rất vui nếu nhận được phản hồi.

---

# Ray tracing chỉ với 2 ngày cuối tuần

<meta charset="utf-8">
<link rel="icon" type="image/png" href="../favicon.png">
<!-- Markdeep: https://casual-effects.com/markdeep/ -->

<p align="center">
<b>Ray Tracing in One Weekend</b>
<br>
<a href="https://github.com/petershirley">Peter Shirley</a>, 
<a href="https://github.com/trevordblack">Trevor David Black</a>,
<a href="https://github.com/hollasch">Steve Hollasch</a>
<br>
Version 4.0.1, 2024-08-31
<br>
Copyright 2018-2024 Peter Shirley. All rights reserved.
</p>


## 1. Tổng quan
Tôi đã dạy rất nhiều lớp về đồ họa vi tính qua nhiều năm, và tôi thường tập trung dạy về Ray Tracing.
Bởi vì sinh viên vẫn có thể tạo ra được những tấm ảnh đẹp dù không cần sử dụng bất cứ API nào. Tôi quyết 
định sẽ biến giáo án của mình thành một hướng dẫn nhỏ gọn, đủ để bạn có thể tự viết một phần mềm ray 
tracing nhanh nhất có thể. Nó sẽ ko đầy đủ chức năng như các phần mềm công nghiệp thật sự, nhưng nó sẽ 
có đủ các chức năng như ánh sáng gián tiếp, thứ đã khiến ray tracing một phần không thể thiếu trong 
phim ảnh. Theo những chỉ dẫn này, bạn sẽ có được một phần mềm với kiến trúc linh hoạt, có thể mở rộng 
thêm chức năng tùy theo nhu cầu của bạn.

Khi nói về 'Ray Tracing', nó có thể mang nhiều ý nghĩa. Thứ tôi miêu tả dưới đây nó gần hơn với cấu trúc 
của một Path Tracer đơn giản. Dù phần code có thể khá đơn giản (hãy để máy tính bạn làm hết phần việc!), 
tôi tin rằng bạn vẫn sẽ hài lòng với hình ảnh mình đã tự tạo ra.

Tôi sẽ hướng dẫn bạn viết một ray tracer theo thứ tự tôi hay viết, cũng như một số mẹo để debug. Khi 
hoàn thành cuốn sách này, bạn sẽ có một ray tracer đủ khả năng tạo nên những bức ảnh đẹp. Bạn có thể 
hoàn thành hướng dẫn này trong vòng 2 ngày cuối tuần, nhưng bạn cũng đừng lo lắng nếu nó tốn nhiều 
thời gian hơn thế. Quyển sách này viết bằng C++, nhưng bạn không cần phải sử dụng nó. Tuy nhiên, tôi 
khuyến khích sử dụng C++ vì nó là một ngôn ngữ nhanh và dễ chuyển đổi, cũng như được dùng bởi phần lớn 
các renderer trong ngành game và phim. Quyển sách này hạn chế dử dụng các chức năng "hiện đại" của C++,
nhưng những chức năng như "kế thừa" (inheritance) hay "nạp chồng toán tử" (operator overload) sẽ được sử
dụng vì chúng rất hữu ích và tiện lợi khi thiết kế một raytracer.

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

  - Cách chúng tôi code dựa trên nguyên tác gần nhất có thể để duy trì tính nối tiếp.

  - Mỗi dòng code bao gồm 96 kí tự nhằm bảo đảm tính nhất quán giữa đoạn code gốc và đoạn code được chú thích trong sách.

Đoạn code sẽ cung cấp một cấu trúc cơ bản, với sự linh hoạt đủ để người đọc phát triển thêm. Có vô vạn
cách để tối ưu hóa và hiện đại hóa code, tuy nhiên, chúng tôi ưu tiên những phương án đơn giản.

Chúng tôi mặc định bạn đã có kiến thức cơ bản về vector (như tích vô hướng và cách cộng trừ vector). Nếu
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


## 2. Xuất thử một hình ảnh

### 2.1 Format PPM cho ảnh
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

<figure>
<p align="center" width="100%">
  <img src="https://github.com/user-attachments/assets/ed872af6-2102-4d9a-833d-796b90bc06b9"
    alt="Cel shading" 
    style="width:25%">
  <figcaption><p align="center"><b>Figure 1:</b> <i>PPM Example</i></p></figcaption>
  </p>
</figure>

Hãy thử làm một đoạn code để xuất ra thứ tương tự:

```C++
#include <iostream>

int main() {

    // Hình ảnh

    int image_width = 256;
    int image_height = 256;

    // Render

    std::cout << "P3\n" << image_width << ' ' << image_height << "\n255\n";

    for (int j = 0; j < image_height; j++) {
        for (int i = 0; i < image_width; i++) {
            auto r = double(i) / (image_width-1);
            auto g = double(j) / (image_height-1);
            auto b = 0.0;

            int ir = int(255.999 * r);
            int ig = int(255.999 * g);
            int ib = int(255.999 * b);

            std::cout << ir << ' ' << ig << ' ' << ib << '\n';
        }
    }
}
```

<p align="center"><b>Listing 1:</b> [main.cc] <i>Tạo bức ảnh đầu tiên của bạn</i></p>

Có 1 số điểm cần lưu ý:
1. Các pixel sẽ được viết theo thứ tự từng dòng.
1. Các pixel từng dòng sẽ theo thứ tự từ trái sang phải.
1. Các dòng sẽ theo thứ tự từ trên xuống dưới.
1. Theo quy ước, giá trị của các màu R/G/B sẽ được lưu dưới dạng số thực nằm trong khoảng 0.0 tới 1.0. Các giá trị này sẽ được chuyển hóa sang số tự nhiên nằm trong khoảng từ 0 tới 255 khi xuất ra.
1. Bức ảnh sẽ có giá trị R chạy từ 0 (đen) đến 255 (đỏ) từ trái sang phải, và giá trị G chạy từ 0 (đen) đến 255 (xanh lá)
từ trên xuống dưới. Khi hòa đỏ và xanh lá ta sẽ được màu vàng nên ta có thể dự đoán phần góc phải cuối ảnh sẽ có màu vàng.

### 2.2 Tạo một file ảnh
---------------------
Bởi vì file ảnh sẽ được viết trực tiếp lên standard output stream (luồng output mặc định). Ta thường làm thế 
bằng cách sử dụng khả năng chuyển hướng của ">" từ command-line (giao diện dòng lệnh)

Trên Windows, bạn sẽ có xây một build debug thông qua CMake bằng cách chạy dòng lệnh này:

    cmake -B build
    cmake --build build

Rồi bạn có thể chạy phần mềm mới được build như thế này:

    build\Debug\inOneWeekend.exe > image.ppm

Sau này, bạn nên chạy những build đã được tối ưu hóa. Trong trường hợp đó bạn có thể dùng:

    cmake --build build --config release

và sau đó chạy phần mềm bằng:

    build\Release\inOneWeekend.exe > image.ppm

Ví dụ trên sử dụng CMake, chạy cùng một phương pháp chung với file CMakeLists.txt có bao gồm trong source code. 
Bạn cứ sử dụng bất kì môi trường (hay ngôn ngữ) nào mà bạn cảm thấy thoải mái.

Trên Mac hoặc Linux, đối với bản release build, bạn có thể chạy phần mềm như thế này:

    build/inOneWeekend > image.ppm

File build hoàn chỉnh cũng như hướng dẫn sử dụng có thể tìm thấy trong mục README của project.

Mở file sẽ hiển thị hình ảnh như thế này (thông qua ToyViewer trên mac, nếu phần mềm đọc ảnh của bạn không hỗ trợ đọc ppm thì bạn có thể search google "ppm viewer"):


<figure>
<p align="center" width="100%">
  <img src="https://github.com/user-attachments/assets/6f75b756-72c5-42de-ba20-92f4fcb10e2c"
    alt="Cel shading" 
    style="width:50%">
  <figcaption><p align="center"><b>Image 1:</b> <i>Bức ảnh PPM đầu tiên</i></p></figcaption>
  </p>
</figure>

Chúc mừng, đây chính là phần mềm "hello world" đầu tiên của bạn đối với đồ họa vi tính. 
Bạn hãy thử mở file ảnh của bạn bằng một phần mềm biên tập văn bản để xem thử, nó sẽ có hình dạng như thế này:

    P3
    256 256
    255
    0 0 0
    1 0 0
    2 0 0
    3 0 0
    4 0 0
    5 0 0
    6 0 0
    7 0 0
    8 0 0
    9 0 0
    10 0 0
    11 0 0
    12 0 0
    ...

<p style="text-align: center;"><b>Listing 2:</b> <i>Output của bức ảnh đầu tiên</i></p>

Nếu file ảnh ppm của bạn không giống vậy thì hãy kiểm tra lại phần code phía trên. Nếu nó nhìn giống thế nhưng không render được, 
thì có khả năng phần đuôi sau từng dòng lệnh của bạn không chính xác hoặc có gì đó tương tự đã làm phần mềm đọc ảnh của bạn hiểu lầm. 
Để debug lỗi này, bạn có thể sử dụng thử file test.ppm [tại đây](https://github.com/RayTracing/raytracing.github.io/tree/release/images). 
Điều này bảo đảm phần mềm đọc ảnh của　bạn đọc được format PPM cũng như dùng để đối chiếu với file của bạn.

Một số người đọc đã báo cáo trục trặc khi đọc file xuất ra trên Windows. Trong trường hợp này, lỗi có thể xuất phát từ việc file PPM
của bạn được viết dưới định dạng UTF-16 (thường xảy ra khi dùng PowerShell). Nếu gặp phải vấn đề này, bạn hãy tham khảo [Discussion 1114](https://github.com/RayTracing/raytracing.github.io/discussions/1114).

Nếu mọi thứ đều hiển thị chính xác, bạn đã set up xong hệ thống và IDE - những phần còn lại trong quyển sách này đều dựa trên cùng nguyên lý để render hình ảnh.

Nếu bạn muốn xuất ảnh theo một định dạng khác, bạn có thể tham khảo <mark style="background-color: LightGray">stb_image.h</mark>. Đây là một library chỉ gồm file header, có thể download full trên [GitHub](https://github.com/nothings/stb).

### 2.3 Tạo một thanh tiến trình
---------------------

Trước khi đến với phần tới của quyển sách, chúng ta hãy tạo thêm một thanh tiến trình khi xuất file.
Đây là một giải pháp tiện lợi để theo dõi tiến trình của một render tốn nhiều thời gian, cũng như giúp phát hiện
phần mềm bị freeze khi có loop vô tận cũng như các vấn đề khác.

Vì chúng ta sử dụng luồng output mặc định (<mark style="background-color: LightGray">std::cout</mark>) để xuất file nên chúng ta không thể sử dụng nó để ghi chú.
Thay vào đó, chúng ta sẽ sử dụng luồng output chuyên cho ghi chú (<mark style="background-color: LightGray">std::clog</mark>):

```C++
    for (int j = 0; j < image_height; ++j) {
        std::clog << "\rScanlines remaining: " << (image_height - j) << ' ' << std::flush;
        for (int i = 0; i < image_width; i++) {
            auto r = double(i) / (image_width-1);
            auto g = double(j) / (image_height-1);
            auto b = 0.0;

            int ir = int(255.999 * r);
            int ig = int(255.999 * g);
            int ib = int(255.999 * b);

            std::cout << ir << ' ' << ig << ' ' << ib << '\n';
        }
    }

    std::clog << "\rDone.                 \n";
```

<p style="text-align: center;"><b>Listing 3:</b> [main.cc] <i>Loop render chính với thanh tiến trình</i></p>

Bây giờ mỗi khi chạy phần mềm, bạn sẽ thấy được một thanh tiến trình hiển thị số hàng còn lại cần phải render.
Ở thời điểm hiện tại, sẽ có khả năng bạn không thấy được thanh này vì code bạn chạy quá nhanh. Nhưng đừng lo,
bạn sẽ có rất nhiều cơ hội để ngắm thanh tiến trình này khi chúng ta mở rộng chức năng của ray tracer này.

## 3 Class vec3
---------------------

Hầu hết các phần mềm đồ họa đều có một vài class để lưu trữ thông tin về vector hình học và màu. Trong nhiều
hệ thống, các vector này là 4D (tọa độ 3D + tọa độ đồng nhất, hay giá trị RGB + giá trị alpha (trong suốt)).
Chúng ta hiện chỉ cần 3 giá trị nên chúng ta sẽ sử dụng class <mark style="background-color: LightGray">vec3</mark> cho tất cả mọi thứ, bao gồm màu sắc, tọa độ, hướng, offset(độ lệch),...
Vài người không thích cách sử dụng này vì nó không giúp ta né khỏi làm những thứ ngờ nghệch như trừ giá trị tòa độ bằng giá trị màu sắc.
Đây là một ý kiến có lý, nhưng quyển sách này ưu tiên lựa chọn "ít code" nếu nó không sai một cách lộ liễu. Dù vậy, để phòng hờ, chúng ta
vẫn sẽ tạo 2 tên khác cho class <mark style="background-color: LightGray">vec3</mark>: <mark style="background-color: LightGray">point3</mark> và 
<mark style="background-color: LightGray">color</mark>. Vì đây chỉ là 2 cái tên khác của class vec3, bạn sẽ không được cảnh báo
nếu vô tình dùng <mark style="background-color: LightGray">color</mark> cho một hàm mong đợi <mark style="background-color: LightGray">point3</mark>,
và cũng không gì ngăn cản bạn cộng <mark style="background-color: LightGray">point3</mark> với <mark style="background-color: LightGray">color</mark>,
nhưng 2 cái tên này sẽ giúp code dễ đọc và dễ hiểu hơn.

Chúng ta sẽ định nghĩa class <mark style="background-color: LightGray">vec3</mark> trong một file header mới với tên <mark style="background-color: LightGray">vec3.h</mark>,
và sẽ định nghĩa luôn một số hàm chức năng của nó.

```C++ 
#ifndef VEC3_H
#define VEC3_H

#include <cmath>
#include <iostream>

class vec3 {
public:
    double e[3];

    vec3() : e{0,0,0} {}
    vec3(double e0, double e1, double e2) : e{e0, e1, e2} {}

    double x() const { return e[0]; }
    double y() const { return e[1]; }
    double z() const { return e[2]; }

    vec3 operator-() const { return vec3(-e[0], -e[1], -e[2]); }
    double operator[](int i) const { return e[i]; }
    double& operator[](int i) { return e[i]; }

    vec3& operator+=(const vec3& v) {
        e[0] += v.e[0];
        e[1] += v.e[1];
        e[2] += v.e[2];
        return *this;
    }

    vec3& operator*=(double t) {
        e[0] *= t;
        e[1] *= t;
        e[2] *= t;
        return *this;
    }

    vec3& operator/=(double t) {
        return *this *= 1/t;
    }

    double length() const {
        return std::sqrt(length_squared());
    }

    double length_squared() const {
        return e[0]*e[0] + e[1]*e[1] + e[2]*e[2];
    }
};

// point3 chỉ là một tên khác cho class vec3. Nó được sử dụng để làm code dễ đọc hơn
using point3 = vec3;


// Các hàm toán của vector

inline std::ostream& operator<<(std::ostream& out, const vec3& v) {
    return out << v.e[0] << ' ' << v.e[1] << ' ' << v.e[2];
}

inline vec3 operator+(const vec3& u, const vec3& v) {
    return vec3(u.e[0] + v.e[0], u.e[1] + v.e[1], u.e[2] + v.e[2]);
}

inline vec3 operator-(const vec3& u, const vec3& v) {
    return vec3(u.e[0] - v.e[0], u.e[1] - v.e[1], u.e[2] - v.e[2]);
}

inline vec3 operator*(const vec3& u, const vec3& v) {
    return vec3(u.e[0] * v.e[0], u.e[1] * v.e[1], u.e[2] * v.e[2]);
}

inline vec3 operator*(double t, const vec3& v) {
    return vec3(t*v.e[0], t*v.e[1], t*v.e[2]);
}

inline vec3 operator*(const vec3& v, double t) {
    return t * v;
}

inline vec3 operator/(const vec3& v, double t) {
    return (1/t) * v;
}

// Tích vô hướng
inline double dot(const vec3& u, const vec3& v) {
    return u.e[0] * v.e[0]
        + u.e[1] * v.e[1]
        + u.e[2] * v.e[2];
}

// Tích có hướng
inline vec3 cross(const vec3& u, const vec3& v) {
    return vec3(u.e[1] * v.e[2] - u.e[2] * v.e[1],
                u.e[2] * v.e[0] - u.e[0] * v.e[2],
                u.e[0] * v.e[1] - u.e[1] * v.e[0]);
}

inline vec3 unit_vector(const vec3& v) {
    return v / v.length();
}

#endif
```

<p style="text-align: center;"><b>Listing 4:</b> [vec3.h] <i>Định nghĩa của vec3 và các hàm chức năng</i></p>

Chúng ta sử dụng <mark style="background-color: LightGray">double</mark> ở đây nhưng một số ray tracer khác sẽ sử dụng <mark style="background-color: LightGray">float</mark>.
<mark style="background-color: LightGray">double</mark> có phạm vi và độ chính xác cao hơn, nhưng size của lớn gấp đôi <mark style="background-color: LightGray">float</mark> .
Sự khác biệt về size này là yếu tố quan trọng nếu bạn code dưới điều kiện khắt khe về bộ nhớ (ví dụ như shader phần cứng). Không có đáp án sai nên hãy sử dụng
cái bạn thích.

### 3.1 Hàm chức năng cho màu sắc
---------------------

Chúng ta sẽ sử dụng hàm <mark style="background-color: LightGray">vec3</mark> để viết một file header mới với tên <mark style="background-color: LightGray">color.h</mark>.
Chúng ta sẽ định nghĩa một hàm chức năng có nhiệm vụ xuất màu của một pixel lên luồng output mặc định.

```C++ 
#ifndef COLOR_H
#define COLOR_H

#include "vec3.h"

#include <iostream>

using color = vec3;

void write_color(std::ostream& out, const color& pixel_color) {
    auto r = pixel_color.x();
    auto g = pixel_color.y();
    auto b = pixel_color.z();

    // Chuyển đổi số thực trong khoảng [0,1] sang byte trong khoảng [0,255].
    int rbyte = int(255.999 * r);
    int gbyte = int(255.999 * g);
    int bbyte = int(255.999 * b);

    // Xuất màu ra luồng output
    out << rbyte << ' ' << gbyte << ' ' << bbyte << '\n';
}

#endif
```

<p style="text-align: center;"><b>Listing 5:</b> [color.h] <i>Hàm chức năng của màu sắc</i></p>

Bây giờ ta có thể edit file main để dùng hai file header mới này:

```C++
#include "color.h"
#include "vec3.h"

#include <iostream>

int main() {

    // Image

    int image_width = 256;
    int image_height = 256;

    // Render

    std::cout << "P3\n" << image_width << ' ' << image_height << "\n255\n";

    for (int j = 0; j < image_height; j++) {
        std::clog << "\rScanlines remaining: " << (image_height - j) << ' ' << std::flush;
        for (int i = 0; i < image_width; i++) {
            auto pixel_color = color(double(i)/(image_width-1), double(j)/(image_height-1), 0);
            write_color(std::cout, pixel_color);
        }
    }

    std::clog << "\rDone.                 \n";
}
```

<p style="text-align: center;"><b>Listing 6:</b> [main.cc] <i>Code cuối cùng cho hình ảnh PPM đầu tiên</i></p>

Tại đây, bạn sẽ có một file ảnh giống với với phần trước.
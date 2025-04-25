---
title: Kĩ sư đồ họa là gì? Lập trình viên hay là họa sĩ?
permalink: "/WhatIsGraphicsProgrammer/"
---

Việc hiển thị một hình ảnh trên máy tính của bạn là cả một phép màu. Phép màu đó đến được với bạn là nhờ vào công sức của những kĩ sư đồ họa (graphics programmer). 
Tiếc thay, vì bản chất hòa hợp giữa lập trình và hội họa, hai mảng vốn không gần gũi nhau mấy, con đường để trở thành một kĩ sư đồ họa theo mình vẫn rất là mơ hồ và phức tạp.
Thông qua bài viết này, mình mong con đường đó sẽ dễ đi hơn một tí cho các bạn có hứng thú và muốn trải nghiệm thử.

## Đồ họa vi tính là gì?
Để hiểu rõ vai trò của một kĩ sư đồ họa, ta phải đầu tiên tìm hiểu về thứ họ trực tiếp làm việc với: đồ họa vi tính. Trích từ Wikipedia:
    
    Computer graphics deals with generating images and art with the aid of computers.

Về nghĩa rộng, đồ họa vi tính là tất cả những hình ảnh được hiển thị trên màn hình máy tính. Nó bao gồm cái meme bạn vừa nhấp vào trên facebook, đoạn video bạn vừa xem trên youtube, hoạt họa của các nhân vật trên game bạn vừa chơi, cũng như trang web bạn đang đọc này.
Tuy nhiên, trong blog này mình sẽ sử dụng cụm từ đồ họa vi tính theo nghĩa hẹp để nói về đồ họa 3D thường thấy trong game và phim hoạt hình.

<figure>
<p align="center" width="100%">
  <img src="https://github.com/user-attachments/assets/9bbbc542-9c6f-434f-b728-d218bdbca3c3"
    alt="Toy story 1" 
    style="width:75%">
  <figcaption><p align="center">Toy story 1 (1995): Bộ phim đầu tiên làm hoàn toàn từ đồ họa vi tính (Credit: Pixar)</p></figcaption>
  </p>
</figure>

## Kĩ sư đồ họa là gì?
Kĩ sư đồ họa là người giúp đồ họa vi tính hiển thị lên màn hình của bạn một cách chính xác và đẹp nhất có thể. 
Công việc của họ bao gồm chuyển hóa thế giới 3D trong game sang chiếc màn hình 2D của bạn, làm việc với từng 
pixel để hiển thị đúng màu sắc mong muốn, tính toán cách ánh sáng tác động lên môi trường và ngược lại,... 

Cụ thể hơn, sau đây là một số ví dụ về những gì mà một kĩ sư đồ họa có thể làm:

<figure>
<p align="center" width="100%">
  <img src="https://github.com/user-attachments/assets/c795a8db-380f-446e-a1d3-aa7ba283e89f"
    alt="Cel shading" 
    style="width:40%">
  <figcaption><p align="center">Toon Shader biến họa tiết trên mô hình 3D sang nét vẽ 2D (Credit: Wikipedia)</p></figcaption>
  </p>
</figure>

<figure>
<p align="center" width="100%">
  <img src="https://github.com/user-attachments/assets/b1614d39-65f3-4742-b159-2e9f11cc389e"
    alt="Acerola Difference of Gaussians" 
    style="width:75%">
  <figcaption><p align="center">Dùng shader để tạo filter cho game (Credit: Acerola)</p></figcaption>
  </p>
</figure>

<figure>
<p align="center" width="100%">
  <img src="https://github.com/user-attachments/assets/2f0824fc-416c-4308-9368-4b1fb3891ec8"
    style="width:75%">
  <figcaption><p align="center">Render ảnh trong thời gian thực với raymarching SDF (Credit: Inigo Quilez)</p></figcaption>
  </p>
</figure>

<figure>
<p align="center" width="100%">
  <img src="https://github.com/user-attachments/assets/c08f4ac7-9d5c-4ca6-9280-4346ffd3e90b"
    style="width:75%">
  <figcaption><p align="center">Tạo bóng giả giúp vừa làm đẹp nhưng vẫn tối ưu hóa tốc độ game (Credit: LearnOpenGL)</p></figcaption>
  </p>
</figure>


<figure>
<p align="center" width="100%">
  <img src= "https://github.com/user-attachments/assets/5a7585d1-c1fe-41e2-94cf-93f6548a43ac"
    alt="Raytracing" 
    style="width:75%">
  <figcaption><p align="center">Hình ảnh được tạo ra từ công nghệ ray tracing (không phải ảnh chụp) (Credit: Physically Based Rendering:
From Theory To Implementation)</p></figcaption>
  </p>
</figure>

## Sự khác biệt giữa lập trình đồ họa và thiết kế đồ họa
Khi nghe từ đồ họa, nhiều người sẽ nghĩ rằng ngành kĩ sư đồ họa sẽ giống với thiết kế đồ họa. Nhưng thực tế, thì đây là 2 ngành khác biệt nhau hoàn toàn. 

Nếu ví thiết kế đồ họa là việc vẽ tranh của một họa sĩ, thì lập trình đồ họa là việc tạo ra cái cọ, cái khung để cho họa sĩ có thể vẽ một cách thoải mái.
Cụ thể hơn, khi làm việc với đồ họa vi tính, việc của thiết kế đồ họa sẽ tạo nên nhân vật, môi trường,... qua các phần mềm như Blender, Maya. Còn việc của các kĩ sư phần mềm là tạo nên các phần mềm đó cũng như các công cụ hỗ trợ.

<figure>
<p align="center" width="100%">
  <img src="https://github.com/user-attachments/assets/31d06934-7029-421b-898b-3dae09b8e222"
    alt="Blender" 
    style="width:75%">
  <figcaption><p align="center">Phần mềm blender hỗ trợ thiết kế đồ họa 3D (Credit: Blender)</p></figcaption>
  </p>
</figure>

## Những ai hợp để trở thành kĩ sư đồ họa?
Bạn nên trở thành kĩ sư đồ họa nếu:
- Bạn yêu thích toán học và muốn ứng dụng nó vào một cái gì đó mới lạ.
- Bạn yêu thích đồ họa, muốn sáng tạo và làm những cái gì mới.
- Bạn yêu thích đồ họa của các con game siêu thật như Cyberpunk2077, Death Stranding,... hay bạn yêu thích những game có đồ họa siêu đặc trưng như series Persona, BOTW, ... (aka bạn thích game)
- ~~Bạn là M, thích nhìn công thức toán và giải tích phân cũng như rà bug không hint không output~~

<figure>
<p align="center" width="100%">
  <img src="https://github.com/user-attachments/assets/b15e1669-4208-4eb2-8f70-61d28b748498"
    alt="Death Stranding" 
    style="width:75%">
  <figcaption><p align="center">Các nhân vật trong game Death Stranding (Credit: Kojima's Production)</p></figcaption>
  </p>
</figure>

## Disclaimer
Mình là một du học sinh nước ngoài nên mình không nắm rõ thị trường của ngành này tại Việt Nam, nhưng theo kinh nghiệm nói chung về thị trường ngành game thì lương sẽ không cao ngất ngưởng hay gì so với những bé bự IT khác. 
Bạn nên học nó khi đam mê và muốn học cái gì mới chứ về mặt tiền bạc thì mình không nói gì được. Tuy nhiên, theo quan điểm cá nhân, đây vẫn là một ngành vẫn còn rất nhiều cái để nghiên cứu và phát triển và rất có triển vọng.

## Bắt đầu từ đâu?
Theo mình, đây là một ngành rất nặng về toán nên những kiến thức từ đại học sẽ rất cần thiết (nhất là những môn đại cương như giải tích và đại số tuyến tính). Nên nếu các bạn thực sự hứng thú với nó thì hãy bắt đầu với việc học đại học ngành máy tính cho thật kỹ vào.

<figure>
<p align="center" width="100%">
  <img src="https://github.com/user-attachments/assets/1714c5b2-a069-4580-94d7-6d4f7ae07af1"
    alt="light transport equation" 
    style="width:75%">
  <figcaption><p align="center">Đẳng thức vận chuyển ánh sáng (Light transport equation) (Credit: Physically Based Rendering:
From Theory To Implementation)</p></figcaption>
  </p>
</figure>

Ngoài ra, dù mình mong muốn dịch và mang lại nhiều kiến thức nhất có thể, nhưng bản chất của ngành vẫn luôn phát triển không ngừng nên việc
đọc được các tài liệu nước ngoài cũng là rất quan trọng. Nếu các bạn có thể đọc được tiếng Anh, mình siêu khuyến khích các bạn hãy đọc qua 
các nguồn sau đây (đây là những sách / hướng dẫn miễn phí mà bản thân mình đã đọc qua):
- Channel Youtube về ứng dụng của đồ họa vi tính: <https://www.youtube.com/@Acerola_t/> \
(Độ khó:★ thích hợp cho những bạn muốn muốn có thêm động lực để chui đầu vào ngành này)
- Hướng dẫn về đồ họa trên Unity: <https://catlikecoding.com/unity/tutorials/> \
(Độ khó:★, thích hợp cho những bạn đã có kinh nghiệm hoặc muốn thử học Unity)
- Hướng dẫn sử dụng OpenGl: <https://learnopengl.com/> \
(Độ khó:★★, thích hợp cho người mới bắt đầu với API đồ họa, các bài viết có đầy đủ code để tham khảo và giải thích cụ thể từng khái niệm)
- Hướng dẫn sơ bộ về shader (có tiếng Việt): <https://thebookofshaders.com/> \
(Độ khó:★★, thích hợp cho những người hứng thú với shader, lập trình trên GPU cũng như muốn thử vẽ vời bằng toán)
- Sách lý thuyết về ray tracing: <https://pbr-book.org/> \
(Độ khó:★★★, thích hợp cho những bạn thích toán và đã có kiến thức cơ bản về lập trình nói chung)

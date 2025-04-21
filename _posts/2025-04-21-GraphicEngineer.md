---
title: Kĩ sư đồ họa là gì? Lập trình viên hay là họa sĩ?
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
Kĩ sư đồ họa là người giúp đồ họa vi tính hiển thị lên màn hình của bạn một cách chính xác và đẹp nhất có thể. Công việc của họ bao gồm chuyển hóa thế giới 3D trong game sang chiếc màn hình 2D của bạn, làm việc với từng pixel để hiển thị đúng màu sắc mong muốn,
tính toán cách ánh sáng tác động lên môi trường và ngược lại,... 

<figure>
<p align="center" width="100%">
  <img src="https://github.com/user-attachments/assets/b1614d39-65f3-4742-b159-2e9f11cc389e"
    alt="Acerola Difference of Gaussians" 
    style="width:75%">
  <figcaption><p align="center">Sử dụng shader để tạo filter đặc biệt cho game (Credit: Acerola)</p></figcaption>
  </p>
</figure>

<figure>
<p align="center" width="100%">
  <img src= "https://github.com/user-attachments/assets/5a7585d1-c1fe-41e2-94cf-93f6548a43ac"
    alt="Raytracing" 
    style="width:75%">
  <figcaption><p align="center">Hình ảnh được tạo ra từ công nghệ ray tracing (Credit: Physically Based Rendering:
From Theory To Implementation)</p></figcaption>
  </p>
</figure>

Một người bạn gắn liền không thể thiếu với kĩ sư đồ họa là GPU (Graphics Process Unit). Đây là phần cứng chuyên về xử lý hình ảnh. Lập trình trên GPU rất khác biệt so với trên CPU nên đây là một skillset không thể thiếu ở một kĩ sư đồ họa. 
Mình sẽ nói rõ hơn về nó việc lập trình trên GPU ở những bài viết sau.

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
- Bạn yêu thích toán học và muốn ứng dụng nó vào thực tế.
- Bạn yêu thích đồ họa, muốn sáng tạo và làm những cái gì mới.
- Bạn yêu thích đồ họa của các con game siêu thật như Cyberpunk2077, Death Stranding,... hay bạn yêu thích những game có đồ họa siêu đặc trưng như series Persona, BOTW, ... (aka bạn thích game)
- ~~Bạn là M và thích giải tích cũng như rà bug không có hiển thị output trên GPU~~

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
Theo mình, đây là một ngành rất nặng về toán nên những kiến thức từ đại học sẽ rất cần thiết (nhất là những môn đại cương như giải tích và đại số tuyến tính). 

Nếu các bạn có thể đọc được tiếng Anh, mình siêu khuyến khích các bạn hãy đọc qua các nguồn sau đây (đây là những sách / hướng dẫn bản thân mình đã đọc qua):
- Hướng dẫn sử dụng OpenGl: <https://learnopengl.com/> \
(Thích hợp cho người mới bắt đầu, các bài viết có đầy đủ code để tham khảo và giải thích cụ thể từng khái niệm)
- Hướng dẫn sơ bộ về shader (có tiếng Việt): <https://thebookofshaders.com/> \
(Thích hợp cho những người hứng thú với shader, lập trình trên GPU cũng như muốn thử vẽ vời bằng toán)
- Sách lý thuyết về ray tracing: <https://pbr-book.org/> \
(Thích hợp cho những bạn thích toán và đã có kiến thức cơ bản về lập trình nói chung)
- Hướng dẫn về đồ họa trên Unity: <https://catlikecoding.com/unity/tutorials/> \
(Thích hợp cho những bạn đã có kinh nghiệm với Unity và muốn tiếp xúc với lập trình trên GPU)
- Channel Youtube về ứng dụng của đồ họa vi tính: <https://www.youtube.com/@Acerola_t/> \
(Thích hợp cho những bạn muốn trầm trồ về những gì một kĩ sư đồ họa có thể làm được)

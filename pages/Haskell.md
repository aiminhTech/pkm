tags:: [[Funktional Programmieren]], [[Programming Language]]

- Haskell là một ngôn ngữ lập trình chức năng (functional programming) bậc cao, được phát triển với mục đích nghiên cứu và giảng dạy các khái niệm lập trình chức năng. Được đặt tên theo nhà toán học và nhà logic học Haskell Curry, Haskell nổi bật với việc sử dụng các khái niệm như hàm bậc cao (higher-order functions), bất biến (immutability), và tính trong suốt tham chiếu (referential transparency).
- ## Các đặc điểm chính của Haskell:
  collapsed:: true
	- **Ngôn ngữ thuần chức năng**: Haskell là một ngôn ngữ lập trình thuần chức năng, nghĩa là mọi tính toán đều được thực hiện thông qua các hàm. Tất cả các biến đều là bất biến, một khi đã được gán giá trị, chúng không thể bị thay đổi.
	- **Đánh giá lười (Lazy Evaluation)**: Trong Haskell, các biểu thức không được đánh giá ngay lập tức mà chỉ khi nào giá trị của chúng thực sự cần thiết. Điều này cho phép viết các chương trình với các cấu trúc điều khiển phức tạp mà không cần quan tâm tới việc sắp xếp thứ tự các phép tính.
	- **Tính trong suốt tham chiếu (Referential Transparency)**: Trong Haskell, cùng một biểu thức luôn cho ra cùng một giá trị bất kể nơi nào hoặc thời điểm nào nó được sử dụng. Điều này giúp việc lý luận và kiểm thử mã trở nên dễ dàng hơn.
	- **Hệ thống kiểu mạnh mẽ**: Haskell sử dụng hệ thống kiểu tĩnh mạnh mẽ, trong đó kiểu của các biến và hàm được xác định tại thời điểm biên dịch. Điều này giúp phát hiện nhiều lỗi tiềm ẩn trước khi chương trình được chạy.
- ##  Ứng dụng của Haskell:
  collapsed:: true
	- Haskell thường được sử dụng trong các lĩnh vực yêu cầu độ chính xác và hiệu suất cao như tài chính, xử lý dữ liệu lớn, phát triển các hệ thống phân tán, hoặc trong nghiên cứu học thuật.
	- Tuy nhiên, do sự phức tạp và sự khác biệt so với các ngôn ngữ lập trình mệnh lệnh như Python hay Java, Haskell chủ yếu được sử dụng trong các dự án đặc thù hoặc bởi những người có kinh nghiệm về lập trình chức năng.
- ## Funktionen
	- Für Funktionen in Haskell gelten folgende drei Regeln
		- Alle Funktionen haben ein Argument.
		- Alle Funktionen geben einen Wert zurück.
		- Eine Funktion,welche wiederholt mit demselben Argumentaufgerufen wird, hatimmerdenselben Rückgabewert.
	- Wenn die dritte Regel gilt, spricht man von *referential transparency*.
	- Eine Funktion in Haskell hat einen Namen und Anweisungen, welche spezifizieren, wie der Rückgabewert aus dem Argument bestimmt wird.
	- Beispiele für Funktionen in Haskelli
		- ```haskell
		  double x = x + x
		  max a b = if a > b then a else b
		  ```
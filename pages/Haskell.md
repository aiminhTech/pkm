tags:: [[Funktional Programmieren]], [[Programming Language]]

- https://www.google.com/search?client=safari&rls=en&q=haskell&ie=UTF-8&oe=UTF-8
-
- ##  Use Cases
  collapsed:: true
	- Haskell thường được sử dụng trong các lĩnh vực yêu cầu độ chính xác và hiệu suất cao như tài chính, xử lý dữ liệu lớn, phát triển các hệ thống phân tán, hoặc trong nghiên cứu học thuật.
	- Tuy nhiên, do sự phức tạp và sự khác biệt so với các ngôn ngữ lập trình mệnh lệnh như Python hay Java, Haskell chủ yếu được sử dụng trong các dự án đặc thù hoặc bởi những người có kinh nghiệm về lập trình chức năng.
- ## Courses
  collapsed:: true
	- https://medium.com/latinxinai/understanding-the-function-application-operator-in-haskell-e4ffe75fdc61
	- Youtube:
		- [https://well-typed.com/blog/2024/06/announcing-free-haskell-intro-course/](https://well-typed.com/blog/2024/06/announcing-free-haskell-intro-course/)
		- [https://teaching.well-typed.com/intro/](https://teaching.well-typed.com/intro/)
	- Playlist:
		- [https://www.youtube.com/playlist?list=PLD8gywOEY4HauPWPfH0pJPIYUWqi0Gg10](https://www.youtube.com/playlist?list=PLD8gywOEY4HauPWPfH0pJPIYUWqi0Gg10)
- ## Funktionen
  collapsed:: true
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
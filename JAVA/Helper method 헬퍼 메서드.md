
Class A
	public void a()
		helper();
	private void helper()


helper는 Class A에 private으로 선언된다.
다른 클래스에서는 helper를 호출할 수 없다. (없어야 한다.)
왜냐고? helper는 Class A의 멤버 메서드를 도우려고 만들어졌으니까. 그게 이 놈의 존재 이유고 그렇게 이름 붙여진 까닭이니까.

helper를 호출할 수 있는 놈은 Class A에 정의된, helper를 필요로 하는 멤버 메서드 뿐이다.

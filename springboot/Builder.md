# Builder

- 복잡한 객체의 생성 과정 및 표현 방법을 분리해 동일한 생성 절차에서 서로 다른 표현 결과를 만들 수 있게 하는 패턴
---

1. 롬복으로 빌더 패턴 적용
````
import lombok.Builder;
import lombok.Getter;

@Getter //Getter 생성 
public class LombokPerson {

	private  String name;
	private  String grade;
	private  int age;
	
	@Builder // 생성자 만든 후 위에 @Build 어노테이션 적용 
	public LombokPerson(String name, String grade, int age) {
		this.name = name;
		this.grade = grade;
		this.age = age;
	}
}
````
````
String name = "jueun";
int age = 24;
String grade = "4";
Person p1 = Person.builder()
		        .name(name)
		        .age(age)
		        .grade(grade)
		        .build();
}
````
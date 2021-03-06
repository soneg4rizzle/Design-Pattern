## 방문자 패턴(Visitor Pattern)
* 방문자 패턴은 방문자와 방문 공간을 분리하여 방문 공간이 방문자를 맞이할 때, 이후에 대한 행동을 방문자에게 위임하는 패턴입니다. 비슷한 객체에서 어떤 동작을 해야할 때 방문자 패턴을 사용하면 수행 로직을 분리할 수 있습니다. 즉, 데이터 구조와 연산을 분리하여 구조를 변경하지 않고 새로운 연산을 추가할 수 있습니다. 새로운 연산을 추가하고 싶으면 새로운 방문자를 추가하면 되는 형식입니다.
> 방문자 패턴은 데이터구조와 처리를 분리하는 패턴이다.  
> 데이터 구조안에 많은 요소들이 저장되어 있고, 이를 처리해 나가는 과정이 필요할 때, 처리에 해당하는 코드는 일반적으로 클래스 안에 기술해야 하는데 만약 처리 종류가 여러가지라면 새로운 종류의 처리가 들어올때마다 데이터 구조를 변경해야 하는 번거로움이 있습니다.  


## 방문자 패턴의 구조
> ![image](https://user-images.githubusercontent.com/96826443/170624105-5d281190-a2fe-46fd-aa75-61c4787f0444.png)  
> Visitor : element를 방문하고 동작을 구현하기 위한 인터페이스  
* ConcreteVisitor : Visitor를 상속받아 실제 동작을 구현한 클래스  
* Element : Visitor가 방문하여 수행해야 하는 대상(구조를 구성하는 인터페이스)  
* ConcreteElement : Element를 상속받아 실제 동작을 구현한 클래스
* ObjectStructure : Element를 가지고 있는 클래스

> 방문자 패턴은 알고리즘을 Object Structure로부터 분리하는 방법이다.  
> 기존에는 객체를 방문해서 알고리즘(코드)를 수행했지만 방문자패턴은 이미 존재하는 클래스나 객체의 수정없이 새로운 알고리즘을 기존 Object에 적용 할 수 있다.  

## 방문자 패턴 예시

```python
class Cat:
  def __init__(self, name, age):
    self.name = name
    self.age = age
   
   def speak(self):
     print("cat: meow")
```
* 위와 같은 코드가 존재할 때, 내부 PROPERTY인 name, age를 출력하는 함수는 존재하지 않는다.  
* 이 때 내부 PROPERTY를 출력하고 싶다면 새로운 함수를 정의할 수도 있지만 Cat 클래스를 수정하지 않고 출력하고 싶다면 방문자(Visitor) 패턴을 활용해볼 수 있다.  

## 구체적인 방문자 패턴 코드 예시
```python
class AnimalVisitor:
    def catVisit(self, element):
        pass

    def dogVisit(self, element):
        pass


class SpeakVisitor(AnimalVisitor):
    def catVisit(self, element):
        print("meow")

    def dogVisit(self, element):
        print("bark")


class NameVisitor(AnimalVisitor):
    def catVisit(self, element):
        print(f"cat, {element.name}")

    def dogVisit(self, element):
        print(f"dog, {element.name}")


class Animal:
    def __init__(self, name: str):
        self.name = name

    def accept(self, visitor: AnimalVisitor):
        pass


class Cat(Animal):
    def accept(self, visitor: AnimalVisitor):
        visitor.catVisit(self)


class Dog(Animal):
    def accept(self, visitor: AnimalVisitor):
        visitor.dogVisit(self)


baduk = Dog('baduk')
kitty = Cat('kitty')

baduk.accept(NameVisitor())
kitty.accept(NameVisitor())

baduk.accept(SpeakVisitor())
kitty.accept(SpeakVisitor())
```
 
## 출력 결과
> ![image](https://user-images.githubusercontent.com/96826443/170626132-95bf708e-6d48-486e-925f-dbe49cdddba2.png)

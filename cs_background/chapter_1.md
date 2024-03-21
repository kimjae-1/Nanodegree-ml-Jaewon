# 디자인 패턴
프로그램을 설계할 때 발생했던 문제점들을 객체 간의 상호 관계 등을 이용하여 해결할 수 있도록 하나의 '규약'형태로 만들어 놓은 것

## 싱글톤 패턴(singleton pattern)
하나의 클래스에 오직 하나의 인스턴스만을 가지는 패턴
=> 해당 클래스를 사용하여 여러 번 객체를 생성해도 실제로는 하나의 객체만이 존재함.
=> 여러 부분에서 동일한 데이터베이스 연결을 공유해야 할 때가 있습니다. 데이터베이스 연결을 매번 새로운 연결로 만드는 것이 아니라, 하나의 연결을 유지하고 여러 곳에서 공유
코드 예시
~~~
class Singleton:
    _instance = None
    
    @staticmethod
    def get_instance():
        if Singleton._instance is None:
            Singleton._instance = Singleton()
        return Singleton._instance

 # 싱글톤 인스턴스 생성
singleton_instance1 = Singleton.get_instance()
singleton_instance2 = Singleton.get_instance()

print(singleton_instance1 is singleton_instance2)  # True
~~~


**단점**
독립적인 인스턴스를 생성하기 어려움
=>의존성 주입(DI, Dependency Injection)을 통해 모듈 간의 결합을 느슨하게 만들어 문제를 해결(의존성 혹은 종속성)
=>의존성이 떨어진다(디커플링이 된다)

## 팩토리 패턴(factory pattern)
객체를 사용하는 코ㅡ에서 객체 생성 부분을 떼어내 추상화한 패턴이자 상속 관계에 있는 두 클래스에서 상위 클래스가 중요한 뼈대를 결정하고, 하위 클래스에서 객체 생성에 관한 구체적인 내용을 결정하는 패턴

e.g. 
하위 클래스 : 라떼 레시피, 아메리카노 레시피
상위 클래스 : 바리스타 공장에서 위의 레시피를 토대로 음료를 만드는 생산 공정

 ~~~
class Vehicle:
    def move(self):
        pass

class Car(Vehicle):
    def move(self):
        print("Car is moving")

class Bicycle(Vehicle):
    def move(self):
        print("Bicycle is moving")

class VehicleFactory:
    def create_vehicle(self, vehicle_type):
        if vehicle_type == 'car':
            return Car()
        elif vehicle_type == 'bicycle':
            return Bicycle()
        else:
            raise ValueError("Invalid vehicle type")

 # 팩토리 인스턴스 생성
factory = VehicleFactory()

 # 차량 생성
car = factory.create_vehicle('car')
bicycle = factory.create_vehicle('bicycle')

 # 차량 이동
car.move()      # 출력: Car is moving
bicycle.move()  # 출력: Bicycle is moving

 ~~~

 ## 전략 패턴(strategy pattern)
 객체의 행위를 바꾸고 싶은 경우 '직접' 수정하지 않고 전략이라고 부르는 '캡슐화한 알고리즘'을 컨텍스트 안에서 바꿔주면서 상호 교체가 가능하게 만드는 패턴

e.g. 결제 수단으로 현대카드, 신한카드(전략만 바꿔서 두 가지 방식으로 결제하는 것)

## 옵저버 패턴(observer pattern)
주체가 어떤 객체의 상태 변화를 관찰하다가 상태 변화가 있을 때마다 메서드 등을 통해 옵저버 목록에 있는 옵저버들에게 변화를 알려주는 디자인 패턴
주체 : 객체의 상태 변화를 보고 있는 관찰자
옵저버 : 이 객체의 상태 변화에 따라 전달되는 메서드 등을 기반으로 '추가 변화 사항'이 생기는 객체

e.g. 트위터

## 프록시 패턴과 프록시 서버
프록시 패턴 : 대상 객체에 접근하기 전 그 접근에 대한 흐름을 가로채 해당 접근을 필터링하거나 수정하는 등의 역할을 하는 계층이 존재
=>객체의 속성, 변환 등을 보완하며 보안, 데이터 검증, 캐싱, 로깅에 사용

프록시 서버 : 서버와 클라이언트 사이에서 클라이언트가 자신을 통해 다른 네트워크 서비스에 간접적으로 접속할 수 있게 해주는 컴퓨터 시스템이나 응용 프로그램
e.g. nginx. 익명 사용자가 직접적으로 서버에 접근하는 것을 차단하고, 간접적으로 한 단계를 더 거치게 만들어 보안을 강화할 수 있음.
e.g. cloudflare. 웹 서버 앞단에 프록시 서버로 두어 DDOS 공격 방어나 HTTPS 구축에 사용됨.

## 이터레이터 패턴
이터레이터를 사용하여 컬렉션의 요소들에 접근하는 패턴
각 책을 하나씩 꺼내어 읽으려면 책장을 한 번씩 넘기면서 책을 찾아야하는 상황. 여기서 책장은 컬렉션, 책장을 넘기면서 책을 하나씩 꺼내는 행위는 이터레이터 패턴이라 비유할 수 있음.
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
=>의존성이 떨어진다 == 디커플링이 된다

## 팩토리 패턴(factory pattern)


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
# Chapter 3: Resource Management.

---

### Item 13. Use objects to manage resources.

- 자원 누출을 막기 위해, 생성자에서 자원을 획득하고 소멸자에서 해제하는 RAII객체를 사용합시다.
- 일반적으로 널리 쓰이는 RAII Class는 tr1::shared_ptr과 auto_ptr입니다. 복사될 때 행동이 더 직관적 이기 때문에 tr1::shared_ptr이 더 좋습니다. auto_ptr은 null로 만들어 버립니다.

### Item 14. Think carefully about copying behavior in resource-managing classes.

- ROII 객체의 복사는 그 객체가 관리하는 자원의 복사 문제를 안고 가기 때문에, 그 자원을 어떻게 복사하느냐에 따라 RAII객체의 복사 동작이 결정됩니다.
- RAII 클래스에 구현하는 일반적인 복사 동작은 복사를 금지하거나, 참조 카운팅을 해 누는 선으로 마무리하는 것입니다, 하지만 이 외의 방법도 가능하니 참고해 둡시다.
- RAII 객체가 복사될 때 이루어져야 할 동작 들 중 하나
    - 복사를 금지합니다.
    - 관리하고 있는 자원에 대한 참조 카운팅을 수행합니다.(shared_ptr)
    - 관리하고 있는 자원을 진짜로 복사합니다.
    - 관리하고 있는 자원의 소유권을 옮김니다.(auto_ptr)

### Item 15. Provide access to raw resources in resource-managing classes.

- 실제 자원을 직접 접근해야 하는 기존 API들도 많기 때문에, RAII클래스를 만들 때는 그 클래스가 관리하는 자원을 얻을 수 있는 방법을 열어 주어야 합니다.
- 자원 접근은 명시적 변환 혹은 암시적 변환을 통해 가능합니다. 안전성만 따지면 명시적 변환이 대체적으로 더 낫지만 고객 편의성을 놓고 보면 암시적 변환이 괜찮습니다.

### Item 16. Use the same form in corresponding uses of new and delete.

- new 표현식에 []를 썼으면, 대응되는 delete 표현식에도 []를 써야 합니다. 마찬가지로 new 표현식에 []를 안 썼으면, 대응되는 delete 표현식에도 []를 쓰지 말아야 합니다.

### Item 17. Store newed objects in smart pointers in standalone statements.

- new로 생성한 객체를 스마트 포인터로 넣는 코드는 별도의 한 문장으로 만듭시다. 이것이 안 되어 있으면, 예외가 발생될 때 디버깅하기 힘든 자원 누출이 초래될 수 있습니다.

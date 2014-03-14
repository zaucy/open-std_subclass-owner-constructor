## Description
A subclass is defined when it's constructor or destructor is declared in a class scope which is not it's own.

```c++
class Object {
public:
  
  int num;
  
  class SubObject {
  public:
    void numPlusOne();
  };
  
  // SubObject's constructor is declared in Object's body making SubObject a subclass owned by Object.
  SubObject() = default;
  ~SubObject() = default;
  
  // subObj can be declared like this and be constructed implicitly.
  SubObject subObj;
};

```

Subclass's have access to their owner's scope. Syntax discussion at issue #1.

```c++

void Object::SubObject::numPlusOne() {
  Object::num += 1;
}

```

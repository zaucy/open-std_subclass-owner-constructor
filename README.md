## Examples

```c++
class Object {
public:
  Object();
  
  void recieveMessage(int);
  
  class SubObject {
  public:
    void giveOwnerMessage();
  };
  
  // SubObject's constructor in Object's body makes it an "owned" subclass.
  SubObject() = default;
  
  // subObj can be declared like this and be constructed implicitly.
  SubObject subObj;
};

void Object::SubObject::giveOwnerMessage() {
  // Call owner function as so
  Object::recieveMessage(10);
  
  // These won't work
  // recieveMessage(10);
  // this->recieveMessage(10);
}

// ...

Object obj;
obj.subObj.giveOwnerMessage();


// This is an error. SubObject's can't live outside their owner's scope.
Object::SubObject subObj = obj.SubObject();

// Pointers and references to subObject's are OK.
Object::SubObject* subObjPtr = &obj.subObj;

```

## Virtual Sub Class

```c++
class BaseObject {
public:
  
  class SubObject {
  public:
    void doSomething();
  };
  
  // Virtual SubObject constructor
  virtual SubObject();
  
  SubObject subObk;
};

BaseObject::SubObject() {
  /* ... */
}

class DerivedObject {
public:
  
  // Optionally define SubObject deriving from BaseObject::SubObject
  // to give the virtual object new members.
  class SubObject
    : public BaseObject::SubObject {
  public:
    void doSomethingCool();
  };
  
  // Optionally define new SubObject constructor.
  SubObject() override;
  
  //BaseObject::subObj gets constructed with DerivedObject::SubObject constructor
  // it also gets DerivedObject::SubObject members.
};

DerivedObject::SubObject()
  /*: BaseObject::SubObject::SubObject() <-- this is implicit like usual with constructors*/ {
  
  /* ... */
}

```

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
  recieveMessage(10);
  
  // This won't work
  // this->recieveMessage(10);
}

// ...

Object obj;
obj.subObj.giveOwnerMessage();

// Sub classes can also be creating by calling the sub class's constructor
// from the parent class.
SubObject subObj = obj.SubObject{};
subObj.giveOwnerMessage();
```

Another idea rather than having the owner's member's inside the sub class's scope is to access them with their type name. So instead of doing `recieveMessage(10);` in the above example you'd type `Object::recieveMessage(10);`. Only issue I see with that is the ambiguity with static functions. That, however could probably be solved with `static_cast`.

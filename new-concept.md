# Native look and feels

## Current
```ts
@ENTRY()
class Program {
  static main() {
    @UCLASS()
    class MyUObject extends UObject {
      ctor() {
        this.Prop = 'Good'
      }

      properties() {
        this.Prop/*EditAnyWhere+string*/;
      }
    }
    const o = new MyUObject()
  }
}
```

## Concept

### with Type specifier
```ts
import { ENTRY, Type } from 'ue4'
import { UCLASS } from 'ue4/classes'
import { UPROPERTY, EditAnywhere } from 'ue4/properties'

@ENTRY()
class Program {
  static main() {
    @UCLASS()
    class MyUObject extends UObject {
      @UPROPERTY(EditAnywhere)
      @Type('string')
      prop: string = 'Good'
    }
    
    const o = new MyUObject()
  }
}
```


# Type specifier

## source
```ts
// from: https://github.com/ncsoft/Unreal.js/wiki/Subclassing#wiki-body
class MyActor extends Actor {
  ReceiveBeginPlay() {
    super.ReceiveBeginPlay()
    console.log("Hello")
  }

  @NetMulticast()
  Client_PlayFX(@Type('string') effect) {
    console.log("fire!")
  }
}
```

## translated

```js
class MyActor extends Actor {
  ReceiveBeginPlay() {
    super.ReceiveBeginPlay()
    console.log("Hello")
  }

  Client_PlayFX(effect/*string*/) /*NetMulticast*/ {
    console.log("fire!")
  }
}
```

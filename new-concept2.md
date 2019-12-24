# write via ts
```ts
import { ENTRY } from '../lib/ue4'
import { UCLASS } from "../lib/class/uclass";
import { UFUNCTION } from '../lib/function/ufunction';

@ENTRY()
// @ts-ignore
class Program {
  static main() {
    @UCLASS()
    class MyActor extends StaticMeshActor {
      @UFUNCTION(Server, Reliable)
      test1(arg: int): int {
        console.log('testing... => ' + arg)

        return 1
      }

      @UFUNCTION(Server, Reliable)
      test2(arg: float): string {
        console.log('testing 2...' + arg)

        return 'hello'
      }
    }

    const actor = new MyActor(GWorld, { x: 0, y: 0 } as any)
  }
}
```
# converted
```ts
// example
function main() {
  class MyActor extends StaticMeshActor {
    test1(arg/*int*/) /*Server+Reliable+int*/ { // just example don't care
      console.log('testing... => ' + arg)

      return 1
    }

    test2(arg/*float*/) /*Server+Reliable+string*/ {
      console.log('testing 2...' + arg)

      return 'hello'
    }
  }

  const actor = new MyActor(GWorld, { x: 0, y: 0 } as any)
}

try {
  module.exports = () => {
    let cleanup: any = null

    process.nextTick(() => cleanup = main())

    return () => cleanup()
  }
} catch (ex) {
  const bootstrap = require('./bootstrap')
  bootstrap('dist/app.js')
}

```

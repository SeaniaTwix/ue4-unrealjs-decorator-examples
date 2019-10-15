# ue4-unrealjs-decorator-examples

## library file

```ts
// ue4.ts
export function UCLASS() {
  return (target: any) => {
    const uclass = require('./uclass')().bind(global, target)
    target = uclass(target)
    return target
  }
}

export function ENTRY() {
  return (target) => {
    try {
      module.exports = () => {
        let cleanup: any = null

        process.nextTick(() => cleanup = target.main())

        return () => cleanup()
      }
    } catch (ex) {
      const bootstrap = require('./bootstrap')
      bootstrap('dist/app.js')
    }
  }
}
```

## entry point

```ts
import { UCLASS, ENTRY } from 'ue4'

@ENTRY()
class Program { // set name feel free
  static main() { // *must* follow this name
    @UCLASS()
    class MyActor extends StaticMeshActor {
      
    }
    
    const actor = new MyActor(GWorld, { x: 0, y: 0 } as any)
  }
}
```


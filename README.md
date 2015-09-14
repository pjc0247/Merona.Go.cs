Merona.Go.cs
====
공사중<br><Br>

Source
----
__Merona.Go__의 서버 모듈 소스는 [이곳](https://github.com/pjc0247/Merona.cs/tree/master/src)에서 Merona의 코어 프로젝트와 같이 배포됩니다.<br>
클라이언트 모듈은 현제 레포지토리에서 배포됩니다.

DAT
----
__Merona.Go__는 서버 프로그래머가 아닌 클라이언트 프로그래머에게 친숙한 인터페이스를 제공하기 위한 확장입니다.<br>
클라이언트의 게임 오브젝트와 1:1 매칭되는 서버 오브젝트 개념이 제공되며, 서버-클라이언트간의 쉬운 동기화를 위해 클라이언트용 라이브러리 또한 제공됩니다.

* __Unity3D__
```c#
using Merona.Go.Unity3d;

class Player : MonoBehaviour {
  void Awake() {
    Meronaize(this);
  }
}
```

* __cocos2d-x__
```cpp
#include <merona_go.h>

using merona::go::cocos2d_x;

class Player : CCLayer {
  bool initialize() {
    /* ... */
    meronarize(this);
    /* ...*/
  }
};
```

* __MeronaServer__
```c#
class Player : ServerObject {
  // 아래의 이벤트는 자동 동기화됩니다.
  public void OnMouseDown(Point pt) {
  }
  public void OnKeyboardDown(Key key) {
    // 아래 움직임은 자동으로 동기화됩니다.
    this.x += 1;
  }
  
  // (필요하다면) update 메소드를 구현해 서버 프레임마다
  // 호출 받을 수 있습니다.
  public void Update(float dt) {
  }
}
```


Meronarize Configs
----
Merona 서버와 Merona.Go 간에 자동으로 동기화되는 데이터는 모두 네트워크 자원이며, 효율적인 사용을 위해 선택적인 기능만 켜고 끌 수 있습니다.

* __Inputs__
  * mouse
  * keyboard
* __Position__
* __Instance Vars__

AutoSync Handler
----
각 게임 혹은 엔진마다 좌표 체계 등 자동 동기화되는 값의 단위는 다를 수 있으며, 이를 위해 자동 동기화 단계에 훅으로 끼어들어 처리할 수 있는 메소드를 제공합니다.

# **DLL (동적 링크 라이브러리)**

## 작성자
[![tdm1223](https://avatars1.githubusercontent.com/u/21440957?s=100&v=4)](https://github.com/tdm1223)

## DLL(동동적 링크 라이브러리) ?
- 함수 및 리소스의 공유 라이브러리로 사용되는 **실행 파일**이다.
- 동적 연결을 사용하면 실행 파일이 함수를 호출하거나 별도 파일에 저장된 리소스를 사용할 수 있다.
- 사용하는 실행 파일과 별도로 컴파일 및 배포할 수 있다.
- DLL은 독립 실행형 실행 파일이 아니다.
  - DLL을 호출하는 애플리케이션의 컨텍스트에서 실행된다.
- 운영 체제는 DLL을 애플리케이션의 메모리 공간에 로드한다.
  - 애플리케이션이 로드될 때(암시적) 또는 런타임에 요청시(명시적) 수행된다.
- DLL을 통해 실행 파일 간에 함수 및 리소스를 쉽게 공유할 수 있다.
- 여러 개의 애플리케이션이 메모리에 있는 하나의 DLL 복사본 내용을 동시에 액세스할 수 있다.

## 동적 링크와 정적 링크의 차이점
- 정적 링크는 정적 라이브러리의 모든 개체 코드를 빌드될 때 이 코드를 사용하는 **실행 파일에 복사**한다.
- 동적 연결에는 윈도우가 런타임에 데이터 항목이나 함수를 포함하는 DLL을 찾아서 로드하는 데 필요한 정보만 포함된다.
- DLL을 호출하는 실행 파일을 빌드하는 경우 링커는 가져오기 라이브러리의 내보낸 기호를 사용하여 윈도우의 로더를 위해 이 정보를 저장한다.
- 로더가 DLL을 로드하면 DLL이 애플리케이션의 메모리 공간에 매핑된다.
  - DLL에 특수 함수 DllMain이 있는 경우 이 함수는 DLL에 필요한 초기화를 수행하기 위해 호출된다.

## 애플리케이션과 DLL의 차이점
### 애플리케이션
- 애플리케이션은 실행할 수 있다.
- 애플리케이션에는 시스템에서 동시에 실행되는 자신의 인스턴스가 여러 개 있을 수 있다.
- 애플리케이션은 프로세스로 로드할 수 있고 스택, 실행 스레드, 전역 메모리, 파일 핸들 및 메시지 큐와 같은 작업을 소유할 수 있다.

### DLL
- DLL은 실행할 수 없다.
- DLL에는 하나의 인스턴스만 있을 수 있다.
- DLL은 작업을 소유할 수 없다.

## DLL 사용 시 좋은점
- 메모리가 절약되고 swapping이 감소한다.
- 여러 프로세스에서 DLL을 동시에 사용하여 메모리에서 DLL의 읽기 전용 부분에 대한 단일 복사본을 공유할 수 있다.
  - 정적으로 연결된 라이브러리를 사용하여 빌드된 모든 애플리케이션에는 윈도우에서 메모리로 로드해야 하는 라이브러리 **코드의 전체 복사본**이 있다.
- 동적 링크을 사용하면 디스크 공간 및 대역폭이 절약된다.
- 여러 애플리케이션이 디스크에 있는 DLL의 단일 복사본을 공유할 수 있다. 
  - 정적 링크 라이브러리를 사용하여 빌드된 각 애플리케이션에는 실행 가능 이미지로 연결된 라이브러리 코드가 있다.
  - 이 코드는 더 많은 디스크 공간을 사용하고 전송될 때 더 많은 대역폭을 사용한다.
- 유지 관리, 보안 수정, 업그레이드를 쉽게 수행할 수 있다.
  - 애플리케이션에서 DLL의 일반 함수를 사용하는 경우 버그 수정 후 DLL에 업데이트를 배포할 수 있다.
  - DLL이 업데이트되었다면 이 DLL을 사용하는 애플리케이션을 다시 컴파일하거나 연결할 필요가 없다.
  - 애플리케이션은 DLL이 배포되자마자 사용할 수 있다. 
  - 정적으로 연결된 개체 코드에서 수정하는 경우 이를 사용하는 모든 애플리케이션을 다시 연결하고 배포해야 한다.
- 출시 후 지원을 제공할 수 있다.
  - 애플리케이션이 배송되었을 때는 사용할 수 없었던 디스플레이를 지원하도록 디스플레이 드라이버 DLL을 수정할 수 있다.
- 명시적 링크를 사용하여 런타임에 DLL을 검색하고 로드할 수 있다.
  - 앱을 다시 빌드하거나 배포하지 않고 새 기능을 앱에 추가하는 애플리케이션 확장을 예로 들 수 있다.
- 다양한 프로그래밍 언어로 작성된 애플리케이션을 쉽게 지원할 수 있다.
- 애플리케이션의 글로벌 버전을 더 쉽게 만들 수 있다.
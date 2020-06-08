---
lab:
    title: '랩: Azure Functions를 사용하여 작업 처리 논리 구현'
    module: '모듈 02: Azure Functions 구현'
    type: 'Answer Key'
---

# 랩: Azure Functions를 사용한 작업 처리 논리 구현
# 학생 랩 Answer Key

## Microsoft Azure 사용자 인터페이스

Microsoft 클라우드 도구의 동적 특성을 감안할 때, 이 교육 콘텐츠를 개발한 후 Azure UI가 변경될 수 있습니다. 이러한 변경 사항으로 랩 지침 및 랩 단계가 서로 일치하지 않을 수 있습니다.

Microsoft는 커뮤니티가 필요한 변경 사항을 제공하면 이 교육 과정을 업데이트합니다. 그러나 클라우드 업데이트가 자주 발생하기 때문에 이 교육 콘텐츠가 업데이트되기 전에 UI가 먼저 변경될 수 있습니다. **이 경우 변경 사항에 적응하고 필요에 따라 랩에서 작업합니다.**

## 지침

### 시작하기 전에

#### 랩 가상 머신에 로그인

다음 자격 증명을 사용하여 Windows 10 VM(가상 머신)에 로그인합니다.
    
-   사용자 이름: **관리자**

-   암호: **Pa55w.rd**

> **참고**: 강사가 가상 랩 환경 연결에 대한 지침을 제공합니다.

#### 설치된 응용 프로그램 리뷰

Windows 10 데스크톱에서 작업 표시줄을 찾습니다. 작업 표시줄에는 이 랩에서 사용할 애플리케이션에 대한 아이콘이 포함되어 있습니다.
    
-   Microsoft Edge

-   File Explorer

-   Windows Terminal

### 연습 1: Azure 리소스 만들기

#### 작업 1: Azure Portal 열기

1.  작업 표시줄에서 **Microsoft Edge** 아이콘을 선택합니다.

1.  열려 있는 브라우저 창에서 Azure Portal(<https://portal.azure.com>)로 이동합니다.

1.  Microsoft 계정의 이메일 주소를 입력한 다음 **다음** 을 선택합니다.

1.  Microsoft 계정의 암호를 입력한 다음 **로그인** 을 선택합니다.

    > **참고**: Azure Portal에 처음 로그인하는 경우 포털 둘러보기가 제공됩니다. 둘러보기를 건너뛰고 포털을 사용하려면 **시작하기** 를 선택합니다.

#### 작업 2: Azure Storage 계정 만들기

1.  Azure Portal 탐색 창에서 **모든 서비스** 를 선택합니다.

1.  **모든 서비스** 블레이드에서 **스토리지 계정** 을 선택합니다.

1.  **스토리지 계정** 블레이드에서 스토리지 계정 인스턴스 목록을 가져옵니다.

1.  **스토리지 계정** 블레이드에서 **추가** 를 선택합니다.

1.  **스토리지 계정 만들기** 블레이드에서 **기본**, **태그** 및 **검토 + 만들기** 와 같은 블레이드의 탭을 관찰합니다.

    > **참고**: 각 탭은 새 스토리지 계정을 만드는 워크플로의 단계를 나타냅니다. 언제든지 **검토 + 만들기** 를 선택하여 나머지 탭을 건너뛸 수 있습니다.

1.  **기본** 탭을 선택하고 탭 영역 내에서 다음 작업을 수행합니다.
    
    1.  **구독** 텍스트 상자를 기본값으로 설정합니다.
    
    1.  **리소스 그룹** 섹션에서 **새로 만들기** 를 선택하고 **Serverless** 를 입력한 다음 **확인** 을 선택합니다.
    
    1.  **스토리지 계정 이름** 텍스트 상자에 **funcstor*[yourname]*** 을 입력합니다.
    
    1.  **위치** 목록에서 **(US) 미국 동부** 지역을 선택합니다.
    
    1.  **성능** 섹션에서 **표준** 을 선택합니다.
    
    1.  **계정 종류** 목록에서 **StorageV2(범용 v2)** 를 선택합니다.
    
    1.  **복제** 목록에서 **LRS(로컬 중복 스토리지)** 를 선택합니다.
    
    1.  **액세스 계층(기본값)** 섹션에서 **핫** 이  선택되어 있는지 확인합니다.
    
    1.  **리뷰 + 만들기** 를 선택합니다.

1.  **검토+ 만들기** 탭에서 이전 단계에서 지정한 옵션을 검토합니다.

1.  지정된 구성을 사용하여 스토리지 계정을 만들려면 **만들기** 를 선택합니다.

    > **참고**: 이 랩을 진행하기 전에 **배포** 블레이드에서 만들기 작업이 완료될 때까지 기다립니다.

#### 작업 3: Azure Functions 앱 만들기

1.  Azure Portal의 탐색창에서 **리소스 만들기** 링크를 선택합니다.

1.  **새로 만들기** 블레이드에서 **Marketplace 검색** 텍스트 상자를 찾습니다.

1.  검색 상자에서 **함수** 를 입력한 다음 엔터를 선택합니다.

1.  **모든** 검색 결과 블레이드에서 **함수 앱** 결과를 선택합니다.

1.  **함수 앱** 블레이드에서 **만들기** 를 선택합니다.

1.  **기본** 과 같은 **함수 앱** 블레이드의 탭을 찾습니다.

    > **참고**: 각 탭은 새 함수 앱을 만드는 워크플로의 단계를 나타냅니다. 언제든지 **검토 + 만들기** 를 선택하여 나머지 탭을 건너뛸 수 있습니다.

1.  **기본** 탭에서 다음작업을 수행합니다.
    
    1.  **구독** 텍스트 박스를 기본값으로 설정된 상태로 둡니다.
    
    1.  **리소스 그룹** 섹션에서 **기존 사용** 을 선택한 다음 목록에서 **Serverless** 를 선택합니다.
    
    1.  **함수 앱 이름** 텍스트 상자에 **funclogic*[yourname]*** 을 입력합니다.

    1.  **게시** 섹션에서 **코드** 를 선택합니다.

    1.  **런타임 스택** 드롭다운 목록에서 **NET Core** 를 선택합니다.

    1.  **지역** 드롭다운 목록에서 **East US** 지역을 선택합니다.
    
    1.  **다음: 호스팅** 을 선택합니다.

1.  **호스팅** 탭에서 다음 작업을 수행합니다.

    1.  **스토리지 계정** 드롭다운 목록에서, 이 랩의 앞에서 만든 **funcstor*[yourname]*** 스토리지 계정을 선택합니다.

    1.  **운영 체제** 섹션에서 **Windows** 를 선택합니다.

    1.  **플랜 유형** 드롭다운 목록에서 **사용량(서버리스)** 옵션을 선택합니다.

    1.  **다음: 모니터링** 을 선택합니다.을 선택합니다.

1.  **모니터링** 탭에서 다음 작업을 수행합니다.

    1.  **Application Insights 사용** 섹션에서 **** 를 선택합니다.

    1.  **검토 + 만들기** 를 선택합니다.

1.  **검토 + 만들기** 탭에서 이전 단계에서 선택한 옵션을 검토합니다.

1.  지정된 구성을 사용하여 함수 앱을 만들려면 **만들기** 를 선택합니다. 

    > **참고**: 이 랩을 진행하기 전에 만들기 작업이 완료될 때까지 기다립니다.

#### 리뷰

이 연습에서는 이 랩에 사용할 모든 리소스를 만들었습니다.

### 연습 2: HTTP 요청에 의해 트리거되는 함수 만들기

#### 작업 1: HTTP 트리거 함수 만들기

1.  Azure Portal의 탐색 창에서 **리소스 그룹** 링크를 선택합니다.

1.  **리소스 그룹** 블레이드에서, 이 랩의 앞에서 만든 **Serverless** 리소스 그룹을 찾아 선택합니다.

1.  **Serverless** 블레이드에서 이 랩의 앞에서 만든 **funclogic*[yourname]*** 함수 앱을 선택합니다.

1.  **함수 앱** 블레이드에서 **함수**메뉴 아래 **함수** 에서 **추가** 를 선택합니다.

1.  **새 함수** 빠른 시작에서 다음 작업을 수행합니다.
    
    1.  템플릿 목록에서 **HTTP 트리거** 를 선택합니다.
    
    1.  **새 함수** 팝업 창에서 **새 함수** 텍스트 상자를 찾아 **Echo** 를 입력합니다.
    
    1.  **새 함수** 팝업 창에서 **Authorization level** 목록을 찾아 **Anonymous** 을 선택합니다.
    
    1.  **새 함수** 팝업 창에서 **함수 만들기** 를 선택합니다.

#### 작업 2: 함수 코드 작성

1.  **코드+테스트**에서 function[yourname]\Echo\**run.csx** 함수 스크립트를 찾습니다.

```
    #r "Newtonsoft.Json"

    using System.Net;
    using Microsoft.AspNetCore.Mvc;
    using Microsoft.Extensions.Primitives;
    using Newtonsoft.Json;

    public static async Task<IActionResult> Run(HttpRequest req, ILogger log)
    {
        log.LogInformation("C# HTTP 트리거 함수가 요청을 처리하였습니다.");

        string name = req.Query["name"];

        string requestBody = await new StreamReader(req.Body).ReadToEndAsync();
        dynamic data = JsonConvert.DeserializeObject(requestBody);
        name = name ?? data?.name;

        return name != null
            ? (ActionResult)new OkObjectResult($"Hello, {name}")
            : new BadRequestObjectResult("Please pass a name on the query string or in the request body");
    }
```

1.  예시 코드를 모두 삭제합니다.

1.  다음 코드 줄을 추가하여 **Microsoft.AspNetCore.Mvc** 네임스페이스를 가져옵니다.

```
    using Microsoft.AspNetCore.Mvc;
```

1.  다음 코드 줄을 추가하여 **System.Net** 네임스페이스를 가져옵니다.

```
    using System.Net;
```

1.  다음 코드 블록을 추가하여 **IActionResult** 형식의 변수를 반환하고 **HttpRequest** 및 **ILogger** 형식의 변수를 *req* 및 *log* 라는 매개 변수로 사용하는 **Run** 이 라는 새 **public static** 메서드를 만듭니다.

```
    public static IActionResult Run(HttpRequest req, ILogger log)
    {
    }
```

1.  **Run** 메서드에서 다음 코드 줄을 입력하여 고정 메시지를 렌더링합니다.

```
    log.LogInformation("Received a request");
```

1.  HTTP 요청의 본문을 HTTP 응답으로 에코하는 다음 코드 줄을 입력합니다.

```
    return new OkObjectResult(req.Body);
```

1.  이제 다음을 포함해야 하는 **run.csx** 파일을 확인합니다.

```
    using System.Net;
    using Microsoft.AspNetCore.Mvc;

    public static IActionResult Run(HttpRequest req, ILogger log)
    {
        log.LogInformation("Received a request");

        return new OkObjectResult(req.Body);
    }
```

1.  스크립트를 저장하려면 **저장** 을 선택합니다.

#### 작업 3: 포털에서 함수 실행 테스트

1. 화면창 아래 **로그** 를 선택합니다.

1. 다음 테스트 실행 후 결과를 관찰합니다. 결과는 원래 요청 본문을 정확하게 반복해야 합니다.

#### 작업 4: 기본 함수 URL 가져오기

1.  Azure Portal의 탐색 창에서 **리소스 그룹** 링크를 선택합니다.

1.  **리소스 그룹** 블레이드에서, 이 랩의 앞에서 만든 **Serverless** 리소스 그룹을 찾아 선택합니다.

1.  **Serverless** 블레이드에서 이 랩의 앞에서 만든 **funclogic*[yourname]*** 함수 앱을 선택합니다.

1.  **함수 앱** 블레이드에서 Echo|코드+테스트에서 **함수 URL 가져오기**의 **URL** 값을 복사합니다. 이 값은 랩에서 나중에 사용합니다.

#### 작업 5: httprepl을 사용하여 함수 실행 테스트

1.  작업 표시줄에서 **Windows Terminal** 아이콘을 선택합니다.(Command로 대체 가능)

1.  열린 명령 프롬프트에서 다음 명령을 입력한 다음 Enter 키를 선택하여 기본 URI(Uniform Resource Identifier)를 이 랩의 앞에서 복사한 URL 값으로 설정하는 **httprepl** 도구를 시작합니다.(**httprepl 설치** https://docs.microsoft.com/ko-kr/aspnet/core/web-api/http-repl?view=aspnetcore-3.1&tabs=windows)

```
    httprepl <function-app-url>
```

    > **참고**: 예를 들어 URL이 **https://funclogicstudent.azurewebsites.net** 인 경우 명령은 **httprepl https://funclogicstudent.azurewebsites.net** 이  됩니다.

1.  도구 프롬프트에서 다음 명령을 입력한 다음 Enter 키를 선택하여 상대 **API** 디렉터리를 찾습니다.

```
    cd api
```

1.  다음 명령을 입력한 다음 Enter 키를 선택하여 상대 **echo** 디렉터리를 찾습니다.

```
    cd echo
```

1.  다음 명령을 입력한 다음 Enter 키를 선택하여 **--content** 옵션을 통해 값이 **3** 으로 설정된 HTTP 요청 본문을 전송하는 **post** 명령을 실행합니다.

```
    post --content 3
```

1.  다음 명령을 입력한 후 Enter 키를 선택하여 다음 **--content** 옵션을 사용하여 숫자 **5** 의 값으로 설정된 HTTP 요청 본문에서 보내는 **게시** 명령을 실행합니다.

```
    post --content 5
```

1.  다음 명령을 입력한 다음 Enter 키를 선택하여 **--content** 옵션을 통해 값이 **Hello** 로 설정된 HTTP 요청 본문을 전송하는 **post** 명령을 실행합니다.

```
    post --content "Hello"
```

1.  다음 명령을 입력한 다음 Enter 키를 선택하고 --content 옵션을 사용하여 **{"msg": "Successful"}** 의 JSON(JavaScript Object Notation) 값으로 설정된 HTTP 요청 본문에서 보내는 **post** 명령을 실행합니다.** "Successful"}** **--content** 옵션을 사용하여:

```
    post --content "{"msg": "Successful"}"
```

1.  다음 명령을 입력한 다음, 엔터를 선택하여 **httprepl** 애플리케이션을 종료합니다.

```
    exit
```

1.  현재 실행 중인 Microsoft Terminal 애플리케이션을 닫습니다.

1.	Azure Portal을 사용하여 브라우저 창으로 돌아갑니다.

#### 리뷰

이 연습에서는 HTTP POST 요청을 통해 전송된 콘텐츠를 에코하는 기본 함수를 만들었습니다.

### 연습 3: 일정에 따라 트리거하는 함수 만들기

#### 작업 1: 일정에 따라 트리거되는 함수 만들기

1.  Azure Portal의 탐색 창에서 **리소스 그룹** 링크를 선택합니다.

1.  **리소스 그룹** 블레이드에서, 이 랩의 앞에서 만든 **Serverless** 리소스 그룹을 찾아 선택합니다.

1.  **Serverless** 블레이드에서 이 랩의 앞에서 만든 **funclogic*[yourname]*** 함수 앱을 선택합니다.

1.  **함수 앱** 블레이드에서 **함수**메뉴 아래 **함수** 에서 **추가** 를 선택합니다.

1.  **새 함수** 빠른 시작에서 다음 작업을 수행합니다.
        
    1.  템플릿 목록에서 **타이머 트리거** 를 선택합니다.
    
    1.  **새 함수** 팝업 창에서 **새 함수** 텍스트 상자를 찾아 **Recurring** 을 입력합니다.
    
    1.  **새 함수** 팝업 창에서 **Schedule** 텍스트 상자를 찾아 **0 \* \* \* \* \*** 를 입력합니다.
    
    1.  **새 함수** 팝업 창에서 **만들기** 를 선택합니다.

#### 작업 2: 함수 실행 관찰

1.  **코드+테스트** 에서 화면 아래쪽에 **로그** 를 선택합니다.

1.  1분마다 발생하는 함수 실행을 관찰합니다. 각 함수 실행은 로그에 간단한 메시지를 렌더링해야 합니다.

#### 작업 3: 함수 통합 구성 업데이트

1.  **함수 앱** 블레이드에 돌아와서 다음 작업을 수행합니다.

    1.  이 랩의 앞에서 만든 **funclogic*[yourname]*** 함수 앱에 대한 노드를 펼칩니다.

    1.  **함수** 노드를 펼칩니다.

    1.  **Recurring** 노드를 선택합니다.

    1.  **통합** 노드를 선택합니다.

1.  **통합** 섹션에서 다음 작업을 수행합니다.

    1.  **트리거** 섹션에서 **Timer(myTimer)** 옵션을 선택합니다.

    1.  **Schedule** 텍스트 상자에 **\*/30 \* \* \* \* \*** 값을 입력합니다.

    1.  **저장** 을 선택합니다.

#### 작업 4: 함수 실행 관찰

1.  **함수 앱** 블레이드에 돌아와서 다음 작업을 수행합니다.

    1.  이 랩의 앞에서 만든 **funclogic*[yourname]*** 함수 앱에 대한 노드를 펼칩니다.

    1.  **함수** 노드를 펼칩니다.

    1.  **Recurring** 노드를 선택합니다.

1.  **코드+테스트**에서 화면아래 **로그** 를 선택합니다.

1.  이제 약 30초마다 발생하는 함수 실행을 관찰합니다. 각 함수 실행은 로그에 간단한 메시지를 렌더링해야 합니다.

#### 검토

이 연습에서는 고정된 일정에 따라 자동으로 실행되는 함수를 만들었습니다.

### 연습 4: 다른 서비스와 통합되는 함수 만들기

#### 작업 1: HTTP 트리거 함수 만들기

1.  Azure Portal의 탐색 창에서 **리소스 그룹** 링크를 선택합니다.

1.  **리소스 그룹** 블레이드에서, 이 랩의 앞에서 만든 **Serverless** 리소스 그룹을 찾아 선택합니다.

1.  **Serverless** 블레이드에서 이 랩의 앞에서 만든 **funclogic*[yourname]*** 함수 앱을 선택합니다.

1.  **함수 앱** 블레이드에서 **함수**메뉴 아래 **함수** 에서 **추가** 를 선택합니다.

1.  **새 함수** 빠른 시작에서 다음 작업을 수행합니다.
        
    1.  템플릿 목록에서 **HTTP 트리거** 를 선택합니다.
    
    1.  **새 함수** 팝업 창에서 **새 함수** 텍스트 상자를 찾아 **GetSettingInfo** 를 입력합니다.
    
    1.  **새 함수** 팝업 창에서 **Authorization level** 목록을 찾아 **Anonymous** 을 선택합니다.
    
    1.  **새 함수** 팝업 창에서 **함수 만들기** 를 선택합니다.

#### 작업 2: 샘플 콘텐츠 업로드

1.  Azure Portal의 탐색 창에서 **리소스 그룹** 링크를 선택합니다.

1.  **리소스 그룹** 블레이드에서, 이 랩의 앞에서 만든 **Serverless** 리소스 그룹을 찾아 선택합니다.

1.  **Serverless** 블레이드에서 이 랩의 앞에서 만든 **funcstor*[yourname]*** 스토리지 계정을 선택합니다.

1.  **스토리지 계정** 블레이드에서 **Blob 서비스** 섹션에 있는 **컨테이너** 링크를 선택합니다.

1.  **컨테이너** 섹션에서 **+ 컨테이너** 를 선택합니다.

1.  **새 컨테이너** 팝업 창에서 다음 작업을 수행합니다.
    
    1.  **이 름** 텍스트 상자에 **content** 를 입력합니다.
    
    1.  **공용 액세스 수준** 드롭다운 목록에서 **프라이빗(익명 액세스 없음)** 를 선택합니다.
    
    1.  **확인** 을 선택합니다.

1.  **컨테이너** 섹션으로 돌아가서 새로 만든 **content** 컨테이너를 선택합니다.

1.	**컨테이너** 블레이드에서 **업로드** 를 선택합니다.

1.	**BLOB 업로드** 창에서 다음 작업을 수행합니다.

    1.  **파일** 섹션에서 **폴더** 아이콘을 선택합니다.

    1.  **파일 탐색기** 창에서 **Allfiles (F):\\Allfiles\\Labs\\02\\Starter** 를 찾아 **settings.json** 파일을 선택하고 **열기** 를 선택합니다.

    1.  **파일이 이미 있는 경우 덮어쓰기** 확인란이 선택되어 있는지 확인하고, **업로드** 를 선택합니다. 
    
    > **참고**: 이 랩을 계속하기 전에 Blob이 업로드될 때까지 기다립니다.

#### 작업 3: HTTP 트리거 함수 구성

1.  Azure Portal의 탐색 창에서 **리소스 그룹** 링크를 선택합니다.

1.  **리소스 그룹** 블레이드에서, 이 랩의 앞에서 만든 **Serverless** 리소스 그룹을 찾아 선택합니다.

1.  **Serverless** 블레이드에서 이 랩의 앞에서 만든 **funclogic*[yourname]*** 함수 앱을 선택합니다.

1.  **Function Apps** 블레이드에서 다음 작업을 수행합니다.

    1.  이 랩의 앞에서 만든 **funclogic*[yourname]*** 함수 앱에 대한 노드를 펼칩니다.

    1.  **함수** 노드를 펼칩니다.

    1.  **GetSettingInfo** 노드를 선택한다.

    1.  **통합** 노드를 선택합니다.

1.  **통합** 섹션에서 다음 작업을 수행하여 **Azure Blob Storage** 형식의 새 입력을 만듭니다.

    1.  **입력** 을 선택합니다.

    1.  **Azure Blob Storage** 를 선택합니다.

    1.  **Azure Blob Storage 정보** 섹션에서 다음 작업을 수행합니다.

    1.  **Blob 매개 변수 이름** 텍스트 상자에 **json** 값을 입력합니다.

    1.  **Path** 텍스트 상자에 **content/settings.json** 값을 입력합니다.

    1.  **Storage account connection** 목록에서 **AzureWebJobsStorage** 를 선택합니다.

    1.  **확인** 을 선택합니다.

1.  **통합** 섹션으로 돌아가서 기존 **트리거 HTTP(req)** 를 선택합니다.

1.  **HTTP 트리거** 섹션에서 다음 작업을 수행합니다.

    1.  **바인딩 형식** 목록에서 **선택된 메서드** 를 선택합니다.

    1.  **Request parameter name** 텍스트 상자에 **request** 값을 입력합니다.

    1.  **Selected HTTP methods** 확인란 그룹에서 **GET** 옵션만 선택되어 있는지 확인합니다.

    1.  **저장** 을 선택합니다.

#### 작업 4: 함수 코드 작성

1.  **Function Apps** 블레이드에서 다음 작업을 수행합니다.

    1.  이 랩의 앞에서 만든 **funclogic*[yourname]*** 함수 앱에 대한 노드를 펼칩니다.

    1.  **함수** 노드를 펼칩니다.

    1.  **GetSettingInfo** 노드를 선택합니다.

1.  **코드+테스트**에서 예제 **run.csx** 함수 스크립트를 확인합니다.

```
    #r "Newtonsoft.Json"

    using System.Net;
    using Microsoft.AspNetCore.Mvc;
    using Microsoft.Extensions.Primitives;
    using Newtonsoft.Json;

    public static async Task<IActionResult> Run(HttpRequest req, ILogger log)
    {
        log.LogInformation("C# HTTP trigger function processed a request.");

        string name = req.Query["name"];

        string requestBody = await new StreamReader(req.Body).ReadToEndAsync();
        dynamic data = JsonConvert.DeserializeObject(requestBody);
        name = name ?? data?.name;

        return name != null
            ? (ActionResult)new OkObjectResult($"Hello, {name}")
            : new BadRequestObjectResult("쿼리 문자열이나 요청 본문에 있는 이름을 전달해 주세요.")
    }
```

1.  예시 코드를 모두 **삭제** 합니다.

1.  다음 코드 줄을 추가하여 **Microsoft.AspNetCore.Mvc** 네임스페이스를 가져옵니다.

```
    using Microsoft.AspNetCore.Mvc;
```

1.  다음 코드 줄을 추가하여 **System.Net** 네임스페이스를 가져옵니다.

```
    using System.Net;
```

1.  다음 코드 블록을 추가하여 **Run** 이 라는 새 **공용 정적** 메서드를 만드는데, 이 메서드는 **IActionResult** 형식의 변수를 반환하고 **httpRequest** 및 **스트링** 의 변수를 *요청* 및 *json이라는* 매개 변수로 사용합니다.

```
    public static IActionResult Run(HttpRequest request, string json)
    {
    }
```

1.  **실행** 메서드에서 다음 코드 줄을 입력하여 *json* 매개 변수의 내용을 함수의 HTTP 응답으로 반환합니다.

```
    return new OkObjectResult(json);
```

1.  이제 다음을 포함해야 하는 **run.csx** 파일을 확인합니다.

```
    using Microsoft.AspNetCore.Mvc;
    using System.Net;

    public static IActionResult Run(HttpRequest request, string json)
    {
        return new OkObjectResult(json);
    }
```

1.  스크립트를 저장하려면 **저장** 을 선택합니다.

#### 작업 5: 함수 실행 테스트

1.  작업 표시줄에서 **Windows Terminal** 아이콘을 선택합니다.(Command로 대체 가능)

1.  명령 프롬프트 열기에서 다음 명령을 입력한 다음 Enter 키를 선택하여 기본 URI를 이 랩의 앞에서 복사한 URL 값으로 설정하는 **httprepl** 도구를 시작합니다.

```
    httprepl <function-app-url>
```

    > **참고**: 예를 들어 URL이 **https://funclogicstudent.azurewebsites.net** 인 경우 명령은 **httprepl https://funclogicstudent.azurewebsites.net** 이  됩니다.

1.  도구 프롬프트에서 다음 명령을 입력한 다음 Enter 키를 선택하여 상대 **API** 엔드포인트로 찾아봅니다.

```
    cd api
```

1.  다음 명령을 입력한 다음 Enter 키를 선택하여 상대 **getsettinginfo** 엔드포인트를 찾아봅니다.

```
    cd getsettinginfo
```

1.  다음 명령을 입력한 다음 Enter 키를 선택하여 현재 끝점에 대한 **get** 명령을 실행합니다.

```
    get
```

1.  함수 앱에서 나온 응답의 JSON 콘텐츠를 살펴봅니다. 여기에는 다음이 포함되어야 합니다.

```
    {
        "version": "0.2.4",
        "root": "/usr/libexec/mews_principal/",
        "device": {
            "id": "21e46d2b2b926cba031a23c6919"
        },
        "notifications": {
            "email": "Anais85@outlook.com",
            "phone": "751.757.2014 x4151"
        }
    }
```

1.  다음 명령을 입력한 다음, 엔터를 선택하여 **httprepl** 애플리케이션을 종료합니다.

```
    exit
```

1.  현재 실행 중인 Microsoft Terminal 애플리케이션을 닫습니다.

1.	Azure Portal을 사용하여 브라우저 창으로 돌아갑니다.

#### 리뷰

이 연습에서는 스토리지에서 JSON 파일의 콘텐츠를 반환하는 함수를 만들었습니다.

### 연습 5: 구독 정리 

#### 작업 1: Azure Cloud Shell 열기 및 리소스 그룹 나열

1.  Azure Portal의 탐색 창에서 **Cloud Shell** 아이콘을 선택하여 새 셸 인스턴스를 엽니다.

    > **참고**: **Cloud Shell** 아이콘은 초과(\>) 기호와 밑줄 문자(\_)로 표시됩니다.

1.  구독을 사용하여 Cloud Shell을 처음으로 여는 경우, 처음 사용할 경우에만 **Azure Cloud Shell 시작 마법사** 를 사용하여 Cloud Shell를 구성할 수 있습니다. 마법사에서 다음 작업을 수행합니다.
    
    1.  대화 박스는 셸을 사용하여 시작할 새 스토리지 계정을 만들라는 메시지를 표시합니다. 기본 설정을 수락하고 **스토리지 만들기** 를 선택합니다. 

    > **참고**: 랩으로 진행하기 전에 Cloud Shell이 초기 설치 절차를 완료할 때까지 기다립니다. Cloud Shell의 구성 옵션이 나타나지 않는 경우 이 과정의 랩에서 기존 구독을 사용하고 있기 때문일 가능성이 높습니다. 랩은 새 구독을 사용한다는 가정 하에서 작성됩니다.

1.  포털의 **Cloud Shell** 명령 프롬프트에서 다음 명령을 입력하고 엔터를 선택하여 구독의 모든 리소스 그룹을 나열합니다.

```
    az group list
```

1.  명령 프롬프트에서 다음 명령을 입력하고 Enter 키를 눌러 리소스 그룹을 삭제하는 데 사용할 수 있는 명령 목록을 가져옵니다.

```
    az group delete --help
```

#### 작업 2: 리소스 그룹 삭제

1.  명령 프롬프트에서 다음 명령을 입력하고 Enter 키를 선택해 **서버리스** 리소스 그룹을 삭제합니다.

```
    az group delete --name Serverless --no-wait --yes
```
    
1.  포털에서 Cloud Shell 창을 닫습니다.

#### 작업 3: 활성 애플리케이션 닫기

1.     현재 실행 중인 Microsoft Edge 애플리케이션.

#### 검토

이 연습에서는이 랩에 사용된 리소스 그룹을 제거하여 구독을 정리했습니다.

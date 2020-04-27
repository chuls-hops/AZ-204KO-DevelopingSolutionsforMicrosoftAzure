---
lab:
    title: '랩: 서비스 전반에서 리소스 비밀에 보다 안전하게 액세스'
    module: '모듈 07: 보안 클라우드 솔루션 구현'
    type: '해답'
---

# 랩: 서비스 전반에서 리소스 비밀에 안전하게 액세스
# 학생 랩 답변 키

## Microsoft Azure 사용자 인터페이스

Microsoft 클라우드 도구의 동적 특성을 감안할 때, 이 교육 콘텐츠를 개발한 후 Azure UI가 변경될 수 있습니다. 이러한 변경으로 인해 랩 지침 및 랩 단계가 일치하지 않을 수 있습니다.

Microsoft는 커뮤니티가 필요한 변경 사항을 제공하면 이 교육 과정을 업데이트합니다. 그러나 클라우드 업데이트가 자주 발생하기 때문에 이 교육 콘텐츠가 업데이트되기 전에 UI가 먼저 변경될 수 있습니다. **이 경우 변경 사항에 적응하고 필요에 따라 랩에서 작업합니다.**

## 지침

### 시작하기 전에

#### 랩 가상 머신에 로그인

다음 자격 증명을 사용하여 Windows 10 가상 머신에 로그인합니다.
    
-   사용자 이름: **Admin**

-   암호: **Pa55w.rd**

> **참고**: 강사가 가상 랩 환경 연결에 대한 지침을 제공합니다.

#### 설치된 응용 프로그램 리뷰

Windows 10 데스크톱에서 작업 표시줄을 찾습니다. 작업 표시줄에는 이 랩에서 사용할 애플리케이션에 대한 아이콘이 포함되어 있습니다.
    
-   Microsoft Edge

-   File Explorer

### 연습 1: Azure 리소스 만들기

#### 작업 1: Azure Portal 열기

1.  작업 표시줄에서 **Microsoft Edge** 아이콘을 선택합니다.

1.  열려있는 브라우저 창에서 **Azure Portal**(<https://portal.azure.com>)로 이동합니다.

1.  Microsoft 계정의 이메일 주소를 입력한 다음 **다음**을 선택합니다.

1.  Microsoft 계정의 **암호**를 입력한 다음 **로그인**을 선택합니다.

    > **참고**: Azure Portal에 처음 로그인하는 경우 포털 둘러보기 기능이 제공됩니다. 둘러보기를 건너뛰고 포털 사용을 시작하려면 **시작하기**를 선택합니다.

#### 작업 2: Azure Storage 계정 만들기

1.  Azure Portal 탐색 창에서 **모든 서비스**를 선택합니다.

1.  **모든 서비스** 블레이드에서 **스토리지 계정**을 선택합니다.

1.  **스토리지 계정** 블레이드에서 스토리지 인스턴스 목록을 확인합니다.

1.  **스토리지 계정** 블레이드에서 **추가**를 선택합니다.

1.  **기본**과 같은 **저장소 계정 만들기** 블레이드에서 탭을 찾습니다.

    > **참고**: 각 탭은 새 스토리지 계정을 만드는 워크플로의 단계를 나타냅니다. 언제든지 **검토 + 만들기**를 선택하여 나머지 탭을 건너뛸 수 있습니다.

1.  **기본** 탭에서 다음 작업을 수행합니다.
    
    1.  **구독** 텍스트 상자를 기본값으로 설정합니다.

    1.  **리소스 그룹** 섹션에서 **새로 만들기**를 선택하고 **SecureFunction**을 입력한 다음 **확인**을 선택합니다.

    1.  **스토리지 계정** 이름 텍스트 상자에 **securestor*[yourname]*** 을 입력합니다.

    1.  **위치** 드롭다운 목록에서 **(미국) 미국 동부** 지역을 선택합니다.

    1.  **성능** 섹션에서 **표준**을 선택합니다.

    1.  **계정 종류** 드롭다운 목록에서 **StorageV2(범용 v2)** 를 선택합니다.

    1.  **복제** 드롭다운 목록에서 **LRS(로컬 중복 스토리지)** 를 선택합니다.

    1.  **액세스 계층** 섹션에서 **핫**이 선택되어 있는지 확인합니다.

    1.  **검토 + 만들기**를 선택합니다.

1.  **검토 + 만들기** 탭에서 이전 단계에서 선택한 옵션을 검토합니다.

1.  지정된 구성을 사용하여 스토리지 계정을 만들려면 **만들기**를 선택합니다. 

    > **참고**: 이 랩을 진행하기 전에 만들기 작업이 완료될 때까지 기다립니다.

1.  Azure Portal 탐색 창에서 **모든 서비스**를 선택합니다.

1.  **모든 서비스** 블레이드에서 **스토리지 계정**을 선택합니다.

1.  **스토리지 계정** 블레이드에서 접두사 *securestor\** 가 있는 스토리지 계정 인스턴스를 선택합니다.

1.  **스토리지 계정** 블레이드에서 **설정** 섹션을 찾은 다음 **액세스 키** 링크를 선택합니다.

1.  **액세스 키** 블레이드에서 키 중 하나를 선택하고 **연결 문자열** 박스 중 하나에 값을 기록합니다. 나중에 이 랩에서 이 값을 사용하게 됩니다.

    > **참고**: 어떤 연결 문자열을 선택하든 상관없습니다. 서로 교환 가능합니다.

#### 작업 3: Azure Key Vault 만들기

1.  Azure Portal의 탐색창에서 **리소스 만들기** 링크를 선택합니다.

1.  **새** 블레이드에서 주요 서비스 목록 위의 **마켓플레이스 검색** 텍스트 상자를 찾습니다.

1.  검색 박스에서 **자격 증명 모음**을 입력한 다음 Enter 키를 누릅니다.

1.  **마켓플레이스** 검색 결과 블레이드에서 **Key Vault** 결과를 선택합니다.

1.  **키 자격 증명 모음** 블레이드에서 **만들기**를 선택합니다.

1.  **기본**과 같은 **키 자격 증명 모음 만들기** 블레이드에서 탭을 찾습니다.

    > **참고**: 각 탭은 새 키 자격 증명 모음을 만드는 워크플로의 단계를 나타냅니다. 언제든지 **검토 + 만들기**를 선택하여 나머지 탭을 건너뛸 수 있습니다.

1.  **기본** 탭에서 다음 작업을 수행합니다.
    
    1.  **구독** 텍스트 상자를 기본값으로 설정합니다.
    
    1.  **리소스 그룹** 섹션에서 **기존 사용**을 선택한 다음 목록에서 **SecureFunction**을 선택합니다.
    
    1.  **키 자격 증명 모음 이름** 텍스트 상자에 **securevault*[yourname]*** 을 입력합니다.

    1.  **지역** 드롭다운 목록에서 **미국 동부** 지역을 선택합니다.
        
    1.  **가격 책정 계층** 드롭다운 목록에서 **표준**을 선택합니다.
    
    1.  **검토 + 만들기**를 선택합니다.

1.  **검토 + 만들기** 탭에서 이전 단계에서 선택한 옵션을 검토합니다.

1.  지정된 구성을 사용하여 키 자격 증명 모음을 만들려면 **만들기**를 선택합니다. 

    > **참고**: 이 랩을 진행하기 전에 만들기 작업이 완료될 때까지 기다립니다.

#### 작업 4: Azure Functions 앱 만들기

1.  Azure Portal의 탐색창에서 **리소스 만들기** 링크를 선택합니다.

1.  **새** 블레이드에서 주요 서비스 목록 위의 **마켓플레이스 검색** 텍스트 상자를 찾습니다.

1.  검색 상자에서 **함수**를 입력한 다음 엔터를 선택합니다.

1.  **마켓플레이스** 검색 결과 블레이드에서 **Function App** 결과를 선택합니다.

1.  **Function App** 블레이드에서 **만들기**를 선택합니다.

1.  **기본**과 같은 **Function App** 블레이드에서 탭을 찾습니다.

    > **참고**: 각 탭은 새 함수 앱을 만드는 워크플로의 단계를 나타냅니다. 언제든지 **검토 + 만들기**를 선택하여 나머지 탭을 건너뛸 수 있습니다.

1.  **기본** 탭에서 다음 작업을 수행합니다.
    
    1.  **구독** 텍스트 상자를 기본값으로 설정합니다.
    
    1.  **리소스 그룹** 섹션에서 **기존 사용**을 선택한 다음 목록에서 **SecureFunction**을 선택합니다.
    
    1.  **함수 앱 이름** 텍스트 상자에 **securefunc*[yourname]*** 을 입력합니다.

    1.  **게시** 섹션에서 **코드**를 선택합니다.

    1.  **런타임 스택** 드롭다운 목록에서 **NET Core**를 선택합니다.

    1.  **지역** 드롭다운 목록에서 **미국 동부** 지역을 선택합니다.
    
    1.  **다음**을 선택합니다.** 호스팅**.

1.  **호스팅** 탭에서 다음 작업을 수행합니다.

    1.  **스토리지 계정** 드롭다운 목록에서, 이 랩의 앞에서 만든 **securestor*[yourname]*** 스토리지 계정을 선택합니다.

    1.  **운영 체제** 섹션에서 **Windows**를 선택합니다.

    1.  **플랜 유형** 드롭다운 목록에서 **소비** 옵션을 선택합니다.

    1.  **다음:**을 선택합니다.** 모니터링**.

1.  **모니터링** 탭에서 다음 작업을 수행합니다.

    1.  **Application Insights 사용** 섹션에서 **아니요**를 선택합니다.

    1.  **검토 + 만들기**를 선택합니다.

1.  **검토 + 만들기** 탭에서 이전 단계에서 선택한 옵션을 검토합니다.

1.  지정된 구성을 사용하여 함수 앱을 만들려면 **만들기**를 선택합니다. 

    > **참고**: 이 랩을 진행하기 전에 만들기 작업이 완료될 때까지 기다립니다.

#### 검토

이 연습에서는 이 랩에 사용할 모든 리소스를 만들었습니다.

### 연습 2: 비밀 및 ID 구성 

#### 작업 1: 할당된 시스템 관리 서비스 ID 구성

1.  Azure Portal의 탐색 창에서 **리소스 그룹** 링크를 선택합니다.

1.  **리소스 그룹** 블레이드에서 해당 랩 앞에서 만든 **SecureFunction** 리소스 그룹을 찾아서 선택합니다.

1.  **SecureFunction** 블레이드에서 해당 랩 앞에서 만든 **securefunc*[yourname]*** 함수 앱을 선택합니다.

1.  **함수 앱** 블레이드에서 **플랫폼 기능** 탭을 선택합니다.

1.  **플랫폼 기능** 탭에서 **네트워킹** 섹션에 있는 **ID** 링크를 선택합니다.

1.  **ID** 블레이드에서 **시스템 할당** 탭을 찾은 후 다음 작업을 수행합니다.
    
    1.  **상태** 섹션에서 **켜기**를 선택한 다음 **저장**을 선택합니다.
    
    1.  확인 대화 상자에서 **예**를 선택합니다.

    > **참고**: 이 랩을 진행하기 전에 할당된 시스템에서 관리 ID가 만들어질 때까지 기다립니다.

#### 작업 2: 키 자격 증명 모음 암호 만들기

1.  Azure Portal의 탐색 창에서 **리소스 그룹** 링크를 선택합니다.

1.  **리소스 그룹** 블레이드에서 해당 랩 앞에서 만든 **SecureFunction** 리소스 그룹을 찾아서 선택합니다.

1.  **SecureFunction** 블레이드에서 이전에 랩에서 만든 **securevault*[yourname]*** 키 자격 증명 모음을 선택합니다.

1.  **키 자격 증명 모음** 블레이드에서 **설정** 섹션에 있는 **비밀** 링크를 선택합니다.

1.  비밀 창에서 **생성/수입**을 선택합니다.

1.  **비밀 만들기** 블레이드에서 다음 작업을 수행합니다.
    
    1.  **업로드 옵션** 드롭다운 목록에서 **수동**을 선택합니다.
    
    1.  **이름** 텍스트 박스에 **storagecredentials**를 입력합니다.
    
    1.  **값** 텍스트 상자에 이전에 랩에서 기록한 스토리지 계정 연결 문자열을 입력합니다.
    
    1.  **콘텐츠 유형** 텍스트 상자를 기본값으로 둡니다.
    
    1.  **활성화 날짜 설정** 텍스트 상자를 기본값으로 설정한 상태로 둡니다.
    
    1.  **만료 날짜 설정** 텍스트 상자를 기본값으로 설정된 상태로 둡니다.
    
    1.  **사용** 섹션에서 **예**를 선택한 다음 **만들기**를 선택합니다. 
    
    > **참고**: 이 랩을 진행하기 전에 비밀이 만들어질 때까지 기다립니다.

1.  비밀 창으로 돌아가서 목록의 **storagecredentials** 항목을 선택합니다.

1.  버전 창에서 **storagecredentials** 비밀의 최신 버전을 선택합니다.

1.  비밀 버전 창에서 다음 작업을 수행합니다.
    
    1.  최신 버전의 비밀에 대한 메타데이터를 찾습니다.
    
    1.  비밀 값을 보려면 **비밀 값 표시**를 선택합니다.
    
    1.  나중에 랩에서 이 값을 사용하기 때문에 **비밀 식별자** 텍스트 상자의 값을 기록합니다.

    > **참고**: **비밀 값** 텍스트 상자가 아닌 **비밀 식별자** 텍스트 상자의 값을 기록하고 있습니다.

#### 작업 3: 키 자격 증명 모음 액세스 정책 구성

1.  Azure Portal의 탐색 창에서 **리소스 그룹** 링크를 선택합니다.

1.  **리소스 그룹** 블레이드에서 해당 랩 앞에서 만든 **SecureFunction** 리소스 그룹을 찾아서 선택합니다.

1.  **SecureFunction** 블레이드에서 이전에 랩에서 만든 **securevault*[yourname]*** 키 자격 증명 모음을 선택합니다.

1.  **Key Vault** 블레이드에서 **설정** 섹션에 있는 **액세스 정책** 링크를 선택합니다.

1.  액세스 정책 창에서 **액세스 정책 추가**를 선택합니다.

1.  **액세스 정책 추가** 블레이드에서 다음 작업을 수행합니다.
    
    1.  **주체 선택** 링크를 선택합니다.
    
    1.  **주체** 블레이드에서 **securefunc*[yourname]***이라는 서비스 주체를 찾아 선택한 다음, **선택**을 선택합니다.

        > **참고**: 이 랩의 앞에서 만든 시스템 할당 관리 ID는 Azure Function 리소스와 이름이 동일합니다.
    
    1.  **키 사용 권한** 목록을 기본값으로 그대로 둡니다.
    
    1.  **비밀 사용 권한** 드롭다운 목록에서 **가져오기** 권한을 선택합니다.
    
    1.  **인증서 사용 권한** 목록을 기본값으로 설정합니다.
    
    1.  **승인된 애플리케이션** 텍스트 상자를 기본값으로 설정합니다.
    
    1.  **추가**를 선택합니다.

1.  액세스 정책 창에서 **저장**을 선택합니다. 

    > **참고**: 이 랩을 진행하기 전에 액세스 정책에 대한 변경 내용이 저장될 때까지 기다립니다.

#### 검토

이 연습에서는 함수 앱에 대해 서버에서 할당된 관리 서비스 ID를 만든 다음, 해당 ID에 키 자격 증명 모음에서 비밀 값을 가져올 수 있는 적절한 권한을 부여했습니다. 마지막으로 함수 앱 내에서 사용할 비밀을 만들었습니다.

### 연습 3: 함수 앱 코드 작성 

#### 작업 1: Key Vault 파생 애플리케이션 설정 만들기 

1.  Azure Portal의 탐색 창에서 **리소스 그룹** 링크를 선택합니다.

1.  **리소스 그룹** 블레이드에서 해당 랩 앞에서 만든 **SecureFunction** 리소스 그룹을 찾아서 선택합니다.

1.  **SecureFunction** 블레이드에서 해당 랩 앞에서 만든 **securefunc*[yourname]*** 함수 앱을 선택합니다.

1.  **함수 앱** 블레이드에서 **플랫폼 기능** 탭을 선택합니다.

1.  **플랫폼 기능** 탭에서 **일반 설정** 섹션의 **구성** 링크를 클릭합니다.

1.  **구성** 섹션에서 다음 작업을 수행합니다.
    
    1.  **애플리케이션 설정** 탭을 선택한 다음 **새 애플리케이션 설정**을 선택합니다.
    
    1.  **애플리케이션 설정 추가/편집** 팝업 창의 **이름** 텍스트 상자에 **StorageConnectionString**을 입력합니다.
    
    1.  **값** 텍스트 박스에서 다음 구문을 사용하여 값을 생성합니다. **@Microsoft.KeyVault(SecretUri=*Secret Identifier*)**

        > **참고**: 위의 구문을 사용하여 ***비밀 식별자***에 대한 참조를 작성해야 합니다. 예를 들어 비밀 식별자가 **https://securevaultstudent.vault.azure.net/secrets/storagecredentials/17b41386df3e4191b92f089f5efb4cbf** 경우 **@Microsoft.KeyVault(SecretUri=https://securevaultstudent.vault.azure.net/secrets/storagecredentials/17b41386df3e4191b92f089f5efb4cbf)** 값이 됩니다.
    
    1.  **패포 슬롯 설정** 텍스트 박스를 기본값으로 설정한 상태로 둡니다.

    1.  **확인**을 선택하여 팝업 창을 닫고 **구성** 섹션으로 돌아갑니다.
    
    1.  블레이드에서 **저장**을 선택하여 설정을 유지합니다.  

    1.  **변경 내용 저장** 확인 팝업 대화 상자에서 **계속**을 선택합니다.

    > **참고**: 랩을 진행하기 전에 애플리케이션 설정이 유지될 때까지 기다립니다.

#### 작업 2: HTTP 트리거 함수 만들기

1.  Azure Portal의 탐색 창에서 **리소스 그룹** 링크를 선택합니다.

1.  **리소스 그룹** 블레이드에서 해당 랩 앞에서 만든 **SecureFunction** 리소스 그룹을 찾아서 선택합니다.

1.  **SecureFunction** 블레이드에서 해당 랩 앞에서 만든 **securefunc*[yourname]*** 함수 앱을 선택합니다.

1.  **함수 앱** 블레이드에서 **함수** 드롭다운 목록 옆에 있는 더하기 기호(**+**)를 선택합니다.

1.  **새 Azure 함수** 빠른 시작에서 다음 작업을 수행합니다.
    
    1.  **개발 환경 선택** 헤더에서 **포털에서**를 선택 후 **계속**을 선택합니다.
    
    1.  **함수 만들기** 헤더에서 **템플릿 추가**를 선택한 다음 **템플릿 종료 및 보기**를 선택합니다.
    
    1.  템플릿 목록에서 **HTTP 트리거**를 선택합니다.
    
    1.  **새 함수** 팝업 창에서 **이름** 텍스트 상자를 찾아 **FileParser**를 입력합니다.
    
    1.  **새 함수** 팝업 창에서 **권한 부여 수준** 목록을 찾아 **익명**을 선택합니다.
    
    1.  **새 함수** 팝업 창에서 **만들기**를 선택합니다.

1.  함수 편집기에서 예제 함수 스크립트를 찾습니다.

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
            : new BadRequestObjectResult("Please pass a name from the query string or in the request body");
    }
    ```

1.  예제 코드를 모두 **삭제**한 다음 함수 편집기에서 다음 자리 표시자 함수를 복사하여 붙여 넣습니다.

    ```
    using System.Net;
    using Microsoft.AspNetCore.Mvc;

    public static async Task<IActionResult> Run(HttpRequest req)
    {
        return new OkObjectResult("Test Successful");
    }
    ```

1.  **저장 및 실행**을 선택하여 스크립트를 저장하고 함수를 테스트합니다.

1.  스크립트가 처음으로 실행될 때 테스트 및 로그 창이 자동으로 나타납니다.

    > **참고**: 로그를 컴파일하는 동안 경고 내용이 나타날 수 있습니다. 무시해도 됩니다.

1.  테스트 창에서 **출력** 텍스트 상자를 찾습니다. 이제 함수에서 반환된 **테스트 성공** 값이 표시됩니다.

#### 작업 3: Key Vault 파생 애플리케이션 설정을 테스트합니다.

1.  스크립트의 **실행** 메서드 내에서 기존 코드를 삭제합니다.

1.  이제 다음을 포함해야 하는 **실행** 메서드를 관찰합니다.

    ```
    using System.Net;
    using Microsoft.AspNetCore.Mvc;

    public static async Task<IActionResult> Run(HttpRequest req)
    {

    }
    ```

1.  다음 코드 줄을 추가하여 **Environment.GetEnvironmentVariable** 메서드를 사용하여 **StorageConnectionString** 애플리케이션 설정의 값을 얻습니다.

    ```
    string connectionString = Environment.GetEnvironmentVariable("StorageConnectionString");
    ```

1.  다음 코드 줄을 추가하고 **OkObjectResult** 클래스 생성자를 사용하여 *connectionString* 변수의 값을 반환합니다.
   
    ```
    return new OkObjectResult(connectionString);
    ```
    
1.  이제 다음을 포함해야 하는 **실행** 메서드를 관찰합니다.

    ```
    using System.Net;
    using Microsoft.AspNetCore.Mvc;

    public static async Task<IActionResult> Run(HttpRequest req)
    {
        string connectionString = Environment.GetEnvironmentVariable("StorageConnectionString");
        return new OkObjectResult(connectionString);
    }
    ```

1.  **저장 및 실행**을 선택하여 스크립트를 저장하고 함수를 테스트합니다.

1.  테스트 창에서 **출력** 텍스트 상자를 찾습니다. 이제 함수에서 반환된 연결 문자열이 표시됩니다.

    > **참고**: 경고 메시지가 나타날 수 있습니다. 이것은 비동기 코드 없이 비동기 메서드를 사용하고 있음을 알리는 단순한 C# 컴파일러 경고입니다. 이 경고는 더 이상 랩에서 표시되지 않습니다.

#### 검토

이 연습에서는 서비스 ID를 사용하여 Key Vault에 저장된 비밀의 값을 읽고 함수 앱의 결과로 해당 값을 반환했습니다.

### 연습 4: 스토리지 계정 Blob에 액세스

#### 작업 1: 샘플 스토리지 blob 업로드

1.  Azure Portal의 탐색 창에서 **리소스 그룹** 링크를 선택합니다.

1.  **리소스 그룹** 블레이드에서 해당 랩 앞에서 만든 **SecureFunction** 리소스 그룹을 찾아서 선택합니다.

1.  **SecureFunction** 블레이드에서 이 랩 앞 부분에서 만든 **securestor*[yourname]*** 스토리지 계정을 선택합니다.

1.  **스토리지 계정** 블레이드에서 **Blob 서비스** 섹션에 있는 **컨테이너** 링크를 선택합니다.

1.  **컨테이너** 섹션에서 **+ 컨테이너**를 선택합니다.

1.  **새 컨테이너** 팝업 창에서 다음 작업을 수행합니다.
    
    1.  **이름** 텍스트 상자에 **드롭**를 입력합니다.
    
    1.  **공용 액세스 수준** 드롭다운 목록에서 **Blob(Blob 전용 익명 읽기 액세스)** 을 선택한 후 **확인**을 선택합니다.

1.  **컨테이너** 섹션으로 돌아가서 새로 만든 **드롭** 컨테이너를 선택합니다.

1.  **컨테이너** 블레이드에서 **업로드**를 선택합니다.

1.  **Blob 업로드** 팝업 창에서 다음 작업을 수행합니다.
    
    1.  **파일** 섹션에서 **폴더** 아이콘을 선택합니다.
    
    1.  **파일 탐색기** 창에서 **Allfiles (F):\\Allfiles\\Labs\\06\\Starter**를 찾아 **records.json** 파일을 선택하고 **열기**를 선택합니다.
    
    1.  **파일이 이미 있는 경우 덮어쓰기**가 선택되어 있는지 확인하고 **업로드**를 선택합니다.  

    > **참고**: 이 랩을 계속하기 전에 Blob이 업로드될 때까지 기다립니다.

1.  **컨테이너** 블레이드의 Blob 목록에서 **records.json** Blob을 선택합니다.

1.  **Blob** 블레이드에서 Blob 메타데이터를 찾은 다음 Blob의 URL을 복사합니다.

1.  작업 표시줄에서 **Microsoft Edge** 아이콘을 오른쪽 버튼으로 클릭하거나 바로 가기 메뉴를 활성화한 다음 **새 창**을 선택합니다.

1.  새 브라우저 창에서 blob에 대해 복사한 URL로 이동합니다.

1.  이제 Blob의 JSON(JavaScript Object Notation) 내용이 표시됩니다. JSON 내용을 표시하는 브라우저 창을 닫습니다.

1.  Azure Portal을 사용하여 브라우저 창으로 돌아가서 **Blob** 블레이드를 닫습니다.

1.  **컨테이너** 블레이드로 돌아가서 **액세스 수준 변경 정책**을 선택합니다.

1.  **액세스 수준 변경** 팝업창에서 다음 작업을 수행합니다.
    
    1.  **공용 액세스 수준** 드롭다운 목록에서 **비공개(익명 액세스 없음)** 를 선택합니다.
    
    1.  **확인**을 선택합니다.

1.  작업 표시줄에서 **Microsoft Edge** 아이콘을 오른쪽 버튼으로 클릭하거나 바로 가기 메뉴를 활성화한 다음 **새 창**을 선택합니다.

1.  새 브라우저 창에서 blob에 대해 복사한 URL로 이동합니다.

1.  이제 리소스를 찾을 수 없다는 오류 메시지가 표시됩니다.

    > **참고**: 오류 메시지가 표시되지 않으면 브라우저가 파일을 캐시한 것일 수 있습니다. Ctrl+F5를 눌러 오류 메시지가 표시될 때까지 페이지를 새로 고침합니다.

#### 작업 2: NuGet에서 저장소 계정 SDK 가져오기

1.  Azure Portal의 탐색 창에서 **리소스 그룹** 링크를 선택합니다.

1.  **리소스 그룹** 블레이드에서 해당 랩 앞에서 만든 **SecureFunction** 리소스 그룹을 찾아서 선택합니다.

1.  **SecureFunction** 블레이드에서 해당 랩 앞에서 만든 **securefunc*[yourname]*** 함수 앱을 선택합니다.

1.  **함수 앱** 블레이드에서 기존 **FileParser** 함수를 찾은 후 선택하여 함수에 대한 편집기를 엽니다.

    > **참고**: 블레이드 메뉴에서 **함수** 옵션을 확장해야 할 수 있습니다.

1.  편집기에서 **파일 보기**를 선택하여 탭을 엽니다.

1.  **파일 보기** 탭에서 **추가**를 선택합니다.

1.  **파일 이름** 대화 상자에서 **function.proj**를 입력한 다음 Enter를 선택하면 빈 코드 편집기가 표시됩니다.

1.  편집기에서 이 구성 내용을 삽입합니다.

    ```
    <Project Sdk="Microsoft.NET.Sdk">
        <PropertyGroup>
            <TargetFramework>netstandard2.0</TargetFramework>
        </PropertyGroup>
        <ItemGroup>
            <PackageReference Include="Azure.Storage.Blobs" Version="12.0.0" />
        </ItemGroup>
    </Project>
    ```

1.  편집기에서 **저장**을 선택하여 구성 변경 내용을 저장합니다.

    > **참고**: 이 .proj 파일에는 [Azure.Storage.Blobs](https://www.nuget.org/packages/Azure.Storage.Blobs/12.0.0) 패키지를 가져오는 데 필요한 NuGet 패키지 참조가 포함되어 있습니다.

1.  **run.csx** 파일을 선택하여 **FileParser** 함수에 대한 편집기로 돌아갑니다.

1.  **파일 보기** 탭을 최소화합니다.

    > **참고**: 탭 헤더에 연결된 화살표를 선택하여 탭을 최소화할 수 있습니다.

1.  편집기 내에서 스크립트의 **Run** 메서드의 기존 코드를 삭제합니다.

1.  코드 파일에 다음 코드 줄을 추가하여 **Azure.Storage** 네임스페이스에 대한 **using** 지시문을 만듭니다.

    ```
    using Azure.Storage;
    ```

1.  코드 파일에 다음 코드 줄을 추가하여 **Azure.Storage.Blobs** 네임스페이스에 대한 **using** 지시문을 만듭니다.

    ```
    using Azure.Storage.Blobs;
    ```

1.  다음 코드 줄을 추가하여 **Azure.Storage.Blobs.Models** 네임스페이스에 대한 **using** 지시문을 만듭니다.

    ```
    using Azure.Storage.Blobs.Models;
    ```

1.  이제 다음을 포함해야 하는 **실행** 메서드를 관찰합니다.

    ```
    using System.Net;
    using Microsoft.AspNetCore.Mvc;
    using Azure.Storage;
    using Azure.Storage.Blobs;
    using Azure.Storage.Blobs.Models;

    public static async Task<IActionResult> Run(HttpRequest req)
    {

    }
    ```

#### 작업 3: 스토리지 계정 코드 작성

1.  **실행** 메서드에서 다음 코드 줄을 추가하고 **Environment.GetEnvironmentVariable** 메서드를 사용하여 **StorageConnectionString** 애플리케이션 설정의 값을 얻습니다.

    ```
    string connectionString = Environment.GetEnvironmentVariable("StorageConnectionString");
    ```

1.  다음 코드 줄을 추가하여 *connectionString* 변수를 생성자에 전달함으로써 **BlobServiceClient** 클래스의 새 인스턴스를 만듭니다.

    ```
    BlobServiceClient serviceClient = new BlobServiceClient(connectionString);
    ```

1.  다음 코드 줄을 추가하여 **드롭** 컨테이너 이름을 전달하면서 **BlobServiceClient.GetBlobContainerClient** 메서드를 사용하여 이 랩의 앞에서 만든 컨테이너를 참조하는 **BlobContainerClient** 클래스의 새 인스턴스를 만듭니다.

    ```
    BlobContainerClient containerClient = serviceClient.GetBlobContainerClient("drop");
    ```

1.  다음 코드 줄을 추가하여 **records.json** Blob 이름을 전달하면서 **BlobContainerClient.GetBlobClient** 메서드를 사용하여 이 랩의 앞에서 만든 Blob을 참조하는 **BlobClient** 클래스의 새 인스턴스를 만듭니다.

    ```
    BlobClient blobClient = containerClient.GetBlobClient("records.json");
    ```
    
1.  이제 다음을 포함해야 하는 **실행** 메서드를 관찰합니다.

    ```
    using System.Net;
    using Microsoft.AspNetCore.Mvc;
    using Azure.Storage;
    using Azure.Storage.Blobs;
    using Azure.Storage.Blobs.Models;

    public static async Task<IActionResult> Run(HttpRequest req)
    {
        string connectionString = Environment.GetEnvironmentVariable("StorageConnectionString");
        BlobServiceClient serviceClient = new BlobServiceClient(connectionString);
        BlobContainerClient containerClient = serviceClient.GetBlobContainerClient("drop");
        BlobClient blobClient = containerClient.GetBlobClient("records.json");
    }
    ```

#### 작업 4: Blob 다운로드

1.  다음 코드 줄을 추가하고 **BlobClient.DownloadAsync** 메서드를 사용하여 참조된 Blob의 내용을 비동기적으로 다운로드하고 결과를 *response*라는 문자열 변수에 저장합니다.

    ```
    var response = await blobClient.DownloadAsync();
    ```

1.  다음 코드 줄을 추가하고 **FileStreamResult** 클래스 생성자를 사용하여 *content* 변수에 저장된 다양한 내용을 반환합니다.

    ```
    return new FileStreamResult(response?.Value?.Content, response?.Value?.ContentType);
    ```

1.  이제 다음을 포함해야 하는 **실행** 메서드를 관찰합니다.

    ```
    using System.Net;
    using Microsoft.AspNetCore.Mvc;
    using Azure.Storage;
    using Azure.Storage.Blobs;
    using Azure.Storage.Blobs.Models;

    public static async Task<IActionResult> Run(HttpRequest req)
    {
        string connectionString = Environment.GetEnvironmentVariable("StorageConnectionString");
        BlobServiceClient serviceClient = new BlobServiceClient(connectionString);
        BlobContainerClient containerClient = serviceClient.GetBlobContainerClient("drop");
        BlobClient blobClient = containerClient.GetBlobClient("records.json");
        var response = await blobClient.DownloadAsync();
        return new FileStreamResult(response?.Value?.Content, response?.Value?.ContentType);
    }
    ```

1.  **저장 및 실행**을 선택하여 스크립트를 저장하고 함수를 테스트합니다.

1.  테스트 창에서 **출력** 텍스트 상자를 찾습니다. 이제 저장소 계정에 저장된 **$/drop/records.json** Blob의 내용이 표시됩니다.

#### 검토

이 연습에서는 C\# 코드를 사용하여 스토리지 계정에 액세스한 다음 Blob의 내용을 다운로드했습니다.

### 연습 5: 구독 정리 

#### 작업 1: Azure Cloud Shell 열기 및 리소스 그룹 나열

1.  Azure Portal의 탐색 창에서 **Cloud Shell** 아이콘을 선택하여 새 셸 인스턴스를 엽니다.

    > **참고**: **Cloud Shell**아이콘은 초과 기호 () 및 밑줄 문자(\_)로 표시됩니다.

1.  구독을 사용하여 Cloud Shell을 처음으로 여는 경우, 처음 사용할 경우에만 **Azure Cloud Shell 시작 마법사**를 사용하여 Cloud Shell를 구성할 수 있습니다. 마법사에서 다음 작업을 합니다.
    
    1.  대화 박스는 셸을 사용하여 시작할 새 스토리지 계정을 만들라는 메시지를 표시합니다. 기본 설정을 수락하고 **스토리지 만들기**를 선택합니다. 

    > **참고**: 랩으로 진행하기 전에 Cloud Shell이 초기 설치 절차를 완료할 때까지 기다립니다. Cloud Shell의 구성 옵션이 나타나지 않는 경우 이 과정의 랩에서 기존 구독을 사용하고 있기 때문일 수 있습니다. 랩은 새 구독을 사용 한다는 가정에서 작성됩니다.

1.  포털의 **Cloud Shell** 명령 프롬프트에서 다음 명령을 입력하고 엔터를 선택하여 구독의 모든 리소스 그룹을 나열합니다.

    ```
    az group list
    ```

1.  프롬프트에서 다음 명령을 입력하고 Enter 키를 선택하여 리소스 그룹을 삭제하는 명령 목록을 찾습니다.

    ```
    az group delete --help
    ```

#### 작업 2: 리소스 그룹 삭제

1.  프롬프트에서 다음 명령을 입력하고 Enter 키를 선택하여 **SecureFunction** 리소스 그룹을 삭제합니다.

    ```
    az group delete --name SecureFunction --no-wait --yes
    ```
    
1.  포털에서 Cloud Shell 창을 닫습니다.

#### 작업 3: 활성 애플리케이션 닫기

1.     현재 실행 중인 Microsoft Edge 애플리케이션.

#### 검토

이 연습에서는 이 랩에 사용된 리소스 그룹을 제거하여 구독을 정리했습니다.
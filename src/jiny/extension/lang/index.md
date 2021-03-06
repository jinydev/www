---
layout: home
---

# 다국어 페키지
---
`지니PHP`는 다국어 처리를 위한 새로운 공개 페키지(`jiny/lang`)를 생성(2018.10.14)하였습니다.  
다국어 페키지는 소스코드의 변경없이 다양한 언어의 문자열을 관리하고 출력하는 역활을 수행합니다.  

<br>
## 설치방법
---
다국어 페키지의 이름은 `jiny/lang`입니다. PHP코드로 작성이 되었으며, 컴포저를 통하여 배포를 합니다.

```
composer require jiny/lang
```

위와 같이 입력하시면 페키지를 설치할 수 있습니다.

<br>
## 사용방법
---
페키지를 설치하시면 간단한 예제 코드가 있습니다.

src/text/index.php
```php
<?php

require 'vendor/autoload.php';

$msg = _msg_init();
$msg->enableTrans("transkey.php");

$str = "오류가 발생하였습니다.";
echo $msg->echo($str,"en");
```

컴포저 오토로드를 통하여 인스턴스를 생성후에 사용을 하실 수 있습니다.

### 인스턴스 생성
---
빠르고 간단한 인스턴스 생성을 위해서 전용 헬퍼함수를 제공합니다. `_msg_init()` 함수는 `jiny/lang`의 패키지 인스턴스를 생성하여 반환을 합니다.

### 구글번역 키
---
`jiny/lang`은 입력된 문자열을 자동으로 번역처리를 지원합니다. 자동번역을 사용하기 위해서는 구글 번역API 키가 필요로 합니다.  

API는 별도의 파일로 작성을 하여 삽입을 합니다. 페키지에는 키작성 방식에 대한 예제파일이 같이 제공됩니다.

transkey.php
```php
<?php

/**
 * 구글 API 설정파일
 */
return [
    'key' => 'API키를 입력해 주세요'
];
```

이렇게 작성한 키파일의 경로를 `enableTrans()` 메소드의 인자값으로 전달을 합니다.

```php
$msg->enableTrans("transkey.php");
```
키파일을 작성되면 자동적으로 번역기능을 통하여 문자열을 관리하게 됩니다.

<br>
## 사용방법
---
문자열의 다국어 처리를 하는 방법은 간단합니다.

```php
$str = "오류가 발생하였습니다.";
echo $msg->echo($str,"en");
```

`echo()`메소드를 호출하시면 됩니다. 호출시 인자값은 2개가 있습니다.  
기준이 되는 문자열과, 언어 코드 입니다. 언어코드는 생략이 가능하나, 생략시에는 입력한 문자열이 반환됩니다.  

<br>
## 동작원리
---
`jiny/lang`의 다국어 처리결과는 파일로 저장이 됩니다.  
각각의 문자열에 맞는 `sha3-512` 해시를 생성하여 파일단위로 관리를 합니다. 

<br>
### 리소스경로
---
각각의 문자열 파일은 설정한 디렉토리(`resource/lang`)에 저장을 하게 됩니다.
기본 저장경로를 변경을 원하신다면 `인스턴스 초기값`으로 경로를 설정하시면 됩니다.  

```php
$msg = _msg_init("경로주소");
```

### 파일구성
---
문자열 리소스는 json 형태로 저장이 됩니다.

```json
{
    "str": "오류가 발생하였습니다.",
    "en": [
        {
            "text": "An error has occurred.",
            "timestamp": 1539499286,
            "email": null
        }
    ]
}
```

위와 같이 원문 문자열 `str`을 가지고 있습니다. 또한, 각각의 언어코드에 맞게 문자열을 가지고 있습니다.
문자열은 `작성일자`와 `작성자 정보`를 같이 가지게 되어 있습니다.

<br>
### 히스토리 관리
---
언어별 문자열은 복수의 배열로 구성이 되어 있습니다. 맨 마지막에 최신 버전을 위에 존재하게 됩니다.

<br>
### 캐쉬기능
---
호출되는 문자열은 파일 형태로 캐쉬되어 있습니다. 매번 번역을 진행하지 않기 때문에 외부 API 서비스 비용을 절감할 수 있습니다.  
또한, 기계번역 외에 `사용자번역`을 직접 추가할 수 있습니다. 사용자 번역을 맨 위의 배열값으로 설정하시면 우선 출력 됩니다.

<br>
## 의존성
---
`jiny/lang` 페키지는 몇개의 다른 페키지들을 포함하는 의존관계가 있습니다.  
보다 자세한 것은 `composer.json`파일을 참고하시길 바랍니다.

<br>
## 오픈소스
---
`jiny/lang`은 오픈소스로 진행되는 응용 페키지 라이브러리 입니다. 모든 소스는 깃허브에 저장되어 있으며 주소는 다음과 같습니다.  
https://github.com/jinyphp/lang.git

누구나 라이브러리 소스 개발에 참여하실 수 있으며, 포크 및 수정후에 풀리퀘스트를 보내주시면 됩니다.

<br>
<br>
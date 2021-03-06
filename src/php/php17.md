---
layout: php
title: "PHP"
keyword: "jinyphp, php"
---
## 오류 및 예외 처리

프로그램을 개발하다 보면 수많은 오류와 예외가 발생합니다. 보통 오류는 크게 코드상의 문법 오류와 소스상의 논리적인 오류로 구분할 수 있습니다. 문법적 오류는 PHP가 시작하기 전에 체크하여 알려주기 때문에 쉽게 문법적 오류를 해결할 수 있습니다. 하지만 논리적인 오류는 쉽게 찾을 수 있는 오류가 아닙니다. 또한 이러한 문제로 인해 프로그램은 정상적인 동작을 수행하지 못하고 중간에 중단되기도 합니다.

개발자는 오류 및 예외 메시지가 발생하면 잘못된 부분을 인지하고, 문제를 해결하기 위해 노력합니다. 이러한 오류와 예외 처리가 미흡하면 다수의 잘못된 메시지가 사용자에게 출력되거나 불편함을 줄 것 입니다. 논리적인 오류는 개발자들에게 많은 디버깅 시간을 투여하게 만들도록 합니다.

그렇다고 해서 발생한 오류 메시지를 화면에 출력하면 프로그램의 완성도에 대한 신뢰를 떨어뜨릴 수 있습니다.

개발의 기술이 높아지고 경험이 많을수록 개발자는 PHP 오류와 예외를 예측하여 처리해야 합니다.

 
17.1 오류

사실 기본적인 오류 처리는 대부분의 프로그래밍 언어에서는 거의 다 지원하는 기능입니다.

우리가 가장 많이 접하는 오류는 문법적으로 코드가 잘못 작성되었을 때입니다. 인터프리터, 컴파일러는 잘못된 부분을 오류 메시지를 통해 개발자에게 즉시 알려 줍니다. 사실상 문법적인 오류는 PHP 스크립트 실행이 되지 않기 때문에 쉽게 문제를 해결할 수 있습니다.

PHP의 기본적인 문법 오류 처리는 매우 간단합니다. 오류 메시지, 파일 이름, 줄 번호를 출력하는 게 전부입니다. 오류가 발생하면 대부분 프로그램은 실행을 할 수 없거나, 동작을 중단합니다. 
  
PHP는 오류 출력 제한 연산자 @를 통해 오류 메시지 출력을 제한할 수 있지만 권장하지 않는 안티 패턴입니다. 개발자는 프로그램 오류가 발생하지 않도록 최대한 노력해야 하며, 만일 오류가 발생하면 다른 대처를 통해 처리하는 것이 좋습니다.

PHP는 오류 발생 시 처리할 수 있는 간단한 몇 가지 함수를 제공합니다.

17.1.1 die() & exit() 

die() 내장 함수는 exit() 함수와 유사합니다. exit() 함수는 사용자 메시지를 출력하고 현재 스크립트를 종료합니다. 

|관련함수|
void exit ([ string $status ] )

예제 파일 exit-01.php
<?php

	$filename = 'abcd.txt';
	$file = fopen($filename, 'r') or exit("파일을 읽을 수 없습니다.");

?>

결과
파일을 읽을 수 없습니다.

위의 예제는 파일 읽기 예입니다. 파일을 읽기 위해서 파일 포인터를 엽니다. 만일 파일 포인터를 생성하지 못면 exit() 함수를 통해서 스크립트를 종료합니다.

17.1.2 오류 발생 

trigger_error() 함수를 이용하면 사용자가 직접 오류를 발생시킬 수 있습니다.

예제 파일 error-01.php
<?php
	trigger_error("사용자 오류 발생", E_USER_ERROR);
?>

결과
[Sun May 14 17:24:40 2017] PHP Fatal error: 사용자 오류 발생 in C:\php-7.1.4-Win32-VC14-x86\jinyphp\error-01.php on line 2
[Sun May 14 17:24:40 2017] ::1:56024 [500]: /jinyphp/error-01.php - 사용자 오류 발생 in C:\php-7.1.4-Win32-VC14-x86\jinyphp\error-01.php on line 2

E_* 상수는 여러 개의 상수를 |, & 비트 연산을 하여 사용할 수 있습니다.

1 : E_ERROR(integer)
치명적인 런타임 오류. 이는 메모리 할당 문제와 같이 복구할 수 없는 오류를 나타냅니다. 스크립트 실행이 중지되었습니다.
 
2 : E_WARNING(integer)
런타임 경고(치명적이지 않은 오류). 스크립트의 실행이 중지되지 않습니다.
 
4 : E_PARSE(integer)
컴파일 타임 구문 분석 오류. 구문 분석 오류는 구문 분석기에서만 생성해야 합니다.

8 : E_NOTICE(integer)
런타임 고지. 스크립트가 오류를 나타낼 수 있지만 스크립트를 실행하는 정상적인 과정에서 발생할 수 있음을 나타냅니다.
 
16 : E_CORE_ERROR(integer)
PHP가 처음 시작될 때 발생하는 치명적인 오류. 이것은 E_ERROR와 비슷하지만, PHP 코어에서 생성된다는 점만 다릅니다.
 
32 :E_CORE_WARNING(integer)
PHP가 처음 시작될 때 발생하는 경고(치명적이지 않은 오류). 이것은 E_WARNING과 비슷하지만 PHP 코어에서 생성된다는 점만 다릅니다.
 
64 : E_COMPILE_ERROR(integer)
치명적인 컴파일 타임 오류. 이것은 Zend Scripting Engine에 의해 생성된다는 것을 제외하고는 E_ERROR와 같습니다.
 
128 : E_COMPILE_WARNING(integer)
컴파일 타임 경고(치명적이지 않은 오류). 이것은 Zend Scripting Engine에 의해 생성된다는 점을 제외하고는 E_WARNING과 같습니다.
 
256 : E_USER_ERROR(integer)
사용자 생성 오류 메시지. PHP 함수 trigger_error ()를 사용하여 PHP 코드에서 생성된다는 점을 제외하고는 E_ERROR와 유사합니다.
 
512 : E_USER_WARNING(integer)
사용자 생성 경고 메시지. 이것은 PHP 함수 trigger_error ()를 사용하여 PHP 코드에서 생성된다는 점을 제외하고는 E_WARNING과 같습니다.
 
1024 : E_USER_NOTICE(integer)
사용자 생성 알림 메시지 PHP 함수 trigger_error ()를 사용하여 PHP 코드에서 생성된다는 점을 제외하고는 E_NOTICE와 같습니다.
 
2048 : E_STRICT(integer)
PHP가 코드의 변경을 제안하도록 하여 최상의 상호 운용성과 코드의 호환성을 보장하십시오.

4096 : E_RECOVERABLE_ERROR(integer)
잡을 수 있는 치명적인 오류. 아마도 위험한 오류가 발생했음을 나타내지만 엔진을 불안정한 상태로 두지 않았습니다. 사용자 정의 핸들(set_error_handler () 참조)이 오류를 catch하지 않으면 응용프로그램은 E_ERROR이므로 중단됩니다.

8192 : E_DEPRECATED(integer)
런타임 고지. 향후 버전에서 작동하지 않을 코드에 대한 경고를 받으려면 이 옵션을 활성화.

16384 : E_USER_DEPRECATED(integer)
사용자 생성 경고 메시지. PHP 함수 trigger_error ()를 사용하여 PHP 코드에서 생성된다는 점을 제외하고는 E_DEPRECATED와 같습니다.

32767 : E_ALL (integer)
PHP 5.4.0 이전의 레벨 E_STRICT를 제외하고 지원되는 모든 오류 및 경고.
PHP 5.4.x에서 32767, PHP 5.3.x에서 30719, PHP 5.2.x에서 6143, 이전에 2047 코드번호.


17.1.3 커스텀 에러 핸들러 

사용자 에러 핸들러는 매우 간단하게 생성할 수 있습니다. 단지 오류가 발생되었을 때 사용할 별도의 함수를 만들어 놓으면 됩니다.

이 함수는 적어도 2개의 파라미터를 가지고 있어야 합니다. 바로 오류 레벨과 메시지입니다. 매개변수는 최대 5개까지 추가할 수 있습니다. 사용자 에러 처리 함수를 set_error_handler() 함수를 통해 전역 오류 처리기로 등록할 수 있습니다.

|관련함수|
오류 처리_함수($errno, $errstr, $errfile, $errline, $errcontext)
set_error_handler(오류 처리_함수);

$errno
오류 단계를 대응합니다. PHP E_* 상수를 대응합니다.

$errstr
오류 메시지

$errfile
오류가 발생된 파일명

$errLine
오류가 발생된 명령줄

$errcontext
오류가 발생된 시점의 심볼 테이블 배열


예제 파일 error-02.php
<?php
	function userError($errno, $errstr){
		echo "사용자 오류 처리: [$errno] = $errstr <br>";
	}
	set_error_handler("userError");

	trigger_error("사용자 오류 발생", E_USER_ERROR);
?>

결과
사용자 오류 처리: [256] = 사용자 오류 발생

위의 예제는 사용자 오류 처리를 위한 예입니다. 먼저 오류 발생 시 처리할 함수를 생성합니다. 생성한 처리 함수를 set_error_handler() 함수를 통해 등록합니다. 그리고 사용자가 직접 오류를 발생하여 앞서 지정한 오류 처리 함수가 동작을 하는지 테스트할 수 있습니다.


17.2 예외
예외라는 말은 프로그램 실행 도중 예상치 않은 동작이나 불확실한 처리로 발생할 수 있는 부분을 예상하여 오류까지도 같이 처리를 하는 코딩 방법입니다. try{} catch {}의 문법과 별도의 예외 처리를 위한 클래스 등이 존재합니다.

예외 처리는 PHP스크립트가 실행하면서 오류가 발생했을 때 처리할 수 있는 로직을 만들어 넣을 수 있는 기술입니다. 예외 처리 개념은 PHP 5.x 이전에는 도입되지 않았습니다.

오류의 경우는 프로그램의 문제가 발생하면 오류를 통보하고 프로그램이 중단됩니다. 하지만, 예외는 갑작스러운 오류 발생 시 스크립트를 그냥 종료하는 것이 아니라 별도의 처리 루틴을 통해 안전하게 프로그램을 마칠 수 있도록 합니다.


17.2.1 Exception 클래스
PHP는 예외 처리를 위해서 특별한 Exception 클래스를 제공합니다. 예외 처리 클래스는 예외 발생 시 심각한 오류를 안전한 경로로 우회하여 처리할 수 있도록 도와줍니다.

예외 처리 클래스 Exception도 new 키워드를 통해 인스턴스를 생성하여 사용할 수 있습니다. Exception 클래스는 오류 코드와 메시지를 전달하고 값을 처리할 수 있는 추가 메서드를 지원합니다.

예제 파일 exception-01.php
<?php
	$msg = "예외 클래스 오류 발생";
	$code = 444;
	$e = new Exception($msg,$code);

	echo "예외 코드 = ".$e->getCode();
	echo "<br>";
	echo "예외 메시지 = ".$e->getMessage();
?>

결과
예외 코드 = 444
예외 메시지 = 예외 클래스 오류 발생

예외 Exception 클래스 구조와 인터페이스는 다음과 같습니다.

Exception {
/* Properties */
protected string $message ;
protected int $code ;
protected string $file ;
protected int $line ;

/* Methods */
public __construct ([ string $message = "" [, int $code = 0 [, Throwable $previous = NULL ]]] )
final public string getMessage ( void )
final public Throwable getPrevious ( void )
final public mixed getCode ( void )
final public string getFile ( void )
final public int getLine ( void )
final public array getTrace ( void )
final public string getTraceAsString ( void )
public string __toString ( void )
final private void __clone ( void )
}

예외 처리가 발생하면 PHP 엔진은 Exception 클래스로 예외를 발생한 부분을 처리하게 됩니다.

PHP 7.x에서는 Exception 클래스는 throwable 인터페이스를 따릅니다.

Throwable {
/* Methods */
abstract public string getMessage ( void )
abstract public int getCode ( void )
abstract public string getFile ( void )
abstract public int getLine ( void )
abstract public array getTrace ( void )
abstract public string getTraceAsString ( void )
abstract public Throwable getPrevious ( void )
abstract public string __toString ( void )
}


17.2.2 throw

throw 키워드를 이용하여 사용자가 직접 예외를 발생할 수 있습니다. 예외가 발생하면 PHP는 코드 실행을 중지됩니다.

 throw 키워드는 Exception과 관련 서브 클래스에서만 사용이 가능한 키워드입니다. 

●	Exception
●	ErrorException

예제 파일 exception-02.php
<?php
	throw new Exception("강제적 예외 발생");
?>

결과
[Sun May 14 16:21:35 2017] ::1:55806 [500]: /jinyphp/exception-02.php - Uncaught Exception: 강제적 예외 발생 in C:\php-7.1.4-Win32-VC14-x86\jinyphp\exception-02.php:2
Stack trace:
#0 {main}
thrown in C:\php-7.1.4-Win32-VC14-x86\jinyphp\exception-02.php on line 2

위의 예제는 예외 발생 처리 예입니다. throw 명령으로 사용자가 직접 예외를 발생할 수 있습니다.

17.2.3 Exception 상속

예외 처리 Exception 클래스를 상속받아 새로운 에외 처리 클래스를 직접 만들어서 사용할 수도 있습니다. 새로운 예외 처리는 클래스는 기존의 exception 함수를 상속받아서 생성을 합니다.

|문법|
class divException extends exception {}

예제 파일 exception-03.php
<?php
	class aaaEx extends exception
	{
		public function showErr($msg)
		{
			echo $msg;
		}
	}

	$msg = "예외 클래스 오류 발생";
	$code = 444;
	$e = new aaaEx($msg,$code);

	$e->showErr("Exception을 상속합니다.");
	echo "<br>";
	echo "예외코드 = ".$e->getCode();
	echo "<br>";
	echo "예외메시지 = ".$e->getMessage();
?>

결과
Exception을 상속합니다.
예외 코드 = 444
예외 메시지 = 예외 클래스 오류 발생

위의 예제는 예외 처리 클래스 상속에 대한 예입니다. 기존 exception 예외 클래스를 상속받아 새로운 예외 처리 클래스를 만들어서 사용할 수 있습니다.

17.2.4 예외 포착
개발자는 예외 처리에 대해서 수동적인 방어 보다는 능동적인 방어가 필요합니다. 적극적으로 예외가 발생될 것을 예측하여 프로그램 코드를 작성해야 합니다.

PHP 언어는 예외를 포착할 수 있는 try ~ catch 명령 키워드를 제공합니다. try~catch는 C++이나 Java 등에서 일찌감치 예외 처리를 위해 사용하던 문법입니다. PHP 5.x 이후부터는 이와 비슷한 스타일로 예외 처리 문장을 만들 수 있습니다.

프로그램이 동작할 때 예외가 발생할 가능성이 있다고 하면 try {} catch {} 명령으로 예외 발생을 대비하는 것이 좋습니다.

 

try~catch는 2개의 영역으로 나누어져 있습니다.

|문법|
try {
	예외가 발생할 가능성이 있는 내용들을 코딩합니다.
} catch (클래스명 $변수명) {
	예외가 발생될 경우 처리할 내용들
}


try { } 부분
try 본문 안에는 예외가 발생될 가능성이 높은 코드를 작성하는 영역입니다. 특별한 코드가 이니라 정상적으로 수행하고자 하는 코드를 작성합니다. 만일 이 코드들이 예외를 발생할 여지가 있는 경우 try{} 로 코드를 감싸서 실행하는 것입니다.

오류 예외가 발생되지 않으면 큰 문제나 의미 없이 코드가 실행될 것입니다. 만일 try 안에 있는 코드에 예외가 발생하면 코드 실행을 중단하게 됩니다. 그리고 catch 부분의 코드를 수행합니다.

catch {} 부분
catch (클래스명 $변수명) { }은 try{} 본문에 예외가 포착되었을 때 처리되는 내용들입니다.

예외가 발생할 때 Excetion 클래스를 통해 예외 상태나 메시지를 받아올 수 있습니다. Exception 클래스는 예외를 처리할 수 있는 다양한 프로퍼티와 메서드를 가지고 있습니다.

|문법|
catch(Exception $err){
	echo $err->getMessage();
} 

예외 발생 시 Exception 클래스로 생성된 인스턴스를 받습니다. 생성된 인스턴스로 Exception 메서드를 실행할 수 있습니다.

예제 파일 exception-04.php
<?php
	try {
	
		throw new Exception("강제적 예외 발생");

	} catch(Exception $err){
		// Try {} 부분에 연산 오류로 인하여 예외 처리가 발생됨
		echo "예외 처리 발생 :".$err->getMessage();
	} 
?>

결과
예외 처리 발생: 강제적 예외 발생

위의 예제는 try~catch 동작에 대한 예입니다. try {} 본문 안에서 강제적으로 throw 명령을 통해 개발자가 직접 예외를 발생합니다. 예외가 발생되면catch{} 안의 내용이 실행됩니다. catch 실행 시 예외 처리 클래스 exception 객체를 동시에 생성하여 catch 내부로 전달합니다.

catch 내에서는 exception 클래스로 생성된 객체를 접근하여 메시지 및 상태를 체크할 수 있습니다.

17.2.5 다중 catch
만일 예외 처리의 유형이 다양한 경우 catch를 연결하여 사용 가능합니다.

|문법|
try {
	예외가 발생할 가능성이 있는 내용들을 코딩합니다.
} catch (클래스명 $변수명) {
	예외가 발생될 경우 처리할 내용들
} catch (클래스명 $변수명) {
	예외가 발생될 경우 처리할 내용들
}

catch는 위의 표현처럼 계속 체인 형태로 연결하여 사용할 수 있습니다.

예제 파일 exception-05.php
<?php
	try {
		$servername = "localhost";
		$dbname = "testDB";
		$username = "jiny";
		$pasword = "abcd1234";

		$conn = new PDO("mysql:host=$servername;dbname=$dbname", $username, $password);
	
	} catch (PDOException $e) {
		echo "PDO 오류";

	} catch (Exception $e) {
		echo "일반예외";
	}
?>

결과
PDO 오류

위의 예제는 다수의 catch 처리를 위한 실험입니다. 예외가 발생되면 예외 상태에 따라서 상항별로 catch 로 분기하여 처리됩니다.
 

17.2.6 finally

finally { } 부분은 PHP 5.5에서 도입된 기능으로 try 부분이나 catch부분 처리가 끝나고 처리할 내용을 추가로 정의할 수 있습니다. finally {}는 독립적으로 사용을 할 수 없고 반드시 try ~ catch문 뒤에 소속되어 사용 가능합니다. 즉, 종속된 기능 명령어 입니다.

사용 문법
try {
	예외가 발생할 가능성이 있는 내용들을 코딩합니다.
} catch (클래스명 $변수명) {
	예외가 발생될 경우 처리할 내용들
} finally {
	예외 발생 여부와 상관없이 처리할 내용
}


예제 파일 exception-06.php
<?php
	try {
	
		throw new Exception("강제적 예외 발생");

	} catch(Exception $err){
		// Try {} 부분에 연산오류로 인하여 예외 처리가 발생됨
		echo "예외 처리 발생 :".$err->getMessage();
	} finally {
		// try {} 또는 catch(){} 부분의 처리 후에 처리가 됩니다.
		echo "<br>";
		echo "finally 연산 종료";
	}
?>


결과
예외 처리 발생: 강제적 예외 발생
finally 연산 종료

위의 예제는 final 에 대한 예입니다. 예외가 발생하면 catch 부분을 수행합니다. 그리고 catch 부분을 처리 후에 finally {} 부분을 실행합니다.


17.2.7 전역 예외 처리
try~catch로 처리하지 못한 예외가 있을 수도 있습니다. 이런 경우 전역 예외 처리를 통해 예상치 못한 예외도 포착할 수 있습니다.

|관련함수|
callable set_exception_handler ( callable $exception_handler )


set_exception_handler(); 내장 함수를 통하여 전역 예외 처리를 등록할 수 있습니다.

|관련함수|
bool restore_exception_handler ( void )

restore_exception_handler(); 내장 함수는 설정한 전역 처리기를 복원합니다.


예제 파일 exception-07.php
<?php
	// 전역 예외 처리기를 등록합니다.
	set_exception_handler(function(Exception $e){
		echo "전역 예외 처리 포착<br>";
		echo "예외 메시지 = ".$e->getMessage();
	});

	throw new Exception("강제적 예외 발생");

	// 설정한 전역 처리기를 복원합니다.
	restore_exception_handler();
?>

결과)
전역 예외 처리 포착
예외 메시지 = 강제적 예외 발생

위의 예제는 전역 예외 처리에 대한 예입니다. set_exception_handler() 함수를 통해 적역 예외 처리 함수를 등록합니다.

## 🚀 기능 요구사항

****
* 로또
  * [x] 당첨 번호
    * 행동 : 총 7번의 공을 뽑는다.
    * 조건 : 중복되지 않는 숫자 6개와 보너스 번호 1개를 뽑는다.
  * [x] 등수
    * 기준 : 맞은 개수에 따라 등수가 차등으로 선전
    * 행동 : 등수에 맞는 상금 적립
  * [x] 수익률
    * 구매자가 구매한 로또의 개수와 당첨된 로또의 상금을 비교하여 수익률을 계산한다.

<BR>

* 구매자
  * [x] 1000원 단위로 로또 구매 가능
  * [x] 구매자가 로또 구입 금액 입력 -> 구입 해당 금액 만큼 로또 발행
  * [x] 본인의 로또 번호는 pickUniqueNumbersInRange()를 활용하여 6개의 숫자를 자동으로 할당받는다.
    ```
    List<Integer> numbers = Randoms.pickUniqueNumbersInRange(1, 45, 6);
    ```


**** 

## 입출력 요구사항

#### 입력
* 로또 구입 금액을 입력 받는다. 구입 금액은 1,000원 단위로 입력 받으며 1,000원으로 나누어 떨어지지 않는 경우 예외 처리한다.
```
8000 일 경우 8장의 로또를 구입하게된다.
```


* 당첨 번호를 입력 받는다. 번호는 쉼표(,)를 기준으로 구분한다.
```
1,2,3,4,5,6
```

* 보너스 번호를 입력 받는다.
```
7
```
<br>

#### 출력
* 발행한 로또 수량 및 번호를 출력한다. 로또 번호는 오름차순으로 정렬하여 보여준다.
```
8개를 구매했습니다.
[8, 21, 23, 41, 42, 43] 
[3, 5, 11, 16, 32, 38] 
[7, 11, 16, 35, 36, 44] 
[1, 8, 11, 31, 41, 42] 
[13, 14, 16, 38, 42, 45] 
[7, 11, 30, 40, 42, 43] 
[2, 13, 22, 32, 38, 45] 
[1, 3, 5, 14, 22, 45]
```
* 당첨 내역을 출력한다.
```
3개 일치 (5,000원) - 1개
4개 일치 (50,000원) - 0개
5개 일치 (1,500,000원) - 0개
5개 일치, 보너스 볼 일치 (30,000,000원) - 0개
6개 일치 (2,000,000,000원) - 0개
```

* 수익률은 소수점 둘째 자리에서 반올림한다. (ex. 100.0%, 51.5%, 1,000,000.0%)

```
총 수익률은 62.5%입니다.
```
```
- 구익 금액만큼의 소득이 있을 시 100.0%로 계산됨
- 8000원을 구입하고 5000원을 번 경우
    
    → 계산 예시 : (5000 / 8000) * 100 = 62.5%
```
****
## 프로그램 요구사항
* [x] indent depth 2 이하
* [x] 3항 연산자 사용 금지
* [x] {....} 함수가 한가지 일만 하도록 최대한 작게 만들기
* [x] JUnit 5와 AssertJ를 이용하여 본인이 정리한 기능 목록이 정상 동작함을 테스트 코드로 확인
<BR>

#### 추가된 요구사항
* [x] 함수(또는 메서드)의 길이가 15라인을 넘어가지 않도록 구현
* [x] else 예약어를 쓰지 않는다.
  * 힌트: if 조건절에서 값을 return하는 방식으로 구현하면 else를 사용하지 않아도 된다.
  * else를 쓰지 말라고 하니 switch/case로 구현하는 경우가 있는데 switch/case도 허용하지 않는다.
* [x] Java Enum을 적용
* [x] 메인 로직에 단위 테스트를 구현해야 한다. 단, UI(System.out, System.in, Scanner) 로직은 제외
  * 핵심 로직을 구현하는 코드와 UI를 담당하는 로직을 분리해 구현
  * 단위 테스트 작성이 익숙하지 않다면 `test/java/lotto/LottoTest`를 참고하여 학습한 후 테스트를 구현
### Lotto 클래스

- 제공된 `Lotto` 클래스를 활용해 구현해야 한다.
- `numbers`의 접근 제어자인 private을 변경할 수 없다.
- `Lotto`에 필드(인스턴스 변수)를 추가할 수 없다.
- `Lotto`의 패키지 변경은 가능하다.

```java
public class Lotto {
    private final List<Integer> numbers;

    public Lotto(List<Integer> numbers) {
        validate(numbers);
        this.numbers = numbers;
    }

    private void validate(List<Integer> numbers) {
        if (numbers.size() != 6) {
            throw new IllegalArgumentException();
        }
    }

    // TODO: 추가 기능 구현
}
```
<BR>

✏️*기울어진 글씨는 저의 판단이 추가된 부분입니다.*
### 활용 사항
* *로또 번호를 입력 받아 저장하고 유효성을 확인하는 클래스로 사용*
* [x] *1. String 입력*
  * *활용경우 : 사용자에게 당첨 번호를 입력 받아 유효성을 확인*
    <BR><BR>
  * *검사 항목*
    1. 빈 값이 아닌지 확인
    2. 숫자인지 확인
    3. 6개의 숫자인지 확인
    4. 모든 숫자가 1 ~ 45 사이의 값인지 확인
    5. 중복 값이 없는지 확인

* [x] *2. List<Integer> 입력*
  * *활용 경우 : LottoMachine을 통해 랜덤으로 생성된 로또 번호의 유효성을 확인한다*
    <BR><BR>
  * *검사 항목*
    1. 6개의 숫자인지 확인
    2. 모든 숫자가 1 ~ 45 사이의 값인지 확인
    3. 중복 값이 없는지 확인

* [x] *공통된 검사항목*
  <BR><BR>
  * 하나의 함수로 묶기
    * 6개의 숫자인지 확인
    * 모든 숫자가 1~45 사이의 값인지 확인
    * 중복 값이 없는지 확인

****
##  기능에 따른 분류
### 1. LottoMachine
*: 조건에 부합하는 로또 번호를 랜덤으로 생성해 주는 클래스*
* [x] 조건에 부합하는 로또 번호 생성 -> 구매자가 구매하는 로또 번호 생성
  * 1~45 사이의 값으로 이루어져야 한다.
  * 중복된 값이 존재해서는 안된다.
* [x] 생성되 번호는 오름차순으로 정렬된다.
<BR><BR>
### 2. InputView
*: 사용자가 로또에서 입력해야 하는 메서드들을 모아둔 클래스*
* [x] 로또 구매 금액 입력
* [x] 로또 당첨 번호 입력
* [x] 로또 보너스 번호 입력
<BR><BR>
### 3. OutputView
* [x] 구매한 로또 번호 출력
  * 오름차순으로 정렬된 자동번호 출력
* [x] 당첨 내역 출력
  * 일치한 개수에 따른 금액과 당첨된 로또 개수 출력
* [x] 총 수익률 출력
  * 수익률은 소수점 둘째 자리에서 반올림하여 출력
<BR><BR>
### 4. LottoData
* [x] 로또 데이터를 관리하는 큻래스
  * Java Enum을 활용한다.
  * 로또 당첨 내역에 관한 데이터 관리
    * 맞힌 번호의 개수에 따른 등수와 상금 처리
<BR><BR>
### 5. PurchaseLotto
*: 사용자가 구매한 로또 번호를 자동으로 생성하고 저장해 주는 클래스*
* [x] LottoMachine 클래스를 통해 구매 수량만큼의 로또 생성
* [x] 생성한 로또 저장
<BR><BR>
### 6. PurchaseAmount
*: 구매금액으로 사용자가 입력한 로또 구매 금액을 저장, 유효성을 검사하는 클래스*
* [x] 입력값 유효성 검증
  ```
  - 숫자인지 체크
  - 0을 초과하는지 체크
  - 1000을로 나누어 떨어지는지 체크

  # 만약 유효성 검사 실패시 #
  - 입력 값이 없거나 숫자가 아닌 경우
    : [ERROR] 금액을 숫자로 정확히 투입해 주셔야 합니다.
  - 0이하의 값을 입력한 경우
    : [ERROR] 0원을  초과한 금액을 투입해 주셔야 합니다.
  
  - 1000원으로 나누어 떨어지지 않는 경우
    : [ERROR] 입력 금액의 단위는 1,000원 단위여야 합니다.
  ```
* [x] 구매 금액 저장
* [x] 구매 금액에 따른 로또 구매 개수 계산
* [x] 구매 로또 개수 저장
<BR><BR>
### 7. Lotto
*: 입력받은 로또 당첨 번호를 저장하고, 유효성을 검증하는 클래스*
*[x] 입력값 유효성 검증
  * 1. 입력된 값이 쉼표로 구분된 6개의 값인지 확인
  * 2. 모든 값이 숫자인지 확인
  * 3. 모든 값이 1~45 사이의 값인지 확인
  * 4. 중복되는 값이 없는지 확인
 ```
  # 만약 유효성 검사 실패시 #
 - 입력 값이 없거나 6개의 값이 아닌경우
   : [ERROR] 6개의 값을 쉼표로 구분하여 입력해주어야 합니다.
 - 숫자가 아닌 값이 있는 경우 
   : [ERROR] 1~45 사이의 숫자를 입력하셔야 합니다.
 
 - 1~45 사이의 값이 아닌 값이 있는 경우
   : [ERROR] 1~45 사이의 값을 입력해주십시오.
   
 - 중복된 값이 있는 경우
   : [ERROR] 서로 다른 값을 입력해야 합니다. 
 ```
*[x] 당첨 번호 저장
*[x] 당첨 입력 값을 List 형태로 저장
<BR><BR>
### 8. BonusNumber
*: 입력 받은 보너스를 저장하고, 보너스 번호에 대한 유효성을 검증하는 클래스*
*[x] 보너스 번호 저장
*[x] 입력된 보너스 번호에 대한 유효성 검증
  1. 값이 존재하는지 확인
  2. 구분 문자가 있는지 확인
  3. 숫자인지 확인
  4. 1~45 사이의 숫자인지 확인
  5. 로또 당첨번호와 중복되지 않은 깂인지 확인
*[x] 유효성 검증 실패 시 오류 메세지 출력
 ```
  - 값이 없거나 숫자가 아닌 경우
    : [ERROR] 1~45 사이의 값을 입력해야 합니다.
  - 구분 문자가 존재하여 값이 둘 이상일 경우
    : [ERROR] 1~45 사이의 값을 하나만 입력해야 합니다.
  - 1~45 사이의 값이 아닌 경우
    : [ERROR] 1~45 사이의 값을 입력해야 합니다.
  - 당첨 번호와 번호가 중복된 경우
    : [ERROR] 당첨번호와 번호가 중복됩니다. 당첨번호에 없는 번호를 입력하세요.
 ```
<BR><BR>
### 9. WinningResultCalculator
*: 당첨 결과 계산기로,당첨 내역 개수와 수익률에 대해 계산하고,저장하는 클래스*
*[x] 당첨 내역 초기화
*[x] 당첨 번호와 사용자 번호 비교
  * 당첨 번호와 사용자 선택 번호의 공통된 값의 개수를 체크
  * 보너스 번호와 일치하는 값이 있는지 확인
*[x] 당첨 내역 개수 계산
  * 1~5등 당첨 개수 체크
*[x] 당첨 결과 저장
*[x] 당첨 금액 저장
*[x] 총 수익률 계산
  * 수익률 계산 : ((당첨 금액) / (구매 금액)) * 100
  * 수익률은 소수점 둘째 자리에서 반올림
*[x] 총 수익률 계산
<BR><BR>
### 10. LottoStore
*: 로또 미션의 전체적인 기능을 관리하는 클래스*
*[x] 로또 구매
*[x] 로또 번호 알려주기
*[x] 당첨 번호 입력
*[x] 보너스 번호 입력
*[x] 당첨 통계 보여주기 
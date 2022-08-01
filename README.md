# YK2P
- 아이디어를 공유하는 장소입니다.

# 8, 9월 스터디 계획 
- 각자 스터디 공부 (2시간 대여 기준, 25분 5분)
- 각자 1주일 동안 공부한 내용, 공유 해주기 
- 각자 블로그, github, notion 편한대 정리해서 흔적 남겨놓기 
- 매주 월요일, (8시 10시 고정)

```swift
protocol AccountPasswordChangerType {
    
    var nowPw: String? { get }
    var newPw: String? { get }
    var newPwConfirm: String? { get }
    
    var isValidNewPw: Bool { get }
    var isValidNewPwConfirm: Bool { get }
    
    var nowPwError: String? { get }
    var newPwError: String? { get }
    var newPwConfirmError: String? { get }
}
```

# YK2P

## 8, 9월 스터디 계획 
- 각자 1주일 동안 공부한 내용, 공유 해주기 
- 각자 블로그, github, notion 편한대 정리해서 흔적 남겨놓기 (지금 Repo에 적용)
- 매주 월요일, (8시 10시 고정)
- 각자 스터디 공부 2명씩 진행, 30 ~40분 잡고 -> 남은 시간 아이디어 회의 (프로젝트)

> Exmple (코드로 사용 하는 방법)
- [마크다운 사용방법](https://github.com/YuGeonHui/YK2P/blob/main/%EB%A7%88%ED%81%AC%EB%8B%A4%EC%9A%B4%20%EC%82%AC%EC%9A%A9%20%EB%B0%A9%EB%B2%95.md)
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

## 10월 이후 (프로젝트) 
- 2주 단위 스크림 진행, 1주마다 회의진행 각자 팀 상황 보고 

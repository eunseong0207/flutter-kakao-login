카카오
84c16916e633fba6e3ebe130dff8fcfc

## Firestore 빌드 속도 빠르게

- 원인 : colud_firestore 패키지 설치 후 실행하면 iOS 네이티브 패키지가 설치됨
- iOS 네이티브 패키지는 C++ 이란 언어로 500,000줄 이상으로 작성됨
- 이 코드들을 기계어로 번역하는 과정이 매우 오래 걸림

### 해결방법
- (https://github.com/invertase/firestore-ios-sdk-frameworks)
- 위 레포지토리에서 이미 번역된 네이티브 패키를 제공함
- 아래의 내용을`Podfile`
---

```
target 'Runner' do
    use_frameworks!
```
---

여기에 붙여 넣기

---
```
target 'RunnerTests' do
    inherit! :search_paths
  end
end
```
---
  
  ```pod 'FirebaseFirestore', :git => 'https://github.com/invertase/firestore-ios-sdk-frameworks.git', :tag => '10.19.0'```

---
실행 후 에러 나면 > Firebase Core와 버전 맞추기
터미널에서 ios 폴더로 이동 후 `pod install --repo-update` 실행해서 패키지 업데이트 하면서 받아오기
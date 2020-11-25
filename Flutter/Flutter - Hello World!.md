## Hello World! Flutter

> [Flutter 공식문서](https://flutter-ko.dev/docs/get-started/install)를 기반으로 Flutter 설치 및 IOS, Android 앱을 만들 수 있는 환경설정까지 진행하면서 공부하고, 겪은 일들을 정리한 문서입니다. (=== 뇌피셜 지뢰밭🤫)
>
> 세부적인 부분은 공식문서에 자세히 나와있으니 공식문서와 함께 보는 것을 추천합니다.
>
> `flutter doctor` 명령어를 통해 설치해야 하는 것들을 확인하면서 진행하면 좋습니다.

### What is Flutter ?

+ 공식 문서에서는 Flutter를 다음과 같이 설명하고 있다. *Flutter는 하나의 코드베이스로 모바일, 웹, 데스크톱에서 네이티브로 컴파일 되는 구글의 아름다운 UI 툴킷입니다.*
+ 모바일 네이티브 앱? 우리가 흔히 알고 있는 모바일 어플리케이션. 안드로이드와 IOS와 같은 플랫폼에서 제공하는 SDK와 요구하는 프로그래밍 언어(JAVA, Swift 등)를  이용해 만들게 된다.
+ 이렇게 각 플랫폼별로 어플리케이션을 만들게 되면 비용도 늘어나고, 플랫폼에 종속되는 한계가 있다.
+ Flutter는 Dart라는 프로그래밍 언어를 이용해 개발을 하게 되며, 하나의 코드베이스에서 IOS나 Android, 웹과 데스크톱 애플리케이션까지. 여러 플랫폼의 앱을 개발할 수 있게하는 크로스 플랫폼 앱 개발 프레임워크이다.
+ 사실 공부하면서 웹이나 데스크톱 앱도 대응한다는 사실을 알게 되었는데, 대부분 IOS와 Android 네이티브 앱을 만들기 위해 사용하는 경우가 많은 것 같다.
+ 구글에서 제작한 오픈소스 프레임워크라는 점(최소한 Android만큼은 제대로 대응이 되지 않을까?), 뛰어난 UI, VS Code와 같이 일반적으로 사용하는 환경에서 개발이 가능하다는 장점이 있다.

### Xcode 설치

+ Xcode는 IOS 앱 개발 공식 IDE이며, 반드시 Mac OS에서만 사용 가능하다. (용량이 생각보다 엄청 크다)
+ IOS 가상 모바일 기기(에뮬레이터)를 사용하려면 Xcode를 설치해야 한다. 
+ 설치는 공식문서를 참고하자. 아주 자세히 설명하고 있다.
+ 설치가 완료되면 `$ open -a Simulator` 명령어로 iOS 에뮬레이터를 실행할 수 있다.

#### CocoaPods 설치(오류 해결)

> *Flutter 앱을 실제 iOS 기기에 배포하려면 서드 파티 CocoaPods 의존성 관리자와 Apple 개발자 계정이 필요합니다. 또한, Xcode에서 실제 기기 배포 설정을 해야합니다. - 공식문서*

사실 공식문서를 아무 생각없이 따라 내려가다 보니 설치까지 진행하게 되었는데, 

`sudo gem install cocoapods` 명령어로 실행하자 다음과 같은 오류 메시지가 뜨기 시작했다.

```
Building native extensions. This could take a while...
ERROR:  Error installing cocoapods:
	ERROR: Failed to build gem native extension.

    current directory: /Library/Ruby/Gems/2.6.0/gems/ffi-1.13.1/ext/ffi_c
/System/Library/Frameworks/Ruby.framework/Versions/2.6/usr/bin/ruby -I /System/Library/Frameworks/Ruby.framework/Versions/2.6/usr/lib/ruby/2.6.0 -r ./siteconf20201125-39485-nb9u3y.rb extconf.rb
checking for ffi.h... *** extconf.rb failed ***
Could not create Makefile due to some reason, probably lack of necessary
libraries and/or headers.  Check the mkmf.log file for more details.  You may
need configuration options.

Provided configuration options:
	--with-opt-dir
	--without-opt-dir
	--with-opt-include
	--without-opt-include=${opt-dir}/include
	--with-opt-lib
	--without-opt-lib=${opt-dir}/lib
	--with-make-prog
	--without-make-prog
	--srcdir=.
	--curdir
	--ruby=/System/Library/Frameworks/Ruby.framework/Versions/2.6/usr/bin/$(RUBY_BASE_NAME)
	--with-ffi_c-dir
	--without-ffi_c-dir
	--with-ffi_c-include
	--without-ffi_c-include=${ffi_c-dir}/include
	--with-ffi_c-lib
	--without-ffi_c-lib=${ffi_c-dir}/lib
	--enable-system-libffi
	--disable-system-libffi
	--with-libffi-config
	--without-libffi-config
	--with-pkg-config
	--without-pkg-config
/System/Library/Frameworks/Ruby.framework/Versions/2.6/usr/lib/ruby/2.6.0/mkmf.rb:467:in `try_do': The compiler failed to generate an executable file. (RuntimeError)
You have to install development tools first.
	from /System/Library/Frameworks/Ruby.framework/Versions/2.6/usr/lib/ruby/2.6.0/mkmf.rb:585:in `block in try_compile'
	from /System/Library/Frameworks/Ruby.framework/Versions/2.6/usr/lib/ruby/2.6.0/mkmf.rb:534:in `with_werror'
	from /System/Library/Frameworks/Ruby.framework/Versions/2.6/usr/lib/ruby/2.6.0/mkmf.rb:585:in `try_compile'
	from /System/Library/Frameworks/Ruby.framework/Versions/2.6/usr/lib/ruby/2.6.0/mkmf.rb:1109:in `block in have_header'
	from /System/Library/Frameworks/Ruby.framework/Versions/2.6/usr/lib/ruby/2.6.0/mkmf.rb:959:in `block in checking_for'
	from /System/Library/Frameworks/Ruby.framework/Versions/2.6/usr/lib/ruby/2.6.0/mkmf.rb:361:in `block (2 levels) in postpone'
	from /System/Library/Frameworks/Ruby.framework/Versions/2.6/usr/lib/ruby/2.6.0/mkmf.rb:331:in `open'
	from /System/Library/Frameworks/Ruby.framework/Versions/2.6/usr/lib/ruby/2.6.0/mkmf.rb:361:in `block in postpone'
	from /System/Library/Frameworks/Ruby.framework/Versions/2.6/usr/lib/ruby/2.6.0/mkmf.rb:331:in `open'
	from /System/Library/Frameworks/Ruby.framework/Versions/2.6/usr/lib/ruby/2.6.0/mkmf.rb:357:in `postpone'
	from /System/Library/Frameworks/Ruby.framework/Versions/2.6/usr/lib/ruby/2.6.0/mkmf.rb:958:in `checking_for'
	from /System/Library/Frameworks/Ruby.framework/Versions/2.6/usr/lib/ruby/2.6.0/mkmf.rb:1108:in `have_header'
	from extconf.rb:10:in `system_libffi_usable?'
	from extconf.rb:42:in `<main>'

To see why this extension failed to compile, please check the mkmf.log which can be found here:

  /Library/Ruby/Gems/2.6.0/extensions/universal-darwin-19/2.6.0/ffi-1.13.1/mkmf.log

extconf failed, exit code 1

Gem files will remain installed in /Library/Ruby/Gems/2.6.0/gems/ffi-1.13.1 for inspection.
Results logged to /Library/Ruby/Gems/2.6.0/extensions/universal-darwin-19/2.6.0/ffi-1.13.1/gem_make.out
```

구글링해보니 xcode 커멘드 도구를 설치하면 해결된다는 글이 가장 많았는데,

```
xcode-select --install
sudo gem install -n /usr/local/bin cocoapods
```

+ 정작 나는 이 명령어로 해결되지가 않았다.
+  `Ruby` 도 새로 깔아보고, `libffi`도 깔아봤는데 문제해결이 안됐는데, 혹시 몰라서 homebrew로 설치해봤는데 다행히 난 여기서 문제 해결 🙏
+ `brew install cocoapods --build-from-source`

### Android Studio 설치

+ Android Studio는  안드로이드 앱 개발 공식 IDE이다. 안드로이드 모바일 가상머신를 구동하기 위해 설치해야한다.

+ [안드로이드 스튜디오](https://developer.android.com/studio) 에서 다운로드

+ 설치 후 Configure -> ADV Manager에서 가상 머신 추가

### VS Code 익스텐션 설치

+ Flutter 검색 후 설치하면 된다.

### ![익스텐션](/Users/soohyuncho/Desktop/익스텐션.png)

Flutter 익스텐션을 설치하면 Dart 플러그인도 함께 설치된다.

### 프로젝트 생성 및 실행

+ `flutter doctor` 실행 시 다음과 같이 표시될 때까지 설정해준다. (에디터 - VS Code 사용 기준)

![](https://images.velog.io/images/harrycod/post/c5bd8aba-b83f-4480-92ff-4162cf30f6e0/doctor.png)

+ `flutter create [원하는 프로젝트 명]` 명령어로 새 프로젝트를 생성해 준다.
+ 생성된 프로젝트로 이동한 다음 실행한 가상머신에서 프로젝트를 실행해 볼 수 있다.

1. `flutter run`으로 실행하는 방법 

   ![](https://images.velog.io/images/harrycod/post/596f78f4-af9d-495c-8316-07bbdcd7f108/run.png)

   + 안드로이드와 IOS 가상 머신을 모두 실행 중이면 둘 중 하나를 선택할 수 있다.

     ![](https://images.velog.io/images/harrycod/post/90e6ebec-ae3f-407d-b4c9-427c1bb5a35f/run%20%E1%84%80%E1%85%AE%E1%84%83%E1%85%A9%E1%86%BC.png)

   + 아이폰을 선택해줬더니 아이폰 가상 머신에 생성한 프로젝트 화면이 띄워졌다 :)

2. VScode에서 실행하는 방법 ( 추천 )

   + 우선 VScode로 생성한 프로젝트를 열어준 다음, 오른쪽 하단의 No device를 클릭.

   + 지금 실행하고 있는 가상머신이 없어서 No Device로 뜨고 있는데, 가상머신을 실행하면 Device명이 뜨게 된다.

     ![](https://images.velog.io/images/harrycod/post/7c9824f5-a09b-4e06-96b0-fe2038c1f6a7/vscode%20%E1%84%92%E1%85%A1%E1%84%83%E1%85%A1%E1%86%AB.png)

   + 기기 선택 후, `F5`로 눌러서 debugging 시작하면

     ![](https://images.velog.io/images/harrycod/post/7507f0a6-a523-4014-a214-0bc32aab76d2/%E1%84%89%E1%85%AE%E1%84%8C%E1%85%A5%E1%86%BC%20%E1%84%8C%E1%85%A5%E1%86%AB.png)

   + 디버깅이 실행되면서 가상 머신에 다음과 같이 표시되게 된다.

     ![](https://images.velog.io/images/harrycod/post/ac455fbf-9e34-4446-810b-21bd565a91e5/%E1%84%89%E1%85%AE%E1%84%8C%E1%85%A5%E1%86%BC%20%E1%84%92%E1%85%AE.png)

   + 코드를 바꾸고 저장하면 실시간으로 변화된 화면이 뜨게 된다.(핫 리로딩 기능 개꿀)

   + 물론 안드로이드도 잘 실행 된다.

### 마무리

+ 처음 설치할 때 용량도 크고, IOS와 안드로이드를 모두 대응해야하다보니 설정할 것들이 생각보다 많았다. 
+ 그래도 전부 설정하고 Hello World까지 띄어보고 나니 조금은 익숙해진 느낌이 들었다.
+ 핫리로드 기능은 정말 좋았다.
+ 다음 번에는 Flutter를 이용해서 간단한 앱을 만들어 봐야겠다.
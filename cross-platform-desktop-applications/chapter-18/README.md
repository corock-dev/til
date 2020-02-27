# 18.

## 18.2 macOS 전용 일렉트론 애플리케이션 실행 파일 만들기

일렉트론은 macOS에서 애플리케이션 실행 파일을 만들 때 사용할 수 있는 다양한 npm 모듈을 제공합니다.

`electron-builder` 모듈은 설치 전용 UX 등도 제공합니다.



```bash
npm i electron-builder --save-dev
```



`electron-builder` 를 설치했다면, 애플리케이션의 `package.json` 파일에 다음과 같은 필드가 제대로 설정되어 있는지 확인해야 합니다.

-   name
-   version
-   author
-   description



이러한 항목을 package.json에 설정했다면, 다음과 같이 빌드 관련 구성을 추가합니다.

```json
{
  "name": "hello-world",
  "version": "0.0.1",
  "main": "main.js",
  "description": "A hello world application for Electron",
  // .app과 .dmg 파일을 만들 때 사용할 스크립트를 추가합니다.
  "scripts": {
    "pack": "node_modules/.bin/build",
    "dist": "node_modules/.bin/build"
  },
  // 빌드 관련 설정을 추가합니다.
  "build": {
    "mac": {
      "title": "Hello World",
      "icon": "icon.icns",
      "background": "background.png",
      "icon-size": 80,
      "contents": [
        {
          "x": 448,
          "y": 220,
          "type": "link",
          "path": "/Applications"
        },
        {
          "x": 192,
          "y": 220,
          "type": "file",
          "path": "dist/hello-world-darwin-x64/hello-world.app"
        }
      ]
    }
  },
  "devDependencies": {
    "electron-builder": "^13.5.0",
    "electron": "1.4.15"
  }
}
```



-   `npm run pack`: 애플리케이션 소스 코드를 기반으로 스탠드얼론으로 실행할 수 있는 .app 파일을 생성합니다.
-   `npm run dist`: 아래와 같은 역할을 합니다.
    -   사용자가 컴퓨터에 애플리케이션을 설치할 때 사용할 수 있는 .dmg 파일을 생성합니다.
    -   Squirrel을 기반으로 애플리케이션을 자동으로 업데이트할 때 활용되는 mac.zip 파일을 생성합니다.
















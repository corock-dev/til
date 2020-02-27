# 7. 데스크톱 애플리케이션의 화면 출력 제어하기

## 7.1 화면의 크기와 모드

### 7.1.1 NW.js 에서 화면 크기 설정하기



### 7.1.2 일렉트론에서 화면 크기 설정하기

NW.js 가 `package.json` 을 사용해서 화면의 크기를 설정하는 것과 다르게, 일렉트론은 **애플리케이션 화면을 초기화할 때** 화면의 크기를 지정합니다.



**main.js**

```javascript
app.on('ready', () => {
  // 너비와 높이를 설정하는 부분
  mainWindow = new BrowserWindow({ width: 400, height: 200 });
  mainWindow.loadURL(`file://${__dirname}/index.html`);
  mainWindow.on('closed', () => { mainWindow = null; });
});
```



### 7.1.4 일렉트론에서 화면의 너비와 높이 제한하기

일렉트론에서 화면의 너비와 높이를 제한할 때는 `BrowserWindow` 객체를 사용합니다.

예를 들어 너비를 300px, 높이를 150px 보다 크게, 너비를 600px, 높이를 450px 보다 작게 제한하고 싶을 때는 다음과 같은 형태로 BrowserWindow 인스턴스를 생성합니다.

```javascript
let mainWindow = null;

(...)

mainWindow = new BrowserWindow({
  width: 400, height: 200,
	minWidth: 300, minHeight: 150,
	maxWidth: 600, maxHeight: 450
});
```



디폴트로 일렉트론은 애플리케이션을 화면의 중앙에 출력합니다. 만약 화면의 특정한 위치에 애플리케이션을 배치해서 실행하고 싶다면, `BrowserWindow` 객체를 생성할 때 `x` 와 `y` 라는 속성을 지정합니다.

```javascript
mainWindow = new BrwoserWindow({
  width: 400, height: 800,
  x: 10, y: 10
});
```





## 7.2 프레임리스 화면과 전체 화면

공항 또는 은행처럼 많은 사람들이 사용할 수 있는 곳에 설치되어 있는 데스크톱 애플리케이션을 키오스크(kiosk) 애플리케이션이라고 부릅니다. 키오스크 애플리케이션은 사용자들이 애플리케이션을 벗어나서 컴퓨터를 가지고 게임을 하지 못하게 하는 애플리케이션을 의미합니다.



### 7.2.2 일렉트론의 전체 화면

`BrowserWindow` 인스턴스를 생성할 때, 전체 화면과 관련된 설정을 지정할 수 있습니다. 만약 일렉트론 애플리케이션이 처음 시작할 때부터 전체 화면으로 실행되게 하고 싶다면, BrowserWindow 인스턴스를 생성할 때 다음과 같이 입력합니다.

```javascript
mainWindow = new BrowserWindow({ fullscreen: true });
```



일렉트론은 `remote` 라는 API를 사용해서 프런트엔드에서 백엔드를 호출할 수 있습니다.

`remote` API 덕분에 렌더러 프로세스(프런트엔드)에서 메인 프로세스(백엔드)로 메시지를 보낼 수 있으며, `BrowserWindow` 인스턴스를 추출하고 상호작용할 수 있는 것입니다.



## 정리

-   [x] 애플리케이션 화면을 특정한 너비와 높이를 주고 생성할 수 있습니다.
-   [x] 애플리케이션 화면의 크기를 사용자가 따로 조절하지 못하게 만들 수 있습니다.
-   [x] 애플리케이션을 전체 화면 모드로 만드는 것은 굉장히 쉽습니다.
-   [x] 애플리케이션 화면의 프레임을 제거하면, 프레임리스 애플리케이션을 만들 수 있습니다.
-   [x] 프레임리스 애플리케이션을 만들 때는 화면 드래그와 관련된 내용에 주의하세요.
-   [x] 공공장소에서 사용되는 ATM 애플리케이션 등에는 키오스크 모드를 활용하세요.


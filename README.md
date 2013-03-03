Alloy Widget
============

Alloy Widget 위젯 설치 방법과 위젯 샘플 모음

## Widget이란?

* [위키백과] (http://ko.wikipedia.org/wiki/%EC%9C%84%EC%A0%AF)
  * **위젯엔진** - 위젯 엔진(widget engine)은 PC에서 웹 브라우저를 대신하는 개인화된 프로그램을 띄워주는 소프트웨어 시스템이다. 대표적으로 OS X의 대시보드, 야후 위젯, 미니플, 네이버 데스크톱, 구글 데스크톱이 있다.
	* **GUI 위젯** - 컴퓨터 프로그래밍에서 위젯(widget) 또는 컨트롤(control)은 컴퓨터 사용자가 상호 작용하는 인터페이스 요소이다.
* [용어사전] (http://terms.co.kr/widget.htm)
	컴퓨터에서의 widget은 정보를 나타내거나, 운영체계 및 응용프로그램 등과 상호 작용하려는 사용자를 위해 특유한 방법을 제공하는 GUI 구성요소이다.
* 기타	
	* **[위젯이란?](http://lumirent.net/wp/?p=20)** 

## Alloy Widgets
[Alloy Widgets 도큐먼트 링크](http://docs.appcelerator.com/titanium/latest/#!/guide/Alloy_Widgets-section-35621514_AlloyWidgets-UsingWidgets) 

### Introduction 

Widgets are self-contained components that can be easily dropped into Alloy-powered Titanium projects.
They were conceived as a way to reuse code in multiple applications or to be used multiple times in the same application. 
Widgets have their own views, controllers, styles and assets and are laid out the same as the app directory in the Alloy project.

```
위젯은 Alloy로 개발되는 Titanium 프로젝트에 쉽게 장착할수 있는 독립적인 컴포넌트이다. 
Alloy 위젯은 단일 어플리케이션 내에서의 반복된 코드, 또는 멀티 어플리케이션에서 코드의 재활용의 개념으로 시작되었다.
위젯은 Alloy 프로젝트의 app 디렉토리와 동일하게 views, controllers, styles, assets 디렉토리를 가진다.
또한 필요시 lib, theme 등의 디렉토리도 가질수 있다. 
```

### Using Widgets

1. 사용하고자 하는 곳에 Require 태그로 `type:widget`, `src:위젯명`, `id:코딩 사용 id`로 지정한다.
```
<Alloy>
    <Window id="win">
        <Require type="widget" src="com.appcelerator.searchForBooks" id="sfb"/>
        <TableView id="table"/>
    </Window>
</Alloy>
```
`<Require type="widget" src="com.appcelerator.searchForBooks" id="sfb"/>`

2. config.json 파일을 열어 ddependencies 부분을 추가한다.
```
"dependencies": {
        "com.appcelerator.searchForBooks":"1.0"
    }
````

### Widget Element 사용

Require 대신 Widget으로 사용한다. require와 기능적으로 동일하다. 적용 방법도 동일하다.
```
<Alloy>
    <Window id="win">
        <Widget src="com.appcelerator.searchForBooks" id="sfb"/>
        <TableView id="table"/>
    </Window>
</Alloy>
```

### Widget 만들기
1. App 또는 Project Explorer에서 마우스 클릭 -> Alloy Widget 선택
2. Widget 이름 입력 -> 만들기
3. `/app/widgets/WidgetName`으로 폴더 자동생성 됨
4. view, tss, controller, .... 작성


### Widget 구조
	view : widget.xml
	styles : widget.tss
	controller : widget.js
	

### Controller에서 Widget 호출 
View에서 정의되지 않은 Widget을 호출할때 Alloy.createWidget 메소드를 이용한다.
```
var loadIcon = Alloy.createWidget("com.appcelerator.loading");
win.add(loadIcon);


var button = Alloy.createWidget('foo', 'button').getView();
$.widget.add(button);

```

createWidget 메소드
```
createWidget( String id, String name, [*... args] ) : Alloy.Controller
Factory method for instantiating a widget controller. Creates and returns an instance of the named widget.

Parameters
id : String
	Id of widget to instantiate.

name : String
	Name of the view within the widget to instantiate ('widget' by default)
args : *... (optional)
	Arguments to pass to the widget.

Returns
Alloy.Controller
	Alloy widget controller object.
```

View에 Widget을 정의했을때 실제로는 createWidget 메소드를 사용하여 resourse에 생성된다.

그러므로 Tag 정의에 해당 프로퍼티의 값을 정해서 넘겨주면 Widget의 propertiy 값을 생성하거나 이용할 수 있다.

```
<controller>
	exports.init = function (args) {
	    // Button object with id=button
	    $.button.title = args.title || 'Si'; 
	    $.button.color = args.color || 'black'; 
	    // global variable
	    message = args.message || 'Hola mundo';
	}

<프로젝트 내 view에서 위젯 호출>
	$.foo.init({title:'Yes', color:'gray', message:'I pity the foo.'});
```

### Alloy Widget 사용시 고려사항

[* Alloy widgets vs JS controllers assets/lib]( http://developer.appcelerator.com/question/142670/alloy-widgets-vs-js-controllers-assetslib ) 

```
위젯은 기본적으로 UI를 갖는 경우에 사용, UI가 없는 기능성의 경우 lib/로 지정하고 사용 권장.
Tony Lukasavage answered a similar question for me on the Google Group for Alloy:
"If the code has no associated markup or tss styling, then yes, a commonjs module in app/lib would be the right choice"

```





여기서 이렇게 이미지가 보인다. ![iOS Drawer Closed](https://github.com/rifi/alloy/raw/master/test/apps/widgets/widget_drawer/docs/img/ios_closed.png)   


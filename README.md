## 개발 참고 가이드 ()
```
스타일 및 테마 적용시 반드시 아래 사이트에서 확인 후 우선 적용 하시기 바랍니다.
http://full___.04___be.com
common.js -> 공통 스크립트
master.scss -> 공통 스타일
/app/http/common.lib.php -> 공통 php 함수

[서버구성]
centos7.3.x
apache 2.4.x
php 7.3.11 이상
mysql 5.7.x

laravel 5.7.x 사용
```

## Installation Guideline

Composer로 라라벨 dependency 인스톨
 - version : 1.10.~ (최신 사용하면 안됨)
``` bash
composer install
```

node modules 인스톨

``` bash
npm install
```

.env 파일 작성후 Laravel 키 생성

``` bash
cp .env.example .env
php artisan key:generate
```

# 이미지 저장에 필요한 작업.
composer.json 의 require 항목에 다음 내용을 추가확이 하고 없으면 추가한다. 그리고 *composer update* 를 실행합니다.
``` bash
"require": {
    "intervention/image": "^2.5"
}
```
라라벨 파일 스토리지 사용.
``` bash
php artisan storage:link
```

# Laravel Excel 패키지를 사용
(참고 https://www.lesstif.com/pages/viewpage.action?pageId=29590459 )

*방법.1 (이미 등록된 composer를 사용시)*
1. *composer install* 를 실행합니다.

*방법.2 (composer에 처음 추가시)*
1. composer.json 의 require 항목에 다음 내용을 추가확이 하고 없으면 추가한다. 그리고 *composer update* 를 실행합니다.
``` bash
"require": {
    "maatwebsite/excel": "~2.1.0"
}
```
2. config/app.php 에 서비스 프로바이더와 파사드를 등록합니다.
``` bash

'providers' => [
    // provider 추가
    Maatwebsite\Excel\ExcelServiceProvider::class,
],
'aliases' => [
    // facade 추가
    'Excel' => Maatwebsite\Excel\Facades\Excel::class,
],
```
3. 기본 엑셀 설정을 퍼블리싱합니다. 이제 config/excel.php 에 설정 파일이 생성됩니다.
``` bash
php artisan vendor:publish
```

# socket chatting
```
참조 : https://modestasv.com/chat-with-laravel-pusher-and-socket-io-at-your-command/?utm_source=learninglaravel

composer require predis/predis

sudo npm install -g laravel-echo-server
sudo npm install socket.io
sudo npm install laravel-echo
sudo npm install --save socket.io-client

npm install redis --save-dev
npm install ioredis --save-dev
npm install vue-socket.io --save-dev

laravel-echo-server init
------- 화면 예시 ----
? Do you want to run this server in development mode? Yes
? Which port would you like to serve from? 6001
? Which database would you like to use to store presence channel members? redis
? Enter the host of your Laravel authentication server. http://localhost:8000
? Will you be serving on http or https? http
? Do you want to generate a client ID/Key for HTTP API? Yes
? Do you want to setup cross domain access to the API? Yes
? Specify the URI that may access the API: http://localhost:8000
? Enter the HTTP methods that are allowed for CORS: GET, POST
? Enter the HTTP headers that are allowed for CORS: Origin, Content-Type, X-Auth-Token, X-Requested-With, Accept, Autho
rization, X-CSRF-TOKEN, X-Socket-Id
? What do you want this config to be saved as? laravel-echo-server.json
appId: fb9e72802cace662
key: 9bf6eb178b5601e2353d387c9d46531b
--------- 화면 예시 끝 ------

laravel-echo-server client:appId
redis-server
laravel-echo-server start


.env 파일 수정
BROADCAST_DRIVER=redis

/config/app.php 수정
App\Providers\BroadcastServiceProvider::class, 앞에 주석 제거
```

# JWT 연동 사전작업
참고자료 : https://dev-yakuza.github.io/ko/laravel/jwt/
```
JWT 기본 테이블명 변경 시 해당 API 컨트롤러에 다음의 코드 필수
    public function __construct()
    {
        Config::set('jwt.user',Member::class);
        Config::set('auth.providers.users.model',Member::class);
    }

composer.json 에 추가
    "require": {
        "tymon/jwt-auth": "1.0.0-rc.3"
    },


 composer 업데이트
 composer update


 미들웨어 적용
 php artisan vendor:publish --provider="Tymon\JWTAuth\Providers\LaravelServiceProvider"


 JWT 암호화 키 생성
 php artisan jwt:secret
```

# 모든 설치 과정이 끝나면
```
npm run dev 실행
```

# 기타
``` bash
package-lock.json이 무결성 해시를 sha1에서 sha512로 변경 되는 문제가 있다면.

npm i -g npm
rm -rf node_modules/
npm cache clear --force
npm i
```

# CUBEONE DB 암호화 사용시
```
.env 파일 내 추가 구성
DB_SECURE=Y
```

# 세종텔레콤 사용시
```
.env 파일 내 추가 구성
SMS_USE=SEJONG
```

# 베스트페이 결제 모듈 사용
```
.env 파일 내 추가 구성
PAY_AGENT=Y
```

# 아마존 안면인식 사용
.env에 추가
``` bash
AWS_SECRET_ACCESS_KEY=
AWS_ACCESS_KEY_ID=
```

# QR URL 세팅
```
.env 파일에
QR_URL=http://qr.domain.co.kr/
```

# 휴면 세팅
```
.env 파일에
DB_HOST2=
DB_PORT2=
DB_DATABASE2=
DB_USERNAME2=
DB_PASSWORD2=

```

# 실서비스 서버에서 laravel-echo-server start를 상시 띄우는 법
```
[PM2 설치]
sudo npm install pm2 -g

[socket.sh 생성]
#!/usr/bin/env bash
laravel-echo-server start
:wq

[pm2 활용]
pm2 start socket.sh
pm2 list 해당 프로시저 등록 상태 확인
pm2 start *******
pm2 stop *******
pm2 restart *******
pm2 list *******
pm2 info *******
```

# table auto rowspan
```
$('table').rowspanizer({
  columns: [0,1,2]
});
```

# multiple select box
출처 및 예시 http://nicolasbize.com/magicsuggest/examples.html
```

<select name="male_count" class="selecttagbox w50">
    <option value="random">랜덤</option>
    <option value="odd">홀수 순</option>
    <option value="even">짝수 순</option>
    <option value="2x">2배수</option>
    <option value="5x">5배수</option>
</select>

$(function() {
    $('.selecttagbox').magicSuggest({
        placeholder: '임의로 수로 증가시 입력'
    });
});
```

# Bootstrap-select
출처 및 예시 https://developer.snapappointments.com/bootstrap-select/options/
```
<script>
    $(function () {
        $('.selectpicker').selectpicker({
        });
    });
</script>

<td class="text-align-center p0">
    <select  name="mode" class="selectpicker form-control" multiple data-actions-box="true">
        <option value="전화"  >전화</option>
        <option value="대행사"  >대행사</option>
        <option value="홈페이지" >홈페이지</option>
    </select>
</td>

동적으로 option 값 추가 필요할시
<select  name="mode" class="selectpicker form-control" data-live-search="true" editable="true">
```

# 마우스 오른쪽 버튼 클릭시 메뉴 만들기
출처 : https://swisnl.github.io/jQuery-contextMenu/demo.html

```
<script src="/js/libs/jquery-3.2.1.min.js"></script>
<link rel="stylesheet" href="/css/jquery.contextMenu.min.css">
<script src="/js/jquery.contextMenu.min.js"></script>
<script src="/js/jquery.ui.position.js"></script>

$.contextMenu({
    selector: '.locker_no',
    callback: function(key, options) {
        var m = key;
        //window.console && console.log(m) || alert(m);
        if(m == 'member') {
            alert('회원을 지정 합니다.');
        } else if(m=='delete') {
            alert('회원을 해제 합니다.');
        }
    },
    items: {
        "member": {name: "회원지정", icon: "member"},
        "delete": {name: "회원해제", icon: "delete"},
        "sep1": "---------",
        "quit": {name: "Quit", icon: function(){
                return 'context-menu-icon context-menu-icon-quit';
            }}
    }
});

$('.context-menu-one').on('click', function(e){
    console.log('clicked', this);
});

```

# swal
```
참고자료 : https://www.npmjs.com/package/sweetalert

/* 메세지 오픈 후 새로고침 처리시 */
swal(message, {
    icon: "success",
}).then(function(){
    location.reload();
});
```

# Datepick
```
참고자료 : http://keith-wood.name/datepick.html#
```

# event 만들기
```
let e = $.Event();
```

## ajax 중복클릭 방지 및 처리시 예시
```
$.ajaxSetup({
    headers: {
        'X-CSRF-TOKEN': $('meta[name="csrf-token"]').attr('content')
    }
});

e.preventDefault();

var url = '/reserve/guestDetail?res_id=' + row_id;

$.ajax({
    url: url,
    type: "POST",
    data: { },
    dataType: "json",
    beforeSend: function() {
        $("#loaderDiv").show();
    },
    success:function(data){
        $("#loaderDiv").hide();

        if(data.ret_code) {
            swal(data.ret_msg, {
                icon: "warning",
            });
            return false;
        }
        $("#reserve_guest_detail").html(data.html);

    },error:function(){
        warning( "처리에 실패하였습니다.", 'warning');
    }
});
```

# 안면인식 서버 종류 설정
```
기본값은 AWS
.env 파일 내 추가 구성
FACE_ENGINE_TYPE=LG
```

# LG 안면인식 서버 설정
```
.env 파일 내 추가 구성
LG_FACE_URL=https://domain/
LG_FACE_APP_KEY=7f2b25b5f9bfaee9
LG_FACE_SECRET_KEY=9e3679d0070e4084c19e0e1a194bf8ef
```

# 아마존 안면인식 사진등록 관련 collection과 bucket 설정
버킷명은 소문자와 - 만 사용 가능함.

그리하여 collection 과 bucket은 소문자와 - 로만 구성 필요
```
.env 파일 내 추가 구성
AWS_FACE_COLLECTION=deverp-golfpay-face-collection
AWS_FACE_BUCKET=deverp-golfpay-face
```

# SMS 발송처 한글, 영문 이름
```
.env 파일 내 추가 구성
sms_kor_name="땡땡CC"
sms_eng_name="XXX CC"
```
# Jquery Excel export
```
https://github.com/hhurz/tableExport.jquery.plugin
https://dodamit.tistory.com/44

Export HTML Table to
CSV
DOC
JSON
PDF
PNG
SQL
TSV
TXT
XLS (Excel 2000 HTML format)
XLSX (Excel 2007 Office Open XML format)
XML (Excel 2003 XML Spreadsheet format)
XML (Raw xml)
```

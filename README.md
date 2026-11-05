# jQuery Mobile 1.0 단계별 실습 — 추가되는 코드만 보기

업로드한 통합 HTML 코드를 단순히 하나씩 떼어내는 대신 **STEP 01→12 순서로 기능이 누적되는 독립 실행 HTML 파일**로 분리했습니다.
각 단계는 이전 단계 코드를 포함하므로, 순서대로 실행해 변화된 UI를 확인할 수 있습니다.
각 HTML 소스의 `<!-- [STEP xx] -->`, `/* [STEP xx] */`, `// [STEP xx]` 주석이 추가한 코드 위치를 나타냅니다.

## 공통 라이브러리 (12개 파일 동일)

```html
<link rel="stylesheet" href="https://code.jquery.com/mobile/1.0/jquery.mobile-1.0.min.css">
<script src="https://code.jquery.com/jquery-1.6.4.min.js"></script>
<script src="https://code.jquery.com/mobile/1.0/jquery.mobile-1.0.min.js"></script>
```

**주의:** 원본 코드의 `10_css.css`는 업로드되지 않았으므로, CSS를 각 HTML의 `<style>`에 포함했습니다. jQuery 1.6.4에서는 `.on()`이 아니라 `.bind()`를 사용합니다.

## STEP 01. 기본 페이지 구조

- **파일:** `01_basic_page.html`
- **핵심:** `data-role="page", data-role="header", data-role="content", data-role="footer"`
- **테스트:** header · content · footer 영역이 표시되는지 확인한다.

기본 HTML 파일을 열어 `<head>`에 CSS·JS를 연결하고 `<div data-role="page">` 안에 header / content / footer를 배치합니다.

## STEP 02. 라디오 버튼과 체크박스

- **파일:** `02_radio_checkbox.html`
- **핵심:** `input type="radio", input type="checkbox", data-role="controlgroup"`
- **테스트:** 수강 형태는 한 가지만, 관심 분야는 여러 개 선택되는지 확인한다.

**HTML (이번 단계에서 새로 추가하는 부분):**
```html
<h4>① 라디오 버튼과 체크박스</h4>
<div data-role="fieldcontain">
  <fieldset data-role="controlgroup">
    <legend>수강 형태(1개만 선택)</legend>
    <input type="radio" name="course" id="courseOnline" value="온라인" checked>
    <label for="courseOnline">온라인</label>
    <input type="radio" name="course" id="courseOffline" value="오프라인">
    <label for="courseOffline">오프라인</label>
  </fieldset>
</div>
<div data-role="fieldcontain">
  <fieldset data-role="controlgroup">
    <legend>관심 분야(복수 선택)</legend>
    <input type="checkbox" name="interest" id="interestAI" value="인공지능">
    <label for="interestAI">인공지능</label>
    <input type="checkbox" name="interest" id="interestWeb" value="웹 개발">
    <label for="interestWeb">웹 개발</label>
    <input type="checkbox" name="interest" id="interestSec" value="정보보호">
    <label for="interestSec">정보보호</label>
  </fieldset>
</div>
```

## STEP 03. 선택 메뉴(Select)

- **파일:** `03_select_menu.html`
- **핵심:** `<select>, <option>`
- **테스트:** 전공 선택 메뉴에서 다른 항목을 선택해 본다.

**HTML (이번 단계에서 새로 추가하는 부분):**
```html
<h4>② 선택 메뉴(Select)</h4>
<div data-role="fieldcontain">
  <label for="major">전공 선택</label>
  <select name="major" id="major">
    <option value="인공지능학과">인공지능학과</option>
    <option value="소프트웨어학과">소프트웨어학과</option>
    <option value="정보보호학과">정보보호학과</option>
  </select>
</div>
```

## STEP 04. 플립 스위치

- **파일:** `04_flip_switch.html`
- **핵심:** `select data-role="slider"`
- **테스트:** 알림 설정을 OFF와 ON으로 전환한다.

**HTML (이번 단계에서 새로 추가하는 부분):**
```html
<h4>③ 플립 스위치(Flip Switch)</h4>
<div data-role="fieldcontain">
  <label for="wifi">알림 설정</label>
  <select name="wifi" id="wifi" data-role="slider">
    <option value="OFF">OFF</option>
    <option value="ON">ON</option>
  </select>
</div>
```

## STEP 05. 숫자 슬라이더

- **파일:** `05_range_slider.html`
- **핵심:** `input type="range", .bind("change keyup", ...)`
- **테스트:** 볼륨을 움직이면 숫자 표시가 함께 변경되는지 확인한다.

**HTML (이번 단계에서 새로 추가하는 부분):**
```html
<h4>④ 숫자 슬라이더(Slider)</h4>
<div data-role="fieldcontain">
  <label for="volume">볼륨: <strong id="volumeText">50</strong></label>
  <input type="range" id="volume" name="volume" min="0" max="100" value="50">
</div>
```

**JavaScript (이번 단계에 추가):**
```javascript
// [STEP 05] range 값을 표시 (jQuery 1.6.4의 .bind 사용)
$("#volume").bind("change keyup", function () {
  $("#volumeText").text($(this).val());
});
```

## STEP 06. 텍스트·검색 폼

- **파일:** `06_text_search.html`
- **핵심:** `input type="text", input type="search"`
- **테스트:** 이름과 검색어를 입력하고 검색창의 지우기 동작을 확인한다.

**HTML (이번 단계에서 새로 추가하는 부분):**
```html
<h4>⑤ 텍스트와 검색 폼</h4>
<div data-role="fieldcontain">
  <label for="studentName">이름</label>
  <input type="text" id="studentName" name="studentName" placeholder="이름 입력">
</div>
<div data-role="fieldcontain">
  <label for="searchWord">검색어</label>
  <input type="search" id="searchWord" name="searchWord" placeholder="예: jQuery Mobile">
</div>
```

## STEP 07. 폼 입력 결과 확인

- **파일:** `07_form_result.html`
- **핵심:** `.val(), :checked, .each(), .text()`
- **테스트:** 입력 결과 확인 버튼을 눌러 현재 선택·입력 값 7항목을 출력한다.

**HTML (이번 단계에서 새로 추가하는 부분):**
```html
<!-- [STEP 07] 기존 폼에서 읽은 값을 출력 -->
<a href="#" id="btnResult" data-role="button" data-theme="b" data-icon="check">입력 결과 확인</a>
<div class="result" id="formResult" role="status" aria-live="polite">아직 입력 결과가 없습니다.</div>
```

**CSS (이번 단계에 추가):**
```css
/* [STEP 07] 수집한 입력 값 표시 */
.result { background:#f5f8fc; border:1px solid #d6e2ec; padding:11px 13px; border-radius:8px; white-space:pre-line; font-size:14px; min-height:45px; }
```

**JavaScript (이번 단계에 추가):**
```javascript
// [STEP 07] 폼에서 선택하거나 입력한 값을 한 번에 읽기
$("#btnResult").bind("click", function (e) {
  e.preventDefault();
  var interests = [];
  $("input[name='interest']:checked").each(function () {
    interests.push($(this).val());
  });
  var output = "수강 형태: " + ($("input[name='course']:checked").val() || "미선택") + "\n" +
               "관심 분야: " + (interests.length ? interests.join(", ") : "미선택") + "\n" +
               "선택 전공: " + $("#major").val() + "\n" +
               "알림 설정: " + $("#wifi").val() + "\n" +
               "볼륨: " + $("#volume").val() + "\n" +
               "이름: " + ($("#studentName").val() || "미입력") + "\n" +
               "검색어: " + ($("#searchWord").val() || "미입력");
  $("#formResult").text(output);
});
$("#studentForm").bind("submit", function (e) {
  e.preventDefault();
  $("#btnResult").trigger("click");
});
```

## STEP 08. 슬라이드 패널

- **파일:** `08_slide_panel.html`
- **핵심:** `.animate(), swiperight, swipeleft`
- **테스트:** 메뉴 열기·닫기, 바깥 영역 탭, 오른쪽/왼쪽 스와이프를 테스트한다.

**HTML (패널 마크업):**
```html
<!-- [STEP 08] 별도 플러그인이 아닌 CSS + 기본 jQuery로 패널 구현 -->
<div id="panelShade" aria-hidden="true"></div>
<nav id="sidePanel" aria-label="실습 사이드 메뉴">
  <h3>실습 목차</h3>
  <a class="panel-link" href="#forms">1. 폼 요소 5종</a>
  <a href="#" id="btnPanelClose" data-role="button" data-theme="b">메뉴 닫기</a>
  <p class="desc">화면을 오른쪽으로 스와이프하면 메뉴가 열리고, 메뉴에서 왼쪽으로 스와이프하면 닫힙니다.</p>
</nav>
```

**CSS (이번 단계에 추가):**
```css
/* [STEP 08] jQuery Mobile 1.0에 panel 위젯이 없으므로 직접 구현 */
#panelShade { display:none; position:fixed; inset:0; background:rgba(15,30,49,.46); z-index:1100; }
#sidePanel { position:fixed; left:-290px; top:0; height:100%; height:100vh; width:260px; padding:18px; background:#f8fbff; z-index:1101; border-right:1px solid #bdd5e9; box-shadow:4px 0 20px rgba(0,0,0,.18); overflow-y:auto; }
#sidePanel h3 { color:#173d68; margin-top:10px; }
#sidePanel .panel-link { display:block; padding:12px; margin-bottom:8px; border:1px solid #d2e2f0; border-radius:7px; background:#e8f2fc; color:#1d4c72; text-decoration:none; font-weight:bold; }
#sidePanel .panel-link:focus { outline:2px solid #247dbd; }
```

**JavaScript (이번 단계에 추가):**
```javascript
// [STEP 08] 패널 열기 / 닫기 / 목차 이동 / 스와이프
function openPanel() {
  $("#panelShade").show();
  $("#sidePanel").stop(true, true).animate({ left: "0px" }, 240);
  $("#btnPanelOpen").attr("aria-expanded", "true");
}
function closePanel() {
  $("#sidePanel").stop(true, true).animate({ left: "-290px" }, 240, function () {
    $("#panelShade").hide();
  });
  $("#btnPanelOpen").attr("aria-expanded", "false");
}
$("#btnPanelOpen").bind("click", function (e) {
  e.preventDefault();
  openPanel();
});
$("#btnPanelClose, #panelShade").bind("click", function (e) {
  e.preventDefault();
  closePanel();
});
$("#sidePanel .panel-link").bind("click", function (e) {
  e.preventDefault();
  var target = $(this).attr("href");
  closePanel();
  var section = $(target);
  if (section.length) {
    $("html, body").animate({ scrollTop: section.offset().top }, 350);
  }
});
$("#mainContent").bind("swiperight", function (e) {
  // 숫자 슬라이더와 입력 요소의 드래그 동작은 메뉴 제스처로 취급하지 않음
  if ($(e.target).closest(".ui-slider, input, select").length) return;
  openPanel();
});
$("#sidePanel").bind("swipeleft", function () { closePanel(); });
```

## STEP 09. 접이식 아코디언

- **파일:** `09_collapsible.html`
- **핵심:** `data-role="collapsible-set", data-role="collapsible"`
- **테스트:** HTML5/CSS3/jQuery Mobile 항목을 차례대로 펼쳐 본다.

**HTML (이번 단계에서 새로 추가하는 부분):**
```html
<section class="section" id="collapsible">
  <h3><span class="number">02</span>접이식 아코디언</h3>
  <p class="desc">jQuery Mobile 1.0 기본 위젯: <code>data-role="collapsible-set"</code></p>
  <div data-role="collapsible-set" data-theme="c" data-content-theme="c">
    <div data-role="collapsible" data-collapsed="false">
      <h3>HTML5란?</h3>
      <p>웹 문서의 제목, 문단, 입력 폼, 표 등 구조를 표현하는 표준 마크업 언어입니다.</p>
    </div>
    <div data-role="collapsible">
      <h3>CSS3란?</h3>
      <p>색상, 배치, 크기, 화면에 따른 반응형 스타일을 정의합니다.</p>
    </div>
    <div data-role="collapsible">
      <h3>jQuery Mobile이란?</h3>
      <p>모바일 화면에 맞는 터치 친화적인 UI를 제공하는 오래된 JavaScript UI 프레임워크입니다.</p>
    </div>
  </div>
</section>
```

## STEP 10. 팝업 대체 구현

- **파일:** `10_popup.html`
- **핵심:** `.fadeIn(), .fadeOut()`
- **테스트:** 팝업 열기·닫기와 배경 클릭, ESC 키 닫기를 테스트한다.

**HTML (팝업 버튼과 팝업 본문):**
```html
<section class="section" id="popupDemo">
  <h3><span class="number">03</span>팝업(Popup) 대체 구현</h3>
  <p class="desc">jQuery Mobile 1.0에는 기본 팝업 위젯이 없어 <code>fadeIn()</code>, <code>fadeOut()</code>을 사용합니다.</p>
  <a href="#" data-role="button" data-theme="b" id="btnPopupOpen">팝업 알림 열기</a>
</section>
<!-- [STEP 10] CSS + jQuery로 중앙 팝업 구현 -->
<div id="popupShade" aria-hidden="true"></div>
<div id="popupBox" role="dialog" aria-modal="true" aria-labelledby="popupHeading" aria-hidden="true">
  <h3 id="popupHeading">실습 알림</h3>
  <p>jQuery Mobile 1.0 환경에서<br>직접 구현한 오버레이 팝업입니다.</p>
  <a href="#" id="btnPopupClose" data-role="button" data-theme="b">닫기</a>
</div>
```

**CSS (이번 단계에 추가):**
```css
/* [STEP 10] 1.0에서 팝업은 CSS + 기본 jQuery로 직접 구현 */
#popupShade { display:none; position:fixed; inset:0; z-index:1200; background:rgba(19,34,52,.58); }
#popupBox { display:none; position:fixed; z-index:1201; width:calc(100% - 42px); max-width:400px; top:50%; left:50%; transform:translate(-50%, -50%); background:white; border-radius:14px; border:1px solid #c4d9eb; box-shadow:0 12px 32px rgba(6,34,56,.32); padding:21px; text-align:center; }
#popupBox h3 { color:#174468; margin:0 0 7px; }
#popupBox p { color:#465b70; line-height:1.65; }
```

**JavaScript (이번 단계에 추가):**
```javascript
// [STEP 10] 팝업 알림 표시/숨기기
function openPopup() {
  $("#popupShade").fadeIn(160);
  $("#popupBox").fadeIn(160).attr("aria-hidden", "false");
}
function closePopup() {
  $("#popupBox").fadeOut(160).attr("aria-hidden", "true");
  $("#popupShade").fadeOut(160);
}
$("#btnPopupOpen").bind("click", function (e) {
  e.preventDefault();
  openPopup();
});
$("#btnPopupClose, #popupShade").bind("click", function (e) {
  e.preventDefault();
  closePopup();
});
// [STEP 10] ESC 키로 팝업과 패널을 닫음
$(document).bind("keydown", function (e) {
  if (e.which === 27) {
    closePopup();
    closePanel();
  }
});
```

## STEP 11. 반응형 테이블 대체 구현

- **파일:** `11_responsive_table.html`
- **핵심:** `@media (max-width: 580px), data-label`
- **테스트:** 브라우저 폭을 580px 이하로 줄여 표가 세로 카드로 바뀌는지 확인한다.

**HTML (이번 단계에서 새로 추가하는 부분):**
```html
<section class="section" id="table">
  <h3><span class="number">04</span>반응형 테이블 대체 구현</h3>
  <p class="desc">화면이 580px 이하이면 CSS 미디어 쿼리가 표의 각 행을 세로 카드로 바꿉니다. 브라우저 폭을 조절해 보세요.</p>
  <table class="demo-table">
    <thead><tr><th scope="col">이름</th><th scope="col">학과</th><th scope="col">성적</th><th scope="col">학습 상태</th></tr></thead>
    <tbody>
      <tr><td data-label="이름">김학생</td><td data-label="학과">인공지능</td><td data-label="성적">95점</td><td data-label="학습 상태">우수</td></tr>
      <tr><td data-label="이름">이학생</td><td data-label="학과">소프트웨어</td><td data-label="성적">88점</td><td data-label="학습 상태">진행 중</td></tr>
      <tr><td data-label="이름">박학생</td><td data-label="학과">정보보호</td><td data-label="성적">92점</td><td data-label="학습 상태">완료</td></tr>
    </tbody>
  </table>
</section>
```

**CSS (이번 단계에 추가):**
```css
/* [STEP 11] 학습 결과 표 구조 */
.demo-table { width:100%; border-collapse:collapse; font-size:14px; }
.demo-table th, .demo-table td { border:1px solid #cfdbe8; padding:10px; text-align:left; }
.demo-table th { background:#e9f2fa; color:#174468; }
.demo-table tr:nth-child(even) { background:#f7fafd; }
/* [STEP 11] 화면이 580px 이하일 때 각 행을 세로 카드로 전환 */
@media (max-width:580px) {
  .section { padding:13px 11px; }
  .demo-table, .demo-table tbody, .demo-table tr, .demo-table td { display:block; width:100%; }
  .demo-table thead { display:none; }
  .demo-table tr { margin-bottom:10px; border:1px solid #cfdbe8; border-radius:8px; overflow:hidden; }
  .demo-table td { border:0; border-bottom:1px solid #e5edf4; display:flex; justify-content:space-between; gap:10px; }
  .demo-table td:last-child { border-bottom:0; }
  .demo-table td:before { content:attr(data-label); font-weight:bold; color:#194567; }
}
```

## STEP 12. 2~5단 그리드 / 전체 완성

- **파일:** `12_grid_layout.html`
- **핵심:** `ui-grid-a ~ ui-grid-d, ui-block-a ~ ui-block-e`
- **테스트:** 2·3·4·5단 그리드를 확인하고 앞 단계 기능이 모두 작동하는지 점검한다.

**HTML (이번 단계에서 새로 추가하는 부분):**
```html
<section class="section" id="grid">
  <h3><span class="number">05</span>그리드(Grid Layout)</h3>
  <p class="desc"><code>ui-grid-a</code>부터 <code>ui-grid-d</code>까지 jQuery Mobile 1.0에서 사용 가능합니다.</p>
  <h4>2단: ui-grid-a</h4>
  <div class="ui-grid-a grid-example"><div class="ui-block-a"><div class="grid-cell">A</div></div><div class="ui-block-b"><div class="grid-cell">B</div></div></div>
  <h4>3단: ui-grid-b</h4>
  <div class="ui-grid-b grid-example"><div class="ui-block-a"><div class="grid-cell">A</div></div><div class="ui-block-b"><div class="grid-cell">B</div></div><div class="ui-block-c"><div class="grid-cell">C</div></div></div>
  <h4>4단: ui-grid-c</h4>
  <div class="ui-grid-c grid-example"><div class="ui-block-a"><div class="grid-cell">A</div></div><div class="ui-block-b"><div class="grid-cell">B</div></div><div class="ui-block-c"><div class="grid-cell">C</div></div><div class="ui-block-d"><div class="grid-cell">D</div></div></div>
  <h4>5단: ui-grid-d</h4>
  <div class="ui-grid-d grid-example"><div class="ui-block-a"><div class="grid-cell">A</div></div><div class="ui-block-b"><div class="grid-cell">B</div></div><div class="ui-block-c"><div class="grid-cell">C</div></div><div class="ui-block-d"><div class="grid-cell">D</div></div><div class="ui-block-e"><div class="grid-cell">E</div></div></div>
</section>
```

**CSS (이번 단계에 추가):**
```css
/* [STEP 12] ui-grid-a ~ ui-grid-d 내부 색상 */
.grid-cell { background:#e5f1ff; color:#20537c; border-radius:7px; padding:10px 3px; margin:4px; text-align:center; border:1px solid #cbdff2; font-weight:bold; font-size:12px; }
.grid-example { margin-bottom:12px; }
.grid-example:after { content:""; display:block; clear:both; }
@media (max-width:580px) {
}
```

## 순서대로 실습하기

1. `index.html`을 브라우저에서 열어 단계 목록을 확인합니다.
2. `01_basic_page.html`부터 `12_grid_layout.html`까지 차례대로 실행합니다.
3. 파일에서 `[STEP nn]` 주석을 찾아 해당 단계에 새로 추가된 HTML·CSS·JS를 비교합니다.
4. 각 단계의 노란색 **실습 테스트** 항목을 수행하고 예상 동작을 확인합니다.
5. 마지막 단계 파일은 모든 기능이 누적된 완성본입니다.

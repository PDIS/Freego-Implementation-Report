# Freego 檢測相容性報告

Freego 是由數位發展部提供的自動化檢測工具，用於台灣各級機關機構學校網站無障礙檢測及認證標章相關業務；[Freego (Sep 27 2024)](https://accessibility.moda.gov.tw/Download/Category/70/1) 適用於[網站無障礙規範 (110.07)](https://accessibility.moda.gov.tw/Accessible/Guide/68)，即對應 W3C [Web Content Accessibility Guidelines (WCAG) 2.1](https://www.w3.org/TR/WCAG21/)。

為確認 Freego 檢測之信效度，爰採用 W3C [ACT Rules Community Group](https://www.w3.org/community/act-r/) 維護之[測試案例](https://act-rules.github.io/pages/implementations/testcases/)進行測試，測試結果可與[其他檢測工具或方法](https://www.w3.org/WAI/standards-guidelines/act/implementations/)進行比較。

## 測試結果判定方式

由於目前 Freego 版本尚不能產製符合 W3C [Evaluation and Report Language (EARL) 1.0 Schema](https://www.w3.org/TR/EARL10-Schema/) 格式之檢測報告，故現階段採用 [ACT Implementor](https://act-implementor.netlify.app/) 工具手動產製檢測相容性報告。又，Freego 目前版本尚不能指定特定一個或多個檢測碼進行檢測，測試檢測相容性之程序調整如下：

1. 檢視 ACT Rules Test Cases 規則名稱及內容
2. 判斷對應的（一個或多個）檢測碼，填入 `Implementation Procedure Name`；若無對應檢測碼，則該規則所有測試案例的 `Outcome` 記錄為 `Inapplicable`
3. 從 Freego 產出之報告中，找到對應的測試案例段落，檢視其結果。若出現前一步驟對應的檢測碼，即記錄 `Outcome` 為 `Failed`，否則記錄為 `Passed`（即使仍有其他檢測碼的不通過結果）
4. Freego 產出之報告中，若發生`頁面載入逾時`，則相關的 `Outcome` 欄位記錄為 `Inapplicable`

## ACT Rules 檢測相容性

Freego 與 [ACT Rules Implementation in Automated Test Tools](https://www.w3.org/WAI/standards-guidelines/act/implementations/#automated-test-tools) 列出之各種自動化檢測工具比較如下：

|自動化檢測工具及版本|一致|部分一致|不一致：誤判|不一致：無效|不一致：誤判且無效|未實作|合計|
|--------------------|----|--------------|--------------|--------------------|------|------|----|
|Freego<br>`Sep 27 2024`|1|0|13 (+5)|14 (+5)|5|54|87|
|[Alfa (fully automated)](https://alfa.siteimprove.com/)<br>`0.80.0`|31|8|??|??|??|??|87|
|[Axe-core](https://www.npmjs.com/package/axe-core/)<br>`4.8.3`|30|11|??|??|??|??|87|
|[Equal Access Accessibility Checker](https://www.ibm.com/able/toolkit/)<br>`3.1.42-rc.0`|25|5|??|??|??|??|87|
|[QualWeb](http://qualweb.di.fc.ul.pt/evaluator/)<br>`3.0.0`|41|20|??|??|??|??|87|
|[SortSite](https://www.powermapper.com/products/sortsite/)<br>`6.45`|44|0|??|??|??|??|87|
|[Total Validator (+Browser)](https://www.totalvalidator.com/)<br>`17.4.0`|44|1|??|??|??|??|87|

註：`不一致：誤判`及`不一致：無效`標示的`(+5)`係表示另有`不一致：誤判且無效`單獨計算。

### 相容性定義

相關定義取自 [Understanding ACT Consistency](https://www.w3.org/WAI/standards-guidelines/act/implementations/#understanding-act-consistency)

#### 特異性

指「應通過」的測試案例可以得到`通過`結果，且「不適用」的測試案例可以得到`不適用`或`通過`結果的比例。

理想值為 `100%`。

#### 敏感性

指「應檢測出錯誤」的測試案例可以得到`不通過`結果的比例。

理想值為 `100%`。

#### 一致

指某個 ACT Rules 檢測規則以 Freego 實測得到`特異性 100%`且`敏感性 100%`的結果。

#### 部分一致

指某個 ACT Rules 檢測規則以 Freego 實測得到`特異性 100%`且`敏感性介於 0%（不包含）～100%（不包含）之間`的結果。

#### 不一致

指某個 ACT Rules 檢測規則以 Freego 實測得到`特異性未達 100%`（`不一致：誤判`）或`敏感性 0%`（`不一致：無效`）的結果。

#### 未實作

指某個 ACT Rules 檢測規則沒有對應的 Freego 檢測規則（檢測碼）。

### ACT Rules 檢測規則相容性詳細結果

依 [freego.json](https://raw.githubusercontent.com/PDIS/Freego-Implementation-Report/main/freego.json) 整理如下表：

|ACT Rules 檢測規則|對應 WCAG|對應檢測碼|特異性|敏感性|相容性|
|--------------|---------|----------|------|------|------|
|[Role attribute has valid value](https://www.w3.org/WAI/standards-guidelines/act/rules/674b10/)|[1.3.1](https://www.w3.org/TR/WCAG2/#info-and-relationships), [4.1.2](https://www.w3.org/TR/WCAG2/#name-role-value)|[HM1410200C](https://accessibility.moda.gov.tw/Download/Detail/1525)|8/8|0/2|不一致：無效|
|[ARIA state or property has valid value](https://www.w3.org/WAI/standards-guidelines/act/rules/6a7281/)|[1.3.1](https://www.w3.org/TR/WCAG2/#info-and-relationships), [4.1.2](https://www.w3.org/TR/WCAG2/#name-role-value)|[HM1410200C](https://accessibility.moda.gov.tw/Download/Detail/1525)|14/14|0/7|不一致：無效|
|[ARIA attribute is defined in WAI-ARIA](https://www.w3.org/WAI/standards-guidelines/act/rules/5f99a7/)|[1.3.1](https://www.w3.org/TR/WCAG2/#info-and-relationships), [4.1.2](https://www.w3.org/TR/WCAG2/#name-role-value)|[HM1410200C](https://accessibility.moda.gov.tw/Download/Detail/1525)|5/5|0/2|不一致：無效|
|[Element with lang attribute has valid language tag](https://www.w3.org/WAI/standards-guidelines/act/rules/de46e4/)|[3.1.2](https://www.w3.org/TR/WCAG2/#language-of-parts)|[HM1310100C](https://accessibility.moda.gov.tw/Download/Detail/1520), [HM2310200C](https://accessibility.moda.gov.tw/Download/Detail/1521)|9/10|1/9|不一致：誤判|
|[Menuitem has non-empty accessible name](https://www.w3.org/WAI/standards-guidelines/act/rules/m6b1q3/)|[1.3.1](https://www.w3.org/TR/WCAG2/#info-and-relationships), [4.1.2](https://www.w3.org/TR/WCAG2/#name-role-value)|[HM1410200C](https://accessibility.moda.gov.tw/Download/Detail/1525)|4/6|2/2|不一致：誤判|
|[Iframe with interactive elements is not excluded from tab-order](https://www.w3.org/WAI/standards-guidelines/act/rules/akn7bn/)|[1.4.12](https://www.w3.org/TR/WCAG2/#text-spacing)||||未實作|
|[Important letter spacing in style attributes is wide enough](https://www.w3.org/WAI/standards-guidelines/act/rules/24afc2/)|[1.4.12](https://www.w3.org/TR/WCAG2/#text-spacing)||||未實作|
|[Important word spacing in style attributes is wide enough](https://www.w3.org/WAI/standards-guidelines/act/rules/9e45ec/)|[1.4.12](https://www.w3.org/TR/WCAG2/#text-spacing)||||未實作|
|[Important line height in style attributes is wide enough](https://www.w3.org/WAI/standards-guidelines/act/rules/78fd32/)|[1.4.12](https://www.w3.org/TR/WCAG2/#text-spacing)||||未實作|
|[autocomplete attribute has valid value](https://www.w3.org/WAI/standards-guidelines/act/rules/73f2c2/proposed/)|[1.3.5](https://www.w3.org/TR/WCAG2/#identify-input-purpose)||||未實作|
|[Button has non-empty accessible name](https://www.w3.org/WAI/standards-guidelines/act/rules/97a4e1/proposed/)|[1.3.1](https://www.w3.org/TR/WCAG2/#info-and-relationships), [4.1.2](https://www.w3.org/TR/WCAG2/#name-role-value)|[HM1130104C](https://accessibility.moda.gov.tw/Download/Detail/1512), [HM1410200C](https://accessibility.moda.gov.tw/Download/Detail/1525)|11/12|4/5|不一致：誤判|
|[Element marked as decorative is not exposed](https://www.w3.org/WAI/standards-guidelines/act/rules/46ca7f/proposed/)|||||未實作|
|[Form field has non-empty accessible name](https://www.w3.org/WAI/standards-guidelines/act/rules/e086e5/proposed/)|[1.3.1](https://www.w3.org/TR/WCAG2/#info-and-relationships), [4.1.2](https://www.w3.org/TR/WCAG2/#name-role-value)|[HM1130104C](https://accessibility.moda.gov.tw/Download/Detail/1512), [HM1130104C](https://accessibility.moda.gov.tw/Download/Detail/1512), [HM1410200C](https://accessibility.moda.gov.tw/Download/Detail/1525)|10/12|5/8|不一致：誤判|
|[HTML page lang attribute has valid language tag](https://www.w3.org/WAI/standards-guidelines/act/rules/bf051a/proposed/)|[3.1.1](https://www.w3.org/TR/WCAG2/#language-of-page)|[HM1310100C](https://accessibility.moda.gov.tw/Download/Detail/1520)|3/3|0/4|不一致：無效|
|[HTML page has non-empty title](https://www.w3.org/WAI/standards-guidelines/act/rules/2779a5/proposed/)|[2.4.2](https://www.w3.org/TR/WCAG2/#page-titled)|[HM1240200C](https://accessibility.moda.gov.tw/Download/Detail/1515)|6/7|6/6|不一致：誤判|
|[Image button has non-empty accessible name](https://www.w3.org/WAI/standards-guidelines/act/rules/59796f/proposed/)|[1.1.1](https://www.w3.org/TR/WCAG2/#non-text-content), [4.1.2](https://www.w3.org/TR/WCAG2/#name-role-value)|[HM1110104C](https://accessibility.moda.gov.tw/Download/Detail/1503), [HM1410200C](https://accessibility.moda.gov.tw/Download/Detail/1525)|6/9|2/3|不一致：誤判|
|[Image has non-empty accessible name](https://www.w3.org/WAI/standards-guidelines/act/rules/23a2a8/proposed/)|[1.1.1](https://www.w3.org/TR/WCAG2/#non-text-content)|[HM1110100C](https://accessibility.moda.gov.tw/Download/Detail/1499)|8/13|4/5|不一致：誤判|
|[Link has non-empty accessible name](https://www.w3.org/WAI/standards-guidelines/act/rules/c487ae/proposed/)|[4.1.2](https://www.w3.org/TR/WCAG2/#name-role-value), [2.4.4](https://www.w3.org/TR/WCAG2/#link-purpose-in-context), [2.4.9](https://www.w3.org/TR/WCAG2/#link-purpose-link-only)|[HM1410200C](https://accessibility.moda.gov.tw/Download/Detail/1525), [HM1240401C](https://accessibility.moda.gov.tw/Download/Detail/1517), [HM3240900C](https://accessibility.moda.gov.tw/Download/Detail/1518), [HM1110101C](https://accessibility.moda.gov.tw/Download/Detail/1500)|13/17|11/11|不一致：誤判|
|[SVG element with explicit role has non-empty accessible name](https://www.w3.org/WAI/standards-guidelines/act/rules/7d6734/proposed/)|[1.1.1](https://www.w3.org/TR/WCAG2/#non-text-content)||||未實作|
|[Element with presentational children has no focusable content](https://www.w3.org/WAI/standards-guidelines/act/rules/307n5z/proposed/)|[1.3.1](https://www.w3.org/TR/WCAG2/#info-and-relationships), [4.1.2](https://www.w3.org/TR/WCAG2/#name-role-value)|[HM1410200C](https://accessibility.moda.gov.tw/Download/Detail/1525)|4/4|0/3|不一致：無效|
|[Headers attribute specified on a cell refers to cells in the same table element](https://www.w3.org/WAI/standards-guidelines/act/rules/a25f45/proposed/)|[1.3.1](https://www.w3.org/TR/WCAG2/#info-and-relationships)|[HM1130101C](https://accessibility.moda.gov.tw/Download/Detail/1508)|11/14|0/4|不一致：誤判且無效|
|[Element with aria-hidden has no content in sequential focus navigation](https://www.w3.org/WAI/standards-guidelines/act/rules/6cfa84/proposed/)|[1.3.1](https://www.w3.org/TR/WCAG2/#info-and-relationships), [4.1.2](https://www.w3.org/TR/WCAG2/#name-role-value)|[HM1410200C](https://accessibility.moda.gov.tw/Download/Detail/1525)|9/9|0/6|不一致：無效|
|[Meta element has no refresh delay](https://www.w3.org/WAI/standards-guidelines/act/rules/bc659a/proposed/)|[2.2.1](https://www.w3.org/TR/WCAG2/#timing-adjustable), [2.2.4](https://www.w3.org/TR/WCAG2/#interruptions), [3.2.5](https://www.w3.org/TR/WCAG2/#change-on-request)||||未實作|
|[Meta viewport allows for zoom](https://www.w3.org/WAI/standards-guidelines/act/rules/b4f0c3/proposed/)|[1.4.4](https://www.w3.org/TR/WCAG2/#resize-text)||||未實作|
|[Object element rendering non-text content has non-empty accessible name](https://www.w3.org/WAI/standards-guidelines/act/rules/8fc3b6/proposed/)|[1.1.1](https://www.w3.org/TR/WCAG2/#non-text-content)|[HM1110105C](https://accessibility.moda.gov.tw/Download/Detail/1504)|11/12|5/6|不一致：誤判|
|[HTML page has lang attribute](https://www.w3.org/WAI/standards-guidelines/act/rules/b5c3f8/proposed/)|[3.1.1](https://www.w3.org/TR/WCAG2/#language-of-page)|[HM1310100C](https://accessibility.moda.gov.tw/Download/Detail/1520)|3/3|4/4|一致|
|[HTML page title is descriptive](https://www.w3.org/WAI/standards-guidelines/act/rules/c4a8a4/proposed/)|[2.4.2](https://www.w3.org/TR/WCAG2/#page-titled)|[HM1240200C](https://accessibility.moda.gov.tw/Download/Detail/1515)|3/4|0/3|不一致：誤判且無效|
|[Image accessible name is descriptive](https://www.w3.org/WAI/standards-guidelines/act/rules/qt1vmo/proposed/)|[1.1.1](https://www.w3.org/TR/WCAG2/#non-text-content)|[HM1110100C](https://accessibility.moda.gov.tw/Download/Detail/1499)|12/13|0/3|不一致：誤判且無效|
|[Scrollable content can be reached with sequential focus navigation](https://www.w3.org/WAI/standards-guidelines/act/rules/0ssw9k/proposed/)|[2.1.1](https://www.w3.org/TR/WCAG2/#keyboard), [2.1.3](https://www.w3.org/TR/WCAG2/#keyboard-no-exception)||||未實作|
|[Element in sequential focus order has visible focus](https://www.w3.org/WAI/standards-guidelines/act/rules/oj04fd/proposed/)|[2.4.7](https://www.w3.org/TR/WCAG2/#focus-visible)||||未實作|
|[Text has minimum contrast](https://www.w3.org/WAI/standards-guidelines/act/rules/afw4f7/proposed/)|[1.4.3](https://www.w3.org/TR/WCAG2/#contrast-minimum), [1.4.6](https://www.w3.org/TR/WCAG2/#contrast-enhanced)||||未實作|
|[Text has enhanced contrast](https://www.w3.org/WAI/standards-guidelines/act/rules/09o5cg/proposed/)|[1.4.6](https://www.w3.org/TR/WCAG2/#contrast-enhanced), [1.4.3](https://www.w3.org/TR/WCAG2/#contrast-minimum)||||未實作|
|[HTML images contain no text](https://www.w3.org/WAI/standards-guidelines/act/rules/0va7u6/proposed/)|[1.4.5](https://www.w3.org/TR/WCAG2/#images-of-text), [1.4.9](https://www.w3.org/TR/WCAG2/#images-of-text-no-exception)||||未實作|
|[Meta element has no refresh delay (no exception)](https://www.w3.org/WAI/standards-guidelines/act/rules/bisz58/proposed/)|[2.2.4](https://www.w3.org/TR/WCAG2/#interruptions), [3.2.5](https://www.w3.org/TR/WCAG2/#change-on-request), [2.2.1](https://www.w3.org/TR/WCAG2/#timing-adjustable)||||未實作|
|[ARIA required context role](https://www.w3.org/WAI/standards-guidelines/act/rules/ff89c9/proposed/)|[1.3.1](https://www.w3.org/TR/WCAG2/#info-and-relationships)||||未實作|
|[ARIA required ID references exist](https://www.w3.org/WAI/standards-guidelines/act/rules/in6db8/proposed/)|[1.3.1](https://www.w3.org/TR/WCAG2/#info-and-relationships), [4.1.2](https://www.w3.org/TR/WCAG2/#name-role-value)|[HM1410200C](https://accessibility.moda.gov.tw/Download/Detail/1525)|6/6|0/3|不一致：無效|
|[ARIA required owned elements](https://www.w3.org/WAI/standards-guidelines/act/rules/bc4a75/proposed/)|[1.3.1](https://www.w3.org/TR/WCAG2/#info-and-relationships)||||未實作|
|[ARIA state or property is permitted](https://www.w3.org/WAI/standards-guidelines/act/rules/5c01ea/proposed/)|[1.3.1](https://www.w3.org/TR/WCAG2/#info-and-relationships), [4.1.2](https://www.w3.org/TR/WCAG2/#name-role-value)|[HM1410200C](https://accessibility.moda.gov.tw/Download/Detail/1525)|13/13|0/3|不一致：無效|
|[Audio element content is media alternative for text](https://www.w3.org/WAI/standards-guidelines/act/rules/afb423/proposed/)|||||未實作|
|[Audio or video element avoids automatically playing audio](https://www.w3.org/WAI/standards-guidelines/act/rules/80f0bf/proposed/)|[1.4.2](https://www.w3.org/TR/WCAG2/#audio-control)||||未實作|
|[Audio element content has text alternative](https://www.w3.org/WAI/standards-guidelines/act/rules/e7aa44/proposed/)|[1.2.1](https://www.w3.org/TR/WCAG2/#audio-only-and-video-only-prerecorded)||||未實作|
|[Audio element content has transcript](https://www.w3.org/WAI/standards-guidelines/act/rules/2eb176/proposed/)|||||未實作|
|[Audio or video element that plays automatically has no audio that lasts more than 3 seconds](https://www.w3.org/WAI/standards-guidelines/act/rules/aaa1bf/proposed/)|||||未實作|
|[Audio or video element that plays automatically has a control mechanism](https://www.w3.org/WAI/standards-guidelines/act/rules/4c31df/proposed/)|||||未實作|
|[Text content that changes automatically can be paused, stopped or hidden](https://www.w3.org/WAI/standards-guidelines/act/rules/efbfc7/proposed/)|[2.2.2](https://www.w3.org/TR/WCAG2/#pause-stop-hide)||||未實作|
|[Block of repeated content is collapsible](https://www.w3.org/WAI/standards-guidelines/act/rules/3e12e1/proposed/)|||||未實作|
|[Bypass Blocks of Repeated Content](https://www.w3.org/WAI/standards-guidelines/act/rules/cf77f2/proposed/)|[2.4.1](https://www.w3.org/TR/WCAG2/#bypass-blocks)||||未實作|
|[Orientation of the page is not restricted using CSS transforms](https://www.w3.org/WAI/standards-guidelines/act/rules/b33eff/proposed/)|[1.3.4](https://www.w3.org/TR/WCAG2/#orientation)||||未實作|
|[Device motion based changes to the content can be disabled](https://www.w3.org/WAI/standards-guidelines/act/rules/c249d5/proposed/)|[2.5.4](https://www.w3.org/TR/WCAG2/#motion-actuation)||||未實作|
|[Device motion based changes to the content can also be created from the user interface](https://www.w3.org/WAI/standards-guidelines/act/rules/7677a9/proposed/)|[2.5.4](https://www.w3.org/TR/WCAG2/#motion-actuation)||||未實作|
|[Document has heading for non-repeated content](https://www.w3.org/WAI/standards-guidelines/act/rules/047fe0/proposed/)||[HM3241000C](https://accessibility.moda.gov.tw/Download/Detail/1519)|7/10|1/4|不一致：誤判|
|[Document has an instrument to move focus to non-repeated content](https://www.w3.org/WAI/standards-guidelines/act/rules/ye5d6e/proposed/)|||||未實作|
|[Document has a landmark with non-repeated content](https://www.w3.org/WAI/standards-guidelines/act/rules/b40fd1/proposed/)|||||未實作|
|[HTML element language subtag matches language](https://www.w3.org/WAI/standards-guidelines/act/rules/off6ek/proposed/)|[3.1.2](https://www.w3.org/TR/WCAG2/#language-of-parts)|[HM2310200C](https://accessibility.moda.gov.tw/Download/Detail/1521)|8/10|2/4|不一致：誤判|
|[Focusable element has no keyboard trap](https://www.w3.org/WAI/standards-guidelines/act/rules/80af7b/proposed/)|[2.1.2](https://www.w3.org/TR/WCAG2/#no-keyboard-trap)||||未實作|
|[Focusable element has no keyboard trap via non-standard navigation](https://www.w3.org/WAI/standards-guidelines/act/rules/ebe86a/proposed/)|||||未實作|
|[Focusable element has no keyboard trap via standard navigation](https://www.w3.org/WAI/standards-guidelines/act/rules/a1b64e/proposed/)|||||未實作|
|[Form field label is descriptive](https://www.w3.org/WAI/standards-guidelines/act/rules/cc0f0a/proposed/)|[2.4.6](https://www.w3.org/TR/WCAG2/#headings-and-labels)||||未實作|
|[Heading is descriptive](https://www.w3.org/WAI/standards-guidelines/act/rules/b49b2e/proposed/)|[2.4.6](https://www.w3.org/TR/WCAG2/#headings-and-labels)||||未實作|
|[Heading has non-empty accessible name](https://www.w3.org/WAI/standards-guidelines/act/rules/ffd0e9/proposed/)|||||未實作|
|[HTML page language subtag matches default language](https://www.w3.org/WAI/standards-guidelines/act/rules/ucwvc8/proposed/)|[3.1.1](https://www.w3.org/TR/WCAG2/#language-of-page)|[HM1310100C](https://accessibility.moda.gov.tw/Download/Detail/1520)|10/10|0/5|不一致：無效|
|[Iframe elements with identical accessible names have equivalent purpose](https://www.w3.org/WAI/standards-guidelines/act/rules/4b1c6c/proposed/)|[4.1.2](https://www.w3.org/TR/WCAG2/#name-role-value)|[HM1410201C](https://accessibility.moda.gov.tw/Download/Detail/1526)|12/19|3/4|不一致：誤判|
|[Iframe element has non-empty accessible name](https://www.w3.org/WAI/standards-guidelines/act/rules/cae760/proposed/)|[4.1.2](https://www.w3.org/TR/WCAG2/#name-role-value)|[HM1410201C](https://accessibility.moda.gov.tw/Download/Detail/1526)|3/7|4/4|不一致：誤判|
|[Image not in the accessibility tree is decorative](https://www.w3.org/WAI/standards-guidelines/act/rules/e88epe/proposed/)|[1.1.1](https://www.w3.org/TR/WCAG2/#non-text-content)|[HM1110106C](https://accessibility.moda.gov.tw/Download/Detail/1505)|15/15|0/5|不一致：無效|
|[Error message describes invalid form field value](https://www.w3.org/WAI/standards-guidelines/act/rules/36b590/proposed/)|[3.3.1](https://www.w3.org/TR/WCAG2/#error-identification)||||未實作|
|[Link is descriptive](https://www.w3.org/WAI/standards-guidelines/act/rules/aizyf1/proposed/)|[2.4.9](https://www.w3.org/TR/WCAG2/#link-purpose-link-only)|[HM3240900C](https://accessibility.moda.gov.tw/Download/Detail/1518)|7/7|0/5|不一致：無效|
|[Link in context is descriptive](https://www.w3.org/WAI/standards-guidelines/act/rules/5effbb/proposed/)|[2.4.4](https://www.w3.org/TR/WCAG2/#link-purpose-in-context), [2.4.9](https://www.w3.org/TR/WCAG2/#link-purpose-link-only)|[HM1240401C](https://accessibility.moda.gov.tw/Download/Detail/1517), [HM3240900C](https://accessibility.moda.gov.tw/Download/Detail/1518)|11/12|0/6|不一致：誤判且無效|
|[Links with identical accessible names have equivalent purpose](https://www.w3.org/WAI/standards-guidelines/act/rules/b20e66/proposed/)|[2.4.9](https://www.w3.org/TR/WCAG2/#link-purpose-link-only)||||未實作|
|[Links with identical accessible names and same context serve equivalent purpose](https://www.w3.org/WAI/standards-guidelines/act/rules/fd3a94/proposed/)|[2.4.4](https://www.w3.org/TR/WCAG2/#link-purpose-in-context), [2.4.9](https://www.w3.org/TR/WCAG2/#link-purpose-link-only)|[HM1240400C](https://accessibility.moda.gov.tw/Download/Detail/1516)|16/16|0/8|不一致：無效|
|[Content has alternative for visual reference](https://www.w3.org/WAI/standards-guidelines/act/rules/9bd38c/proposed/)|[1.3.3](https://www.w3.org/TR/WCAG2/#sensory-characteristics)||||未實作|
|[No keyboard shortcut uses only printable characters](https://www.w3.org/WAI/standards-guidelines/act/rules/ffbc54/proposed/)|[2.1.4](https://www.w3.org/TR/WCAG2/#character-key-shortcuts)||||未實作|
|[Element with role attribute has required states and properties](https://www.w3.org/WAI/standards-guidelines/act/rules/4e8ab6/proposed/)|[1.3.1](https://www.w3.org/TR/WCAG2/#info-and-relationships), [4.1.2](https://www.w3.org/TR/WCAG2/#name-role-value)|[HM1410200C](https://accessibility.moda.gov.tw/Download/Detail/1525)|9/9|0/6|不一致：無效|
|[Summary element has non-empty accessible name](https://www.w3.org/WAI/standards-guidelines/act/rules/2t702h/proposed/)|[1.3.1](https://www.w3.org/TR/WCAG2/#info-and-relationships), [4.1.2](https://www.w3.org/TR/WCAG2/#name-role-value)|[HM1410200C](https://accessibility.moda.gov.tw/Download/Detail/1525)|9/9|0/3|不一致：無效|
|[Table header cell has assigned cells](https://www.w3.org/WAI/standards-guidelines/act/rules/d0f69e/proposed/)|[1.3.1](https://www.w3.org/TR/WCAG2/#info-and-relationships)|[HM1130101C](https://accessibility.moda.gov.tw/Download/Detail/1508)|12/13|0/3|不一致：誤判且無效|
|[Video element auditory content has accessible alternative](https://www.w3.org/WAI/standards-guidelines/act/rules/eac66b/proposed/)|[1.2.2](https://www.w3.org/TR/WCAG2/#captions-prerecorded)||||未實作|
|[Video element visual content has accessible alternative](https://www.w3.org/WAI/standards-guidelines/act/rules/c5a4ea/proposed/)|[1.2.3](https://www.w3.org/TR/WCAG2/#audio-description-or-media-alternative-prerecorded), [1.2.5](https://www.w3.org/TR/WCAG2/#audio-description-prerecorded), [1.2.8](https://www.w3.org/TR/WCAG2/#media-alternative-prerecorded)||||未實作|
|[Video element content is media alternative for text](https://www.w3.org/WAI/standards-guidelines/act/rules/fd26cf/proposed/)|||||未實作|
|[Video element visual content has audio description](https://www.w3.org/WAI/standards-guidelines/act/rules/1ea59c/proposed/)|||||未實作|
|[Video element auditory content has captions](https://www.w3.org/WAI/standards-guidelines/act/rules/f51b46/proposed/)|[1.2.1](https://www.w3.org/TR/WCAG2/#audio-only-and-video-only-prerecorded)||||未實作|
|[Video element visual-only content has accessible alternative](https://www.w3.org/WAI/standards-guidelines/act/rules/c3232f/proposed/)|[1.2.1](https://www.w3.org/TR/WCAG2/#audio-only-and-video-only-prerecorded)||||未實作|
|[Video element visual-only content is media alternative for text](https://www.w3.org/WAI/standards-guidelines/act/rules/fd26cf/proposed/)|||||未實作|
|[Video element visual-only content has audio track alternative](https://www.w3.org/WAI/standards-guidelines/act/rules/d7ba54/proposed/)|||||未實作|
|[Video element visual-only content has transcript](https://www.w3.org/WAI/standards-guidelines/act/rules/ee13b5/proposed/)|||||未實作|
|[Video element visual content has strict accessible alternative](https://www.w3.org/WAI/standards-guidelines/act/rules/1ec09b/proposed/)|[1.2.5](https://www.w3.org/TR/WCAG2/#audio-description-prerecorded)||||未實作|
|[Audio and visuals of video element have transcript](https://www.w3.org/WAI/standards-guidelines/act/rules/1a02b0/proposed/)|[1.2.8](https://www.w3.org/TR/WCAG2/#media-alternative-prerecorded)||||未實作|
|[Visible label is part of accessible name](https://www.w3.org/WAI/standards-guidelines/act/rules/2ee8b8/proposed/)|[2.5.3](https://www.w3.org/TR/WCAG2/#label-in-name)||||未實作|
|[Zoomed text node is not clipped with CSS overflow](https://www.w3.org/WAI/standards-guidelines/act/rules/59br37/proposed/)|[1.4.4](https://www.w3.org/TR/WCAG2/#resize-text)||||未實作|

## Freego 檢測規則（檢測碼）與 ACT Rules 檢測規則相容性

|完全相容|部分相容|不相容|無法對應|合計|
|--------|--------|------|--------|----|
|0|1|15|13|29|

### 相容性定義

#### 完全相容

指 Freego 檢測規則可對應至 ACT Rules 檢測規則，且所有對應規則均達到`一致`之相容性。

完全相容的 Freego 檢測規則表示可獲得國際社群認可，可用於檢測網頁無障礙符合程度。

#### 部分相容

指 Freego 檢測規則可對應至 ACT Rules 檢測規則，但僅部分對應規則達到`一致`之相容性，或所有對應規則均達到`部分一致`之相容性。

部分相容的 Freego 檢測規則表示尚有改善空間，應謹慎考量如何用於檢測網頁無障礙符合程度。

#### 不相容

指 Freego 檢測規則可對應至 ACT Rules 檢測規則，且所有對應規則均為`不一致`之相容性。

不相容的 Freego 檢測規則表示判斷結果不可信，應重新檢討修訂檢測碼之實作，建議勿用於檢測網頁無障礙符合程度。

#### 無法對應

指 Freego 檢測規則無法對應至 ACT Rules 檢測規則。

無法對應的 Freego 檢測規則表示國際社群普遍認為相關檢測規則尚不成熟，極容易誤判，應充分與國際社群討論檢測規則適當性，建議勿用於檢測網頁無障礙符合程度。

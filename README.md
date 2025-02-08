# 「Freego 檢測相容性報告」專案

Freego 是由數位發展部提供的自動化檢測工具，用於台灣各級機關機構學校網站無障礙檢測及認證標章相關業務；[Freego (Sep 27 2024)](https://accessibility.moda.gov.tw/Download/Category/70/1) 適用於[網站無障礙規範 (110.07)](https://accessibility.moda.gov.tw/Accessible/Guide/68)，即對應 W3C [Web Content Accessibility Guidelines (WCAG) 2.1](https://www.w3.org/TR/WCAG21/)。

本專案目的為確認 Freego 檢測之信效度，採用 W3C [ACT Rules Community Group](https://www.w3.org/community/act-r/) 維護之[測試案例](https://act-rules.github.io/pages/implementations/testcases/)進行測試，預計測試結果可與[其他檢測工具或方法](https://www.w3.org/WAI/standards-guidelines/act/implementations/)進行比較。

由於目前 Freego 版本尚不能產製符合 W3C [Evaluation and Report Language (EARL) 1.0 Schema](https://www.w3.org/TR/EARL10-Schema/) 格式之檢測報告，故現階段本專案將採用 [ACT Implementor](https://act-implementor.netlify.app/) 工具手動產製檢測相容性報告。又，Freego 目前版本尚不能指定特定一個或多個檢測碼進行檢測，測試檢測相容性之程序調整如下：

1. 檢視 ACT Rules Test Cases 規則名稱及內容
2. 判斷對應的（一個或多個）檢測碼，填入 `Implementation Procedure Name`
3. 從 Freego 產出之報告中，找到對應的測試案例段落，檢視其結果。若出現前一步驟對應的檢測碼，即記錄 `Outcome` 為 `Failed`，否則記錄為 `Passed`（即使仍有其他檢測碼的不通過結果）
4. Freego 產出之報告中，若發生`頁面載入逾時`，則記錄為 `Cannot tell`

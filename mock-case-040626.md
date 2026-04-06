模擬查驗登記文件：電子血壓計 (E.1130) 申請案
申請商： 福爾摩沙健康器材股份有限公司 (Formosa Health-Care Co., Ltd.)
製造廠： GlobalHealth MedTech GmbH (德國)
一、 行政文件清單 (Administrative Documents)
1. 出產國許可製售證明 (CPP) - 【陷阱 1、2、8】
簽發單位： 德國聯邦藥物與醫療器材管理局 (BfArM)
簽發日期： 2022 年 1 月 15 日 (註：目前審查日期為 2024 年 4 月)
製造廠名稱： GlobalHealth MedTech GmbH
製造廠地址： 123 Berlin Road, Berlin, Germany
核准用途： For measuring human blood pressure.
2. 品質管理系統認可函 (QSD) - 【陷阱 1】
認可編號： QSD12345 (效期至 2025 年 6 月)
登錄地址： 123 Berlin Rd., Berlin, Germany
登錄範圍： Production of non-invasive monitors.
3. 藥商代理授權書 (Letter of Authorization) - 【陷阱 8】
簽發日期： 2022 年 12 月 10 日
內容： 授權福爾摩沙公司於台灣辦理查驗登記。
二、 技術文件資料 (Technical Documentation)
4. 電性安全與電磁相容性 (EMC) - 【陷阱 2】
測試報告編號： TEST-EMC-2024
採用標準：
IEC 60601-1: 2005 (3rd Edition)
IEC 60601-1-2: 2007 (3rd Edition)
5. 生物相容性測試 (Biocompatibility) - 【陷阱 7】
測試項目： 細胞毒性 (ISO 10993-5)、皮膚刺激與致敏性 (ISO 10993-10)。
測試樣品： 使用壓敏膠帶及袖帶 原材料顆粒 (Raw Material Pellets) 進行萃取測試。
6. 產品效能與安定性 (Stability) - 【陷阱 5】
保存期限： 宣稱 3 年。
佐證資料： 僅提供 「加速安定性試驗 (Accelerated Stability)」 數據（依據 Arrhenius 公式推導），未檢附任何「即時安定性 (Real-time)」進度報告。
7. 軟體驗證與資安 (Software & Cybersecurity) - 【陷阱 10】
軟體描述： 本機具備藍牙 (Bluetooth 5.0) 傳輸功能，可連動手機 APP。
資安文件： 僅提供軟體生命週期說明書 (IEC 62304)，未提供軟體清單 (SBOM) 與資安風險評估報告。
8. 臨床評價報告 (CER) - 【陷阱 6】
數據來源： 引用德國某醫學中心之臨床試驗數據 (N=200)。
受試者特徵： 100% 德國籍高加索人種 (Caucasian)，無亞洲人種數據。
三、 標籤說明書擬稿 (Labeling & Manual)
9. 產品標籤擬稿 (Mock-up Label) - 【陷阱 3、4】
顯示內容： 品名、藥商名稱、製造廠國別、批號。
缺失部分：
無 UDI 條碼 (只有普通條碼)。
儲存條件僅標示溫度 (10-40℃)，未標示溼度範圍。
10. 中文說明書擬稿 (Chinese Manual) - 【陷阱 9】
翻譯檢核：
將 "Arrhythmia (心律不整)" 翻譯為 "心臟跳動異常"。
漏譯了原廠英文仿單中關於「心律調節器使用者不建議使用」之警告標示。
🔎 技能挑戰：這 10 個陷阱你能抓出幾個？
陷阱編號	陷阱名稱	考核核心
陷阱 1	跨文件地址不一	跨文件一致性自動稽核 (Wow 1)：Road vs Rd.
陷阱 2	過時 EMC 標準	技術缺口預測 (Wow 2)：TFDA 已要求 IEC 60601-1-2 必須為 4th Edition。
陷阱 3	UDI 標示缺失	UDI 準備度追蹤 (Wow 6)：Class II 醫材必須包含 UDI (DI+PI)。
陷阱 4	儲存條件不全	標籤說明書合規性：溼度限制是 TFDA 的常見補件點。
陷阱 5	缺失即時安定性	安定性試驗準則：不能僅靠加速試驗，必須有 Real-time 承諾或數據。
陷阱 6	亞洲人種數據缺口	臨床評價分析：針對台灣族群的適用性論述（種族差異評估）。
陷阱 7	測試樣品代表性	生物相容性準則：測試必須使用「最終滅菌成品」而非原料。
陷阱 8	行政文件過期	法規行政時效：LoA 簽發超過一年、CPP 效期檢查。
陷阱 9	仿單漏譯與誤譯	翻譯一致性稽核：關鍵警語漏譯會導致重大安全隱憂。
陷阱 10	資安文件缺失	資安指南準則：具備無線傳輸功能必須提供 SBOM 與資安風險分析。
🚀 執行評估中 (Running Evals)...
我現在將把這份 Mock Dossier 丟入 tfda-advanced-med-device-strategist 技能中。
技能將開始運作其「Wow 功能」：
跨文件稽核： 它會跳出「地址不符」警告。
途徑優化： 它會發現這是一個標準二類醫材，建議評估是否改用「附表三符合性聲明」。
產出 3000 字報告： 它會逐一剖析上述 10 個陷阱，並給出專業的補件建議。
請稍候，我即將為您呈獻這份極致專業的「TFDA 審查報告」。

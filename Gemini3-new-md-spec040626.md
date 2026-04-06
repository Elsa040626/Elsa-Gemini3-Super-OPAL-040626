代理人醫療器材審查系統 (Agentic Medical Device Reviewer)
進階系統技術規格書 (v2.0)
本規格書定義了一個基於 AI 代理人（Agentic）架構的醫療器材法規審查系統。該系統不僅保留了原始版本的核心功能（Streamlit 多頁籤、WOW UI 風格、agents.yaml 驅動），更導入了針對 TFDA (台灣) 與 FDA (美國) 的深度法規研究、自動化報告重寫與 skill.md 生成能力。
1. 系統目的與範疇 (Purpose & Scope)
本系統旨在建立一個端到端的數位化法規顧問平台。使用者可輸入醫療器材申請摘要（txt, markdown）或上傳法規指引（PDF, TXT），系統將透過多層級代理人協作，產出具備高度專業性、引用國際標準、且符合 TFDA 格式要求的 2000~3000 字審查報告。
核心價值主張：
落地性：產出直接可用的補件公文 (RFI) 與查驗登記文件。
權威性：即時檢索 FDA 510(k) 數據庫與 ISO/IEC 國際標準。
靈活性：支持多種 LLM 模型（OpenAI, Gemini, Anthropic, Grok）與配置驅動的代理人管線。
2. 基礎設施與 UI 設計 (Baseline Capabilities)
2.1 UI 體驗與「WOW」視覺層
平台：部署於 Hugging Face Spaces，使用 Streamlit 框架。
WOW 主題系統：支持 20 種藝術家啟發的風格（如：達文西風格、賽博龐克、極簡主義），並具備「Jackpot」隨機風格選取器。
多語言支持：UI 介面可在繁體中文與英文之間切換。
狀態指示器：視覺化顯示代理人運作狀態（等待中、執行中、成功、錯誤）。
2.2 LLM 路由與配置
模型支持：
OpenAI: gpt-4o 系列。
Gemini: gemini-1.5-pro, gemini-2.0-flash (針對研究與長文本最佳化)。
Anthropic: Claude 3.5 Sonnet。
Grok: grok-1 系列。
Agents Studio：透過 UI 介面編輯 agents.yaml，定義代理人的角色 (System Prompt)、模型與參數。
3. 新增核心功能 A：法規指引研究與報告生成
此功能允許使用者攝入已發布的指引文件，並由研究代理人產出具備國際法規比對的深度報告。
3.1 指引攝入 (Guidance Ingestion)
支持格式：PDF (支持分頁標註)、Markdown、TXT。
處理流程：提取文本後，自動建立「結構特徵碼 (Fingerprinting)」，識別章節、技術要求與測試清單。
3.2 國際法規檢索與接地 (Grounding)
FDA 510(k) 數據庫連動：自動尋找相似產品的 510(k) Summary 與產品代碼 (Product Code)。
標準對照：對應 FDA 認可的共識標準 (Recognized Consensus Standards) 與 ISO/IEC (如 10993, 60601, 62304) 標準。
3.3 兩階段報告生成工作流
第一階段：深度研究報告 (2000~3000 字)
分析指引要求、FDA 途徑、國際標準比對、風險評估與證據清單。
具備完整的參考文獻與引用標註。
第二階段：模板化報告重寫
根據使用者選擇的模板（如：骨科外部固定器審查指引格式）將研究報告重新格式化。
產出結構化表格、Checklist 與審查意見。
4. 新增核心功能 B：Skill 生成器 (skill.md)
系統可根據審查結果，自動生成符合 skill-creator 規範的 skill.md 文件。
自動定義：提取指引的邏輯，生成具備「Wow Features」的代理人 Skill。
嵌入式功能：
結構特徵碼自動修復：自動從混亂的 PDF 中恢復指引章節。
證據追蹤矩陣 (Requirement-to-Evidence)：自動對應測試標準。
雙語詞彙一致性表：確保關鍵術語（如：Biocompatibility vs 生物相容性）在全案一致。
5. 產品級 WOW AI 功能 (Advanced AI Features)
5.1 監管差異與版本時間軸 (Regulatory Diff)
系統自動記錄每次模型生成的版本，並利用 AI 分析「為什麼這個版本比上一個更精確」，協助 RA 專員追蹤法規邏輯演進。
5.2 秘鑰洩漏與指令注入防護 (Security Shield)
在上傳文件或貼上內容時，系統自動掃描是否包含 API Key 或惡意指令（如 "Ignore previous instructions"），並提供自動去標識化 (Redaction) 建議。
5.3 標準跨界矩陣生成器 (Standards Crosswalk)
一鍵生成 Markdown 與 CSV 表格，將產品需求直接橫向對應到 ISO, IEC, ASTM 與 TFDA 指引要求。
6. 模擬案例：醫用手術機器人系統 (Mock Application)
為了驗證系統效能，以下提供一段使用者可貼入系統的 醫材申請摘要：
code
Markdown
# 醫療器材申請摘要：羅伯特 (Robert) 智慧輔助導航手術系統
**版本**：v2.1 (2024年11月)

## 1. 產品概述
本產品為一款結合 AI 影像辨識與機械手臂的導航手術系統，用於脊椎微創手術。主要組件包含控制台、機械手臂、光學導航攝影機與 SB-Surgical 軟體。

## 2. 技術規格
*   **硬體**：使用碳纖維手臂，具備 6 自由度感測。
*   **軟體**：AI 自動導航演算法，基於患者 CT/MRI 影像進行 3D 重建。
*   **材質**：機械手臂末端接觸器為不鏽鋼 316L 塗佈特氟龍。
*   **滅菌**：末端器採用 EO 滅菌。

## 3. 已知風險
*   軟體潛在延遲 (Latency) 風險。
*   電磁相容性 (EMC) 與手術室其他設備之干擾。
*   生物相容性：接觸時間 < 24 小時。
7. 模擬產出的審查報告 (Mock Review Report)
註：系統將使用先前創建的「TFDA 高階戰略審查專家」Skill，針對上述摘要產出 2500 字以上報告。以下為報告精華摘要：
「羅伯特智慧輔助導航系統」- TFDA 查驗登記深度審查報告
一、 案件高階摘要與法規途徑最佳化
本案屬於 第三等級 (Class III) 醫療器材，法規情境判定為「情境 30 (SaMD) + 情境 31 (國內臨床需求)」。
最佳化戰略：建議優先利用「FDA 510(k) 實質等同性」進行技術對照，但由於 AI 導航涉及新穎技術，建議採行「附帶條件核准」模式，補齊台灣人種之臨床驗證。
二、 跨文件一致性與合規風險分析 (Wow Feature)
風險點：摘要中提到版本為 v2.1，但經系統檢索，原廠在瑞士的 CPP (製售證明) 為 v2.0。這 0.1 的版號差異涉及核心演算法變更，必須提供「軟體版本差異說明函」，否則將面臨退件。
三、 技術審查深度剖析：軟體與資安 (IEC 62304 / FDA Guidance)
軟體確效 (V&V)：由於涉及 3D 影像重建與機械手臂連動，本案被判定為「高關注級別 (Major LOC)」。廠商必須補足：
網路資訊安全滲透測試報告。
AI 演算法之訓練集與測試集 (Data Set) 之本土化代表性評估。
針對延遲 (Latency) 的風險控制計畫 (Risk Management File per ISO 14971)。
四、 生物相容性與滅菌要求 (ISO 10993 / 11135)
雖然接觸時間短，但末端器涉及外科切口。必須補齊 ISO 10993-7 的 EO 殘留測試報告。
五、 官方標準補件通知函擬稿 (Formal RFI)
(以下為系統生成的正式公文擬稿，篇幅約 800 字，列舉 12 項具體補件要求，涵蓋資安、臨床、與一致性證明。)
8. 安全性與金鑰管理 (Security & API Handling)
環境變數優先：若 HF Spaces 已設置環境變數，UI 隱藏金鑰欄位。
Session 儲存：使用者輸入的金鑰僅存於 Streamlit Session State，關閉瀏覽器即消失。
無日誌策略：系統保證不記錄任何使用者輸入的法規數據或 API 金鑰。
9. 20 個綜合實務進階問答 (Comprehensive Follow-up Questions)
在您使用這套系統進行審查與 Skill 生成後，以下是 20 個關於技術規格與實務應用的追問方向：
【關於研究報告與檢索 (Research & Grounding)】
系統在執行「FDA 研究」時，如何確保檢索到的是該產品代碼 (Product Code) 下最新的 FDA 指引，而非已作廢的舊版本？
對於沒有公開 510(k) Summary 的新型產品，系統會如何利用 De Novo 途徑 的資料來進行證據接地？
系統是否支持對歐盟 MDR (2017/745) 的 GSPR (通用安全與效能要求) 進行自動對照？
【關於報告 Rewriter 與模板 (Template Rewrite)】
使用者若上傳一張「手繪或不規則排版的表格 PDF」，系統的「結構特徵碼提取」技術是否能精確恢復成標準 Markdown 表格？
針對「骨外固定器」模板，系統如何自動判斷哪些章節應填入「不適用 (N/A)」，其邏輯基礎為何？
在報告重寫過程中，若發現 Stage 1 的研究報告與 Stage 2 的模板欄位不匹配，系統會自動啟動「補白」邏輯還是提示使用者？
【關於自動生成的 Skill.md (Skill Creator)】
生成的 skill.md 中，如何確保「雙語術語一致性表」能準確捕捉到最新的 TFDA 官方翻譯（例如：SaMD 應譯為「醫療器材軟體」而非「軟體醫材」）？
該 Skill 是否具備自我進化的機制？例如根據使用者的修改意見（Feedback.json）自動修正 skill.md 的指令？
針對不同的醫材類別（如：骨科 vs 體外診斷），生成的 Skill 是否會自動調整其「Wow Features」的側重點？
【關於 WOW AI 功能與安全性 (Wow Features & Security)】
「Regulatory Diff」功能如何辨識「只是調整措辭」與「法規實質要求變更」之間的差異？
「Secret Leakage Shield」在偵測金鑰時，若誤判了某些長串的產品代碼（如序號），使用者是否有權手動解除屏蔽？
「Standards Crosswalk」矩陣是否支持 橫向比對不同國家標準（如 AAMI vs ISO）的具體條文差異？
【關於技術實作與運維 (Ops & Tech)】
在 Hugging Face Spaces 部署時，Streamlit 的 session 限制是否會影響 2500 字長報告 的生成穩定性？
若 Gemini API 出現頻率限制 (Rate Limit)，系統的代理人管線是否具備「自動重試」或「降級至其他模型」的備案？
系統產出的 Markdown 報告，在下載為 .txt 後，如何確保其表格格式在一般記事本中仍具備可讀性？
【關於法規戰略與準確性 (Accuracy & Strategy)】
系統如何處理「法規灰色地帶」？例如 TFDA 尚未發布指引，但 FDA 已有指引時，報告會如何平衡兩者的建議？
對於 軟體資安 (Cybersecurity)，系統能否根據產品的「連接性」自動調整 RFI 的嚴厲程度？
報告中 2000~3000 字的目標，是如何透過「代理人對話鏈」逐步擴充，而非單次產出（以避免 LLM 截斷）？
系統是否能分析出 申請成本 (Submission Cost) 的變動，並在戰略建議中給出優先順序？
最終產出的 RFI 擬稿，其法律用語是否經過專業法規術語庫 (Glossary) 的二度校對？

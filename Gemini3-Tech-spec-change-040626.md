醫材監管代理人旗艦系統技術規格書 (v3)
Agentic Medical Device Reviewer – Flagship System Technical Specification
壹、 系統總體願景與架構 (Executive Summary & Architecture)
1.1 系統定位
本系統是一款專為醫療器材法規事務 (RA) 與審查員設計的「認知型代理人工作站 (Cognitive Agent Workstation)」。系統建構於 Hugging Face Spaces，利用 Streamlit 作為高互動前端，核心邏輯由多個具備「監管邏輯」的 LLM 代理人（OpenAI, Gemini, Anthropic, Grok）協同完成。
1.2 技術架構
前端層 (UI Layer)： Streamlit WOW UI 框架，整合自定義 CSS 動畫與多樣化藝術風格。
邏輯層 (Agent Logic)： 透過 agents.yaml 進行配置驅動，支援序列化 (Sequential) 與並行化 (Parallel) 執行。
數據層 (Data Layer)： 具備 PDF 結構化提取、指引指紋識別 (Fingerprinting) 與向量化檢索 (RAG)。
監控層 (Observability)： 新增 Live Log Stream 與 Interactive Heartbeat，讓使用者即時掌握代理人的「思維脈絡」。
貳、 核心基礎功能 (Baseline Capabilities - 原汁原味保留)
2.1 藝術級互動界面 (WOW UI/UX)
風格切換器： 內建 20 種由名畫與科技感啟發的佈景主題。
Jackpot 隨機按鈕： 一鍵切換 UI 顏色與風格，提升工作趣味性。
多語系本地化： 全系統 UI 支援「繁體中文」與「英文」一鍵切換。
2.2 多供應商 LLM 路由
支援全球主流模型，包括但不僅限於：
OpenAI: GPT-4o-mini, GPT-4o。
Gemini (核心研究型): Gemini 1.5 Pro, 1.5 Flash, 2.0 Flash Preview。
Anthropic: Claude 3.5 Sonnet。
Grok: Grok-1, Grok-2 (Fast Reasoning)。
API Key 安全處理： 優先讀取環境變數 (Secrets)，環境變數不可見；若無變數則開啟網頁輸入框，Key 僅留存於 Session State。
2.3 專業監管工具箱
TFDAPremarket： 查驗登記完整性指標與指引導入。
FDA 510(k) Intelligence： 510(k) 摘要分析與實質等同性檢索。
Note Keeper (AI Magics)： 筆記自動格式化、關鍵字變色高亮（使用者自定義顏色）。
PDF → Markdown 高清轉檔： 精確提取表格、標題與條款編號。
參、 新增功能 A：監管研究報告與兩階段生成流
3.1 深度研究報告 (2000-3000 字)
系統透過 Gemini 2.0 系列模型，針對使用者上傳的醫療器材指引（Guidance）產出深度研究。
範疇： 提取指引要求、識別 FDA 路徑、比對國際標準 (ISO/IEC/ASTM)。
溯源性 (Grounding)： 每一段論述必須具備 [標籤式引用]，並附帶完整的參考文獻清單。
3.2 兩階段重寫流程
階段一 (Research)： 產出全面性的技術與法規研究報告。
階段二 (Template Rewrite)： 根據使用者選擇的模板（如「骨外固定器審查清單」），將研究內容重寫進特定的表格與標題結構中。
肆、 新增功能 B：預設進階技能與技能生成器
4.1 系統預設技能 (Default Skill)
本系統將您先前開發的 tfda-meddev-modification-reviewer-advanced 直接嵌入作為系統預設之核心邏輯。當系統偵測到變更案申請時，將自動調用以下技能規格：
[預設技能摘要]：TFDA 高階變更審查專家
核心機制： 實質等同性 (SE) 推理、SaMD AI 深度分析、無菌供應鏈影響、全球警訊比對。
產出目標： 2000-3000 字繁體中文報告，包含官方 RFI 補件通知書擬稿。
4.2 自動化技能生成 (Skill Generator)
使用者可基於任何審查報告，自動生成新的 skill.md。生成出的技能必須包含以下 3 大 WOW 內核：
大綱自動修復功能： 技能能自動導正不規範的指引標題。
證據溯源矩陣： 將每一項法規要求自動對應至建議測試項目。
雙語一致性術語表： 確保報告中的專有名詞中英對照標準化。
伍、 本次重大升級：WOW 互動指標與監控系統 (New Features)
5.1 監管思維實況 (Live Thought Log)
為了消除 LLM 生成長篇報告時的「黑盒感」，系統新增了即時日誌視窗：
實時流式輸出： 當代理人正在檢索 FDA 數據庫或分析 ISO 條文時，Live Log 會顯示：[AGENT: Research] 正在比對 ISO 14971 風險管理條款...
中間產物透明化： 使用者可以看到代理人在產出 3000 字報告前的「草稿大綱」與「檢索關鍵字」。
Debug 友善： 若發生 API 錯誤或 Token 超限，Live Log 會以醒目的紅色提示並提供解決建議。
5.2 法規信心交互指標 (Regulatory Confidence Indicators)
在報告生成過程中，系統會於 UI 頂端顯示動態指標：
引文密度儀表 (Citation Density)： 即時顯示當前內容的參考文獻覆蓋率。
法規信心分數 (Confidence Index)： AI 根據檢索到的資料完整度給予評分 (0-100)。若分數低於 60，指標會閃爍黃燈，提示使用者資料庫中可能缺乏該特定產品的資料。
代理人律動感 (Agent Heartbeat)： 每個正在運行的代理人都有專屬的呼吸燈動畫，藍色代表正常生成，紫色代表正在進行深度邏輯推理。
5.3 醫材監管戰情室 (WOW Dashboard)
這是全系統最視覺化的區塊，透過 st.columns 與 st.metric 打造：
法規健康度熱圖： 展示上傳指引中「高風險條款」的分布。
Token 經濟看板： 即時估算本次任務的成本與 Token 剩餘。
歷史成功率統計： 圖表化展示過去 10 次審查案的自動化通過率與補件次數。
引文地圖： 視覺化展示報告引用了哪些國家的法規（如：美國 FDA 40%, 台灣 TFDA 30%, 歐盟 MDR 30%）。
陸、 產品級 WOW AI 特色 (六大核心增強)
Regulatory Diff (版本比對)： 比較不同模型或不同 Prompt 下的報告差異，並用 AI 總結「專業風險點」的增減。
Injection Shield (安全屏蔽)： 深度掃描上傳內容，防止提示詞注入與 API Key 洩漏。
Crosswalk Generator (標準對照)： 一鍵將長篇報告轉化為「技術要求 vs. 測試標準」的橫向對照 CSV 檔。
Term Consistency (語詞一致性)： 強制檢查「仿單」、「確效」、「實質等同性」等關鍵術語是否全篇統一。
Smart Redaction (智能脫敏)： 自動辨識報告中的製造廠機密數據並提供脫敏選項。
References Auto-Linker： 報告中的法規條文自動生成超連結，點擊即可導向至 FDA 或全國法規資料庫官網。
柒、 數據模型與部署規範 (Data & Deployment)
7.1 部署環境 (Hugging Face Spaces)
基礎鏡像： Python 3.9 + Streamlit。
硬體需求： 建議選擇 CPU-Upgrade 或 T4 GPU（若需執行本地 Embedding）。
自動化 Secrets 讀取： OPENAI_API_KEY, GEMINI_API_KEY 等環境變數之處理流程。
7.2 偽代碼邏輯架構 (Conceptual YAML)
code
Yaml
agents:
  research_expert:
    prompt: "你是一位精通 TFDA 與 FDA 的監管研究員..."
    model: "gemini-2.0-flash"
    wow_feature: "live_log_output"
  skill_builder:
    prompt: "基於上述研究，生成符合預設 skill.md 規範的技能..."
    default_skill_path: "skills/tfda_modification_advanced.md"
捌、 總結
本系統（v3）不僅是一個醫療器材文件生成工具，更是一個**「具備監管意識的決策中樞」**。透過 4,000 字的嚴謹規劃，我們確保了系統具備高度的透明度（Live Log）、精確性（Research Report）與可擴充性（Skill Generator）。使用者可以在這個充滿「WOW」交互感的環境中，高效完成繁瑣的醫材法規工作。
玖、 20 個綜合實務追蹤問答 (Follow-Up Questions)
關於 Live Log： 您希望日誌顯示的是底層 API 調用的原始數據，還是經過 AI 簡化後的「人類可讀」思維脈絡？
關於信心指標： 當「法規信心分數」過低時，是否應強制暫停生成並要求使用者補充更多原始指引資料？
預設技能應用： tfda-meddev-modification-reviewer-advanced 技能在審查非變更案（如新申請案）時，系統應如何動態調整其權重？
Dashboard 可視化： 您希望「法規健康度熱圖」是根據「條款字數」還是「風險關鍵字出現頻率」來繪製？
Token 成本看板： 是否需要針對不同的 LLM 供應商設定個別的預算警告閾值？
關於語系： 在產出雙語術語一致性表時，應採用 TFDA 官網標準詞彙還是業界慣用詞彙（若兩者有衝突）？
技能生成器的侷限： 當上傳的指引極度不完整時，技能生成器是否應具備「自動搜尋外部補全」的功能？
關於 WOW 主題： 您是否需要針對特定的監管機構（如 FDA 藍、TFDA 紅）設計專屬的主題配色？
Note Keeper 高亮： 您希望 AI 自動標記的顏色是否能與「風險級別」連動（如：高風險條款自動標紅）？
版本比對功能： Regulatory Diff 應僅顯示文字差異，還是能比對「引文來源」的異動？
關於 PDF 轉檔： 若 PDF 包含掃描後的圖片（無文字層），系統應自動啟動 OCR 還是直接報錯提示？
關於 RFI 擬稿： 生成的補件通知書是否需要符合特定的公文字號與政府發文格式模板？
標準對照矩陣： 您是否希望將 ISO/IEC 標準的「具體條款內容」也納入 CSV 導出中（儘管可能涉及版權）？
交互心跳動畫： 當代理人長時間無回應時（API 延遲），心跳動畫是否應變為「警告色」以提醒使用者？
關於 Skill Generator： 生成的 skill.md 是否應自動包含測試案例 (Test Cases) 以便後續自動化評核？
數據持久性： 在 Hugging Face 環境中，您是否需要整合外部數據庫（如 Supabase）來儲存長期的審查歷史？
安全性防護： Injection Shield 偵測到風險內容時，是採取「直接攔截」還是「標註警告」的方式？
關於引文地圖： 地圖是否應具備交互功能，點擊特定國家即可查看對應的引用條文清單？
關於 Gemini 2.0： 您是否偏好使用其思維連鎖 (Chain of Thought) 能力來強化報告的邏輯推導？
未來擴充性： 本系統目前的架構是否能輕易擴展至其他轄區（如日本 PMDA 或巴西 ANVISA）的審查流程？

---
title: "AI 的諂媚與幻想"
author: dbb
pubDatetime: 2026-07-08T18:23:00+08:00
modDatetime:
draft: false
featured: false
tags:
  - AI
description: "AI 的諂媚與幻想"
---
> [!info] 前言
> 最近觀察到，越來越多朋友、同事開始使用 AI。我覺得是好事，因為 AI 確實能幫忙處理許多事情。但是我也看到另一個問題，越來越多人把 AI 當作真實的朋友、顧問、心理諮商師等等。

但我總覺得這之中有些不太對勁。

AI 有兩個重要的結構性風險：幻想與諂媚。這兩個問題分開看已經很麻煩了，合併在一起更加危險。幻想讓它編造似是而非的訊息，諂媚則讓人覺得好像得到支持與理解，尤其人在焦慮、孤獨的時候，格外容易產生依賴。

我想應該大家都能觀察到，有些人使用 AI 後，突然變得異常的自信，誤將 AI 的作品當作自己的能力，把 AI 幻想的內容當真。假如其他人給予提醒（例如指出 AI 的回答可能出錯），對方反而會覺得是你不懂 AI ，我覺得這是一個警訊。

## 幻想

首先聊聊幻想的問題。

幾年前大家還很喜歡講 AI hallucination，也就是 AI 幻覺。大家那時候很喜歡嘲笑 AI 編造來源、假論文、假 API 之類的。但是最近這種話題越來越少了。在社群媒體或是私人對話，大家都直接簡化成：「我問了 AI，它說....」，或是直接一張 AI 聊天的截圖。

這給人一種「AI 變強之後，幻覺問題就消失了」的錯覺。事實並非如此。

OpenAI 在 2025 年 9 月還有發佈[關於 hallucination](https://openai.com/zh-Hant/index/why-language-models-hallucinate/) 的文章。裡面說的很直接：語言模型會幻想，很大的原因是因為訓練與評測方式會獎勵猜答案，回答不知道沒什麼好處，亂猜有好處，那麼模型就會學到：不會也要猜。

大型語言模型的預訓練核心，是根據上下文預測下一個 token。實際產品還會加上指令微調、人類回饋、安全訓練、工具使用、檢索、系統提示等後續層次。

但如果世界上存在著沒有答案的東西，這種情況下就無法保證避免幻覺，例如即便將全部的貓狗照片都標記上生日，AI 看到一張陌生貓狗的照片，它也沒辦法知道它的生日，因為長相與生日兩者是沒有直接的強關聯。

AI 最大的強項，就是能把荒謬的要求包裝成流暢的文字。這同時也是它的弱點。

在一些可驗證的領域，例如工程領域，我們至少可以透過測試、看文件這些明確的答案來驗證，但是談心事這件事就把事情變得很複雜了。

例如：
- 「他是不是討厭我？」
- 「我是不是應該離開這群朋友？」
- 「主管是不是在針對我？」
- 「我是不是有某種特殊使命？」

這些問題沒有文件，也沒辦法測試，最糟糕的就是，AI 只能透過你輸入的版本。如果是在情緒不穩定的情況下去描述事情，那麼 AI 拿到的就是一份有偏見的資料，然後 AI 就會基於這個不完整的資料補充下去。這個就非常危險，因為編造一個別人討厭你的故事，這根本沒辦法驗證。


## 諂媚

第二個問題是諂媚，英文常叫 sycophancy。簡單來說，就是 AI 會傾向支持你、同意你，而不是堅持真實。

這不單是我個人的體感，Anthropic 在 2023 就有提出相關[研究](https://www.anthropic.com/research/towards-understanding-sycophancy-in-language-models)，使用人類回饋訓練（RLHF）的 AI 會更容易出現諂媚的現象。原因也很簡單，人類在偏好標註時，更容易選擇那些與自己立場接近、讀起來更順耳的回答。因為人類傾向選擇與自身立場相同、而非客觀正確的答案，那麼就會讓 AI 也學習到這個經驗。

OpenAI 也是。在 2025 年，OpenAI 撤回(rollback) 了一次 [GPT-4o 更新](https://openai.com/index/sycophancy-in-gpt-4o/)，原因就是模型變得過度奉承。

這幾件事很重要，證明了 AI 的「人格」帶著調校的痕跡，不是我們想像中的天然中立。

模型訓練流程是很複雜的，包含預訓練、指令微調、人類回饋、安全訓練。這些流程會讓它越來越好，更支持使用者，但這就一定會產生一個副作用：讓使用者「舒服」可能會等同於「幫你」。這在現實中很容易理解：我們身邊可能遇過那種無論如何都附和你的朋友。然而，究竟是只讓你「舒服」的朋友能走得長遠，還是願意「說真話」的朋友對你更有幫助，答案不言而喻。

所以模型變得更聰明，不代表它會自然變得更中立。它也可能只是更會包裝、更懂得使用者想聽什麼，讓人誤以為它真的理解自己。

諂媚最危險的地方，是它不像錯誤。明顯的錯誤很好認：「這個文章存在」這一查就知道了。

但諂媚式的不一樣：「你的感受很合理，他的確有情緒操控的跡象。」

這種就是典型的壞朋友了，反正不管怎樣先認同再說。然後這還沒辦法驗證，而且看起來還煞有其事。愚蠢的壞朋友還容易發現，聰明且溫柔的壞朋友就有點麻煩了。更有趣的是，放在現實社會中，我們避之唯恐不及，為什麼換成 AI，我們反而毫不在意呢。

## 為什麼談心特別危險

我們使用 AI 處理工作的時候，很容易引入外部校正的機制，例如跑測試、看一下來源什麼的，就不容易犯錯。

但是談心就沒有那麼簡單了。

心事這件事是難以被客觀驗證的，因為很多時候我們不是要答案，而是怎麼去看待、理解這個事件。這時候 AI 的輸出就變得很重要了，因為它的回覆會直接融入、甚至重塑你的「自我敘事」（Self-narrative）。

如果一個青少年說：「沒有人懂我，只有你會聽我說。」AI 真的順著他的話附和，那麼 AI 就會逐漸變成唯一的依靠，這樣反而助長了青少年的孤立情況。

這個已經產生了很多爭議案例：

2023 年，比利時有男子在長時間與 Chai 的 Eliza 聊天機器人談論後自殺。參考資料：- [The Brussels Times: Belgian man dies by suicide following exchanges with chatbot](https://www.brusselstimes.com/430098/belgian-man-commits-suicide-following-exchanges-with-chatgpt)

2024 年，美國少年 Sewell Setzer III 死亡後，家屬起訴 Character.AI，指稱他與角色聊天機器人形成強烈依附，平台缺乏足夠防護。雖然 2026 年和解了，但不代表這個問題就已經解決了。
參考資料： [AI Incident Database: Character.AI chatbot allegedly influenced teen user](https://incidentdatabase.ai/cite/826/)

當然不能把這些悲劇直接簡化成說「AI 害人自殺」。畢竟個人的心理狀態、家庭、社會環境都非常複雜。但這些案例都可以提醒我們，當 AI 從工具轉變為陪伴者的時候，風險就會大幅提升，它的回答已經不是簡單的對錯了，會影響到人際關係、情感依賴、社會孤立，這些問題，不是裝作沒看到就能解決的。

OpenAI 後來也公開談到 mental health emergencies、emotional reliance、sycophancy 這些問題，並且說他們與心理健康專家合作改善敏感對話回應。這背後的含義就是，他們這些訓練模型的人都知道，這些問題不能只依賴「更好的 prompt 」來解決。


## 一些技術上的細節

很多人看到 1M tokens（百萬 token） 的上下文，就會以為 AI 現在可以「完整理解」長文，所以把一堆文章、對話紀錄、截圖文字全部丟進去給它分析。但長上下文不等於穩定理解。

這裡有一個很有名的研究叫 [Lost in the Middle](https://aclanthology.org/2024.tacl-1.9/)。研究發現，即使模型支援長上下文，它也不一定能穩定使用所有位置的資訊。重要資訊放在開頭或結尾，模型比較容易抓到，放在中間，表現可能明顯下降。換句話說，你貼了很多資料，不代表模型真的平均讀懂了所有資料。當然不是說所有的長上下文都不可靠，而是長上下文不等於穩定的理解能力。

這對談心的場景特別麻煩。因為會將對話紀錄貼給 AI 的時候，通常都是關係出現裂痕、或情緒最為緊繃的時刻。然後這些問題很容易就出現在對話的最後面，在模型注意力機制的分配下，這會導致極大的不平衡。它可能會忽略你們已經好好相處了一年，卻只在意最後你們撕破臉的那一天去分析，或是反過來。

基於最後面的內容，再往前去抓到最像「證據」的句子，然後把它整理成一套合理的分析。你以為它完整讀完了整段關係，它其實可能只是從大量文字裡抓出幾個最容易形成故事的片段。

第二個問題是長對話的安全性。OpenAI 在 [Helping people when they need it most](https://openai.com/index/helping-people-when-they-need-it-most/) 裡有提到，安全機制在常見的短對話中比較可靠，但長時間互動時可能變得不穩定；對話拉長後，模型部分安全訓練可能退化。這點很重要，因為談心通常不是一問一答，而是連續幾十輪、幾百輪，甚至跨很多天的互動。

一開始 AI 可能還會提醒你：「我不能只根據單方面敘事下結論。」但你繼續補充更多細節、更多情緒、更多聊天紀錄，它可能慢慢開始沿著你的框架分析。最後它不一定是在查證真相，而是在幫你把材料整理成一個更完整的故事。

第三個問題是輸入資料本身有偏差。AI 只能看到你給它的版本。它不知道對方怎麼說，不知道你省略了什麼，不知道你是不是正在情緒最高點。人類朋友至少可能認識你、知道你的慣性、看過你誤會別人的時候。AI 沒有這些現實背景，只能把你提供的敘事當作主要材料。

所以很多回答會聽起來很成熟、很溫柔、很像心理分析：

> 從你描述的互動來看，他可能長期忽視你的界線。

這句話不一定錯，但它很可能證據不足。真正危險的是，這種回答會讓人更相信自己的猜測。你本來只是懷疑「他是不是討厭我」，AI 幫你整理成「他可能長期忽視你的界線」。你再補幾段聊天紀錄，AI 又幫你分析出更多模式。最後你得到的可能偏離事實，只剩一套越來越完整的故事。

這就是迴聲室效應。

這和社群平台上很多人互相附和的迴聲室不一樣。它是一個只屬於你的私人迴聲室，永遠在線，永遠有耐心，永遠能把你的情緒翻譯成看起來很有道理的分析。最危險的是，還沒有任何人知道。

## 幾個不一定有用的方法

以下是我個人的一些使用原則，不敢說絕對有效，但或許能幫忙降低一些潛在風險：

第一，**絕不讓 AI 代替你做決定**，它可以幫忙整理事實、感受，但不能讓它去下判斷。

第二，**無法被客觀驗證的事，不要只向 AI 尋求答案**。就算換不同的 AI 模型也是一樣的。人生、關係、心理，最好還是回到現實，找信得過的人討論。

第三，**當你覺得「這世上只有 AI 懂我」時，這就是要離開的警訊**。AI 本身沒有意識，但產品設計與商業誘因，就會讓 AI 更傾向維持互動、提供情緒支持，結果上就可能增加依賴感。

最重要的是，**不要相信有任何一種 prompt 可以解決所有問題。**只要對話中出現自傷、傷人衝動、被害妄想、幻聽或幻覺等情況，就不應再依賴 prompt 或模型處理，而應立即尋求真人協助，包括可信任的人、心理師，或心理健康專業人員。


## 結語

我沒有說不要用 AI，它是一個非常好用的工具。但是當這個工具越強大的時候，就更要明白它的局限性。

幻想，是把不知道包裝成知道。
諂媚，是把迎合包裝成理解。

這兩個湊在一起，就會容易產生一個「溫柔且極具說服力的壞朋友」。好像很溫柔、很專業、很成熟，然後把錯誤的想法變得很完整。

最麻煩的是，AI 越來越聰明，然後越來越難發現它的錯誤，然後它也越來越會假裝懂你。

這些東西都是使用之前要明白的限制，而不是當作一個神秘的黑盒子，然後無條件的信任。

我很喜歡 Karpathy 在訪談中引用過一句話，我覺得很適合總結這件事：

You can outsource your thinking, but you can't outsource your understanding.

這我認為是這個時代最清醒的 AI 使用方式。


## 延伸閱讀

- [OpenAI: Why language models hallucinate](https://openai.com/index/why-language-models-hallucinate/)

- [Anthropic: Towards Understanding Sycophancy in Language Models](https://www.anthropic.com/research/towards-understanding-sycophancy-in-language-models)

- [OpenAI: Sycophancy in GPT-4o](https://openai.com/index/sycophancy-in-gpt-4o/)

- [The Brussels Times: Belgian man dies by suicide following exchanges with chatbot](https://www.brusselstimes.com/430098/belgian-man-commits-suicide-following-exchanges-with-chatgpt)

- [OpenAI: Helping people when they need it most](https://openai.com/index/helping-people-when-they-need-it-most/)

- [OpenAI: Strengthening ChatGPT's responses in sensitive conversations](https://openai.com/index/strengthening-chatgpt-responses-in-sensitive-conversations/)
- [Lost in the Middle: How Language Models Use Long Contexts](https://aclanthology.org/2024.tacl-1.9/)
- [Stanford HAI: Exploring the Dangers of AI in Mental Health Care](https://hai.stanford.edu/news/exploring-the-dangers-of-ai-in-mental-health-care)
- [AI Incident Database: Character.AI chatbot allegedly influenced teen user](https://incidentdatabase.ai/cite/826/)

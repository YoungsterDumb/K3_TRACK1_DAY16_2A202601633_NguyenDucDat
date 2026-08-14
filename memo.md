# Teardown sản phẩm AI: Perplexity AI

**Nhóm:** Bumble

**Thành viên:** Nguyễn Đức Đạt, La Thế Quyền, Bùi Hoàng Vương, Trần Hoài Nam

**Sản phẩm phân tích:** Perplexity AI
**Ngày:** 14/08/2026

---

## §1. Timeline các cập nhật lớn

| Thời điểm | Cập nhật | Context lúc đó | Nguyên lý |
|---|---|---|---|
| **12/2022** | Ra mắt "answer engine" — chatbot tìm kiếm trả lời trực tiếp kèm trích dẫn nguồn, thay vì trả về 10 link xanh. Founder: Aravind Srinivas, Denis Yarats, Johnny Ho, Andy Konwinski. ([Wikipedia](https://en.wikipedia.org/wiki/Perplexity_AI), [Contrary Research](https://research.contrary.com/company/perplexity)) | ChatGPT vừa ra mắt (30/11/2022) gây sốt nhưng không có trích dẫn nguồn và hay bịa (hallucination); Google vẫn thống trị tìm kiếm nhưng kết quả ngập SEO spam. | **Wrapper → moat qua lớp tin cậy**: Perplexity không cạnh tranh model, mà quấn một lớp "trích dẫn + tổng hợp" lên trên LLM có sẵn, giải quyết đúng lỗ hổng lòng tin mà ChatGPT và Google đều có. |
| **2023 (~Q2)** | Ra mắt gói trả phí **Perplexity Pro** ($20/tháng) — cho phép chọn model nền (GPT-4, Claude, v.v.) thay vì khoá cứng một model. ([perplexity.ai/pro](https://www.perplexity.ai/pro), [tweet Aravind Srinivas](https://x.com/AravSrinivas/status/1904912486035579176)) | GPT-4 vừa ra (3/2023) với chi phí API đắt; công ty vừa gọi vốn Series A ($25.6M, định giá $121M) và đạt 2M MAU, cần dòng tiền để bù chi phí inference. | **Wrapper mỏng dễ bị hấp thụ → phải build moat bằng orchestration**: thay vì cược vào 1 model (rủi ro bị model đời sau nuốt chửng), Perplexity biến việc "chọn đúng model cho đúng việc" thành giá trị cốt lõi trả phí. |
| **07/2024** | Ra mắt **Publishers Program** — chia sẻ doanh thu quảng cáo với báo chí mỗi khi câu trả lời trích dẫn bài của họ (Fortune, TIME, Der Spiegel, WordPress.com...). Xảy ra chỉ **2 tháng** sau khi Perplexity ra mắt **Pages** (**30/05/2024** — [VentureBeat](https://venturebeat.com/business/perplexity-goes-beyond-ai-search-launches-publishing-platform-pages), không phải 02/2024 như bản nháp trước; công cụ tạo trang nội dung xuất bản công khai từ một prompt nghiên cứu), thứ đã kích ngòi khủng hoảng dưới đây. ([CNBC](https://www.cnbc.com/2024/07/30/perplexity-ai-to-share-revenue-with-publishers-after-plagiarism-accusations.html), [Slashdot](https://news.slashdot.org/story/24/07/30/2038226/perplexity-ai-will-share-revenue-with-publishers-after-plagiarism-accusations)) | Forbes (6/2024) và Wired phát hiện Perplexity/Pages đăng lại gần nguyên văn bài báo trả phí của họ mà gần như không dẫn nguồn rõ ràng; Wired còn tố Perplexity dùng IP ẩn danh để cào nội dung bất chấp robots.txt. Khủng hoảng truyền thông, nguy cơ publisher chặn crawler. | **Revert nguyên lý — vòng lặp tăng trưởng qua nội dung user-generated (Pages) phản tác dụng ngay khi thiếu kiểm soát nguồn, buộc phải sửa hướng**: moat của answer engine nằm ở chuỗi cung ứng dữ liệu, không chỉ ở model — phải trả tiền giữ nguồn cấp dữ liệu trước, mới có gì để tổng hợp mà thu phí sau. |
| **02/2025** | Ra mắt **Deep Research** — miễn phí cho tất cả (5 câu hỏi/ngày cho free, 500 cho Pro): tự động chạy hàng chục lượt tìm kiếm, đọc hàng trăm nguồn, tổng hợp báo cáo dài. ([TechCrunch](https://techcrunch.com/2025/02/15/perplexity-launches-its-own-freemium-deep-research-product/), [Perplexity blog](https://www.perplexity.ai/hub/blog/introducing-perplexity-deep-research)) | Google tung Gemini Deep Research (12/2024), OpenAI tung ChatGPT Deep Research (2/2025) gần như cùng lúc — cuộc đua giành danh mục "trợ lý nghiên cứu AI" thay vì chỉ trả lời một câu hỏi. | **Vertical AI / nâng cấp JTBD**: JTBD dịch chuyển từ "trả lời nhanh một câu hỏi" sang "làm hộ một tác vụ nghiên cứu nhiều bước" — X-Expert (AI) + domain workflow, không chỉ tốc độ. |
| **07/2025 – 10/2025** | Ra mắt trình duyệt **Comet** — trình duyệt AI-native (nền Chromium) tự đọc trang, tóm tắt, thực thi tác vụ nhiều bước; ban đầu độc quyền gói Max $200/tháng, rồi chỉ 3 tháng sau **mở miễn phí toàn cầu** kèm Background Assistants và kết nối Slack. ([CNBC](https://www.cnbc.com/2025/10/02/perplexity-ai-comet-browser-free-.html), [IBM](https://www.ibm.com/think/news/comet-perplexity-take-agentic-browser), [Perplexity Changelog](https://www.perplexity.ai/changelog) — mục 10/02/25) | Perplexity vừa đạt định giá $14–18B (5–7/2025); Perplexity đồng thời ra giá thâu tóm Chrome $34.5B (8/2025) — bị từ chối nhưng lộ rõ tham vọng. Google (Project Mariner) và các trình duyệt agent khác cũng nhắm vào "lớp thực thi". | **Sở hữu bề mặt phân phối = moat thật, và hạ giá ngay khi có tín hiệu PMF**: từ tính năng tìm kiếm, Perplexity nhảy sang kiểm soát cả trình duyệt; việc mở miễn phí toàn cầu chỉ sau 3 tháng cho thấy ưu tiên chiếm thị phần trình duyệt hơn doanh thu ngắn hạn từ Comet riêng lẻ. |
| **09/2025 – 08/2026** | Chuỗi mở rộng thành lớp workflow + thương mại: **App Connectors** (Gmail, Calendar, Notion, Linear, GitHub) + gói **Enterprise Max** (09/2025) → **Memory** (nhớ ngữ cảnh xuyên phiên) + **Instant Buy with PayPal** + Virtual Try On (12/2025) → Amazon kiện Comet vì "truy cập trái phép" tài khoản để mua hộ user (CFAA, đơn kiện nộp 11/2025); tòa án cấp quận ra **lệnh cấm sơ thẩm nghiêng về Amazon** (03/2026); Tòa Phúc thẩm Khu vực 9 sau đó **đảo ngược lệnh cấm sơ thẩm** này, xác định chính user — không phải Perplexity — là bên truy cập (phán quyết ngày **04/08/2026**, không phải 03/2026 như bản nháp trước — hai mốc này là hai sự kiện khác nhau, cách nhau ~5 tháng). ([Perplexity Changelog](https://www.perplexity.ai/changelog) — mục 09/18/25, 12/04/25; [CNBC](https://www.cnbc.com/2026/03/10/amazon-wins-court-order-to-block-perplexitys-ai-shopping-agent.html) — lệnh cấm sơ thẩm 03/2026; [PYMNTS](https://www.pymnts.com/news/artificial-intelligence/2026/ninth-circuit-narrows-cfaa-reach-in-perplexity-agentic-commerce-ruling/) — phán quyết phúc thẩm 04/08/2026) | Đối thủ (Google, Microsoft Copilot) cũng đẩy mạnh "agent kết nối vào app khác"; thương mại trong chat (agentic commerce) trở thành mặt trận cạnh tranh mới; các nền tảng thương mại điện tử lớn bắt đầu cảnh giác với agent bên ngoài truy cập tài khoản user thay họ. | **Nhúng sâu vào workflow/tài khoản bên thứ ba làm tăng giá trị — nhưng đẩy vào vùng xám pháp lý mới**: ranh giới "ai là bên truy cập khi agent hành động thay user" trở thành một dạng moat/rủi ro mới, không chỉ là vấn đề kỹ thuật hay UX. |
| **02/2026** | **Bỏ hoàn toàn quảng cáo**, chuyển 100% sang mô hình subscription + enterprise. ([ALM Corp](https://almcorp.com/blog/perplexity-ai-abandons-advertising-2026-analysis/), [GEAFirst](https://geafirst.com/perplexity-450m-arr-subscription-model-2026/)) | Doanh thu quảng cáo chưa tới 0.1% tổng doanh thu (~$20K/$34M năm 2024); đồng thời Comet Plus (chia 80% doanh thu cho publisher) vừa chứng minh mô hình subscription+rev-share khả thi. MRR tăng ~50% ngay tháng sau khi bỏ ads; ARR đạt $450M, 45M user, 1B+ query/tháng (7/2026). | **Định nghĩa "tốt" gắn với lòng tin, không phải doanh thu ngắn hạn**: một answer engine sống nhờ user tin câu trả lời không bị chi phối bởi ai trả tiền quảng cáo — quảng cáo mâu thuẫn trực tiếp với chính lời hứa cốt lõi của sản phẩm. |
| **02/2026 – 08/2026** | Ra mắt **Perplexity Computer** — sản phẩm agentic "computer-use" hoàn toàn mới, kèm tích hợp Samsung Galaxy S26 (02/2026). Chỉ trong 6 tháng, mở rộng thần tốc: phủ toàn bộ Pro users, Enterprise, Slack, Comet Enterprise, Personal Computer bản desktop cho Mac (03/2026) rồi Windows (07/2026); Computer học được nhớ việc đã làm, tự đổi model giữa tác vụ, tự xuất bản website (07/2026); tích hợp Microsoft 365 (Word/Excel/PowerPoint/Outlook/Teams), Model Council, Projects với file dùng chung (08/2026). ([Perplexity Changelog](https://www.perplexity.ai/changelog) — các mục 02/26/26 đến 08/04/26) | Microsoft (Copilot) và Google (Workspace AI/Gemini) đều đang đua vào "lớp thực thi tác vụ trên toàn máy tính", không chỉ trong một app/tab. Perplexity vừa thất bại vụ mua Chrome (8/2025) — Computer là hướng thay thế để không phụ thuộc hạ tầng trình duyệt/hệ điều hành của đối thủ. | **Đẩy "sở hữu bề mặt phân phối" (Comet) lên một tầng cao hơn — sở hữu cả lớp thực thi trên desktop và stack doanh nghiệp**: không chỉ trình duyệt, mà toàn bộ máy tính (Slack, Microsoft 365). Tốc độ rollout — ra mắt → phủ toàn nền tảng trong dưới 6 tháng — cho thấy đây là ưu tiên chiến lược số 1, không phải tính năng phụ. |

---

## §2. Tệp user & JTBD

### So sánh early adopters vs tệp hiện tại

| | **Early adopters (2022–2023)** | **Tệp hiện tại (2025–2026)** |
|---|---|---|
| **Đặc điểm** | Dân kỹ thuật, "search nerd" mệt mỏi với SEO spam của Google; theo dõi sát AI Twitter/Hacker News; thường là sinh viên/researcher/developer dùng bản free để thử ChatGPT-thay-thế-có-nguồn. | Dải rộng hơn nhiều: sinh viên & nhà nghiên cứu (Deep Research), nhà phân tích/marketer làm báo cáo, người mua sắm online (Buy with Pro), và nhóm đang biến Comet thành trình duyệt mặc định thay Chrome. |
| **JTBD chính** | "Cho tôi câu trả lời đáng tin, có trích dẫn, nhanh hơn việc tôi tự lọc 10 kết quả Google" — việc cần làm là *tra cứu & xác minh nhanh*, không phải "cần chatbot". | Dịch chuyển từ "trả lời câu hỏi" sang "**làm hộ tác vụ nhiều bước**": viết báo cáo nghiên cứu hoàn chỉnh (Deep Research), so sánh rồi mua sản phẩm (Buy with Pro), hoặc để Comet tự đặt vé/điền form trong lúc lướt web. |
| **Cách cũ họ làm việc đó** | Google search + tự đọc, đối chiếu nhiều tab, hoặc hỏi ChatGPT nhưng phải tự kiểm chứng vì không có nguồn. | Trước khi có Deep Research/Comet: tự làm nghiên cứu thủ công nhiều giờ, hoặc dùng nhiều tool rời rạc (search + so sánh giá + đặt hàng) trên nhiều tab/app khác nhau. |
| **Cột mốc gây dịch chuyển** | — | §1 · Deep Research (02/2025) và Comet (07/2025) là hai cột mốc trực tiếp nâng JTBD từ "trả lời" lên "hành động thay". |

### Switching cost — 4 forces

- **Push (đẩy khỏi Google):** SEO spam, quảng cáo dày đặc, phải tự tổng hợp nhiều nguồn; Google AI Mode/SGE vẫn bị xem là "dán thêm AI" chứ chưa đổi trải nghiệm gốc.
- **Pull (kéo về Perplexity):** trích dẫn minh bạch, tốc độ tổng hợp, và giờ đây là Comet — biến trình duyệt thành "trợ lý" tự làm việc thay, không chỉ trả lời.
- **Habit/Anxiety (ở lại với cái cũ):** thói quen Google ăn sâu 20+ năm; dữ liệu, mật khẩu, extension đã khoá trong Chrome — chi phí chuyển trình duyệt cao hơn nhiều so với chuyển search engine.
- **Anxiety (lo ngại cái mới):** lo về quyền riêng tư khi agent đọc trang thay mình và có thể truy cập tài khoản (chính là tâm điểm vụ kiện Amazon ở §1); lo sai sót khi để AI tự quyết định mua hàng/tài chính thay mình.

---

## §3. Ba dự đoán hướng đi (6–12 tháng tới, từ 08/2026)

**Dự đoán 1 (loại: mở rộng tính năng / segment thương mại)**
Dự đoán: Perplexity sẽ mở rộng "Buy with Pro" từ thí điểm cùng PayPal sang mạng lưới nhiều retailer và nhiều quốc gia hơn, biến Comet thành agent "làm hộ" mua sắm ở diện rộng chứ không chỉ một vài đối tác.
Lập luận: chiến thắng pháp lý trước Amazon ở Tòa Phúc thẩm Khu vực 9 (§1, **8/2026** — chỉ mới xảy ra 10 ngày trước thời điểm viết memo này) vừa gỡ rào cản pháp lý lớn nhất cho agent truy cập nền tảng thứ ba thay mặt user; kết hợp hạ tầng thanh toán đã có sẵn từ Buy with Pro (§1, 11/2025), bước tiếp theo hợp lý là nhân rộng, không phải dừng lại.

**Dự đoán 2 (loại: thay đổi mô hình kiếm tiền)**
Dự đoán: Mô hình chia doanh thu kiểu Comet Plus (80% cho publisher) sẽ trở thành chuẩn mặc định cho mọi nội dung được trích dẫn trên Perplexity — không chỉ giới hạn ở các đối tác Comet Plus đăng ký riêng lẻ.
Lập luận: bỏ hoàn toàn quảng cáo (§1, 2/2026) đã chứng minh subscription + rev-share nuôi được tăng trưởng (MRR +50%, ARR $450M); để giữ nguồn cung dữ liệu chất lượng (nguyên lý đã revert ở mốc Publishers Program §1, 7/2024), Perplexity cần chuẩn hoá cơ chế trả tiền cho publisher thay vì đàm phán từng deal.

**Dự đoán 3 (loại: đe doạ từ Big Tech)**
Dự đoán: Sau khi bị từ chối mua Chrome với giá $34.5B (§1, 8/2025), Google sẽ siết chặt quyền truy cập của các trình duyệt/agent bên thứ ba (kiểu Comet) vào hệ sinh thái Chrome/Gemini, buộc Perplexity phải đẩy mạnh Comet trên Android/di động và dựa vào "không quảng cáo = đáng tin hơn" làm lợi thế cạnh tranh thay vì đối đầu trực diện về hạ tầng phân phối.
Lập luận: dẫn từ hai mốc liên quan ở §1 — nỗ lực mua Chrome thất bại cho thấy Perplexity nhận ra bị phụ thuộc vào hạ tầng của Google, còn vụ kiện Amazon cho thấy các nền tảng lớn sẵn sàng dùng công cụ pháp lý để chặn agent bên ngoài; Google nhiều khả năng sẽ đi con đường tương tự Amazon nhưng ở tầng hệ điều hành/trình duyệt.

---

## §4. AI LOG - PHIÊN CHAT PHÂN TÍCH PERPLEXITY


**Phân công chất vấn (gợi ý theo guide.md — nhóm tự điều chỉnh nếu cần):**
- **Nguyễn Đức Đạt** — phụ trách mốc 12/2022 & 2023 (Launch, Pro)
- **La Thế Quyền** — phụ trách mốc 07/2024 & 02/2025 (Publishers Program, Deep Research)
- **Bùi Hoàng Vương** — phụ trách mốc 07/2025 & 09/2025–08/2026 (Comet, App Connectors/Amazon lawsuit)
- **Trần Hoài Nam** — phụ trách mốc 02/2026 & 02–08/2026 (Bỏ ads, Perplexity Computer)
- Cả 4 người cùng chất vấn chung: §2 (tệp user/JTBD) và §3 (3 dự đoán) — theo đúng guide.md, hai phần này "bắt buộc cả nhóm cùng làm, không giao một người".


Định dạng: Việc | AI làm hay nhóm làm? | Nhóm kiểm chứng/phán đoán lại thế nào?

1. Đọc và tổng hợp cuộc hội thoại tham chiếu
AI: Đọc lại các phân tích trước, gom yêu cầu và xác định cấu trúc đầu ra.
Nhóm: Kiểm tra AI có sử dụng đúng nội dung đã thảo luận, không bỏ sót yêu cầu hoặc đưa thêm kết luận ngoài phạm vi.

2. Chọn 7 cột mốc sản phẩm của Perplexity
AI: Đề xuất và sắp xếp Answer Engine, Pro, Enterprise Pro, Shopping, Deep Research, Comet và Computer.
Nhóm: Đối chiếu ngày ra mắt với nguồn chính thức; chỉ giữ mốc làm thay đổi core experience, segment, business model hoặc moat.

3. Phân tích context tại từng cột mốc
AI: Liên kết mỗi quyết định với bối cảnh thị trường, công nghệ và cạnh tranh.
Nhóm: Xem lại quan hệ nhân quả; phân biệt dữ kiện công khai với diễn giải chiến lược.

4. Rút ra nguyên lý sản phẩm
AI: Tổng hợp x10/xóa bước, wrapper → moat, Vertical AI, learning loop và định nghĩa “tốt”.
Nhóm: Đánh giá nguyên lý nào thực sự được timeline hỗ trợ; bỏ kết luận quá khái quát hoặc thiếu bằng chứng.

5. Xác định early adopters
AI: Suy luận persona từ review và hành vi quan sát được: technical builder/frontend dev ở startup nhỏ, đã dùng Google + ChatGPT/VS Code, theo dõi AI Twitter/X và Hacker News.
Nhóm: Kiểm tra Product Hunt comments, subreddit và review sớm; không trình bày suy luận như dữ liệu nhân khẩu học chính thức.

6. Xác định nơi tìm early adopters
AI: Đề xuất Product Hunt, r/perplexity_ai, r/ChatGPT, r/programming, Hacker News, X/Twitter và cộng đồng startup/AI.
Nhóm: Mở mẫu bài viết/review, kiểm tra thời điểm đăng và xem người dùng có thực sự mô tả pain/JTBD liên quan hay không.

7. Phân tích user hiện tại
AI: Mở rộng tệp thành knowledge workers, students/researchers, analysts, professionals, enterprise teams và agent users.
Nhóm: Đối chiếu với sản phẩm, tài liệu enterprise và nghiên cứu usage; tránh đồng nhất “user hiện tại” với toàn bộ thị trường mục tiêu.

8. Xác định cột mốc gây dịch chuyển user
AI: Gắn Enterprise Pro với B2B, Shopping với quyết định/giao dịch, Deep Research với deliverable và Comet/Computer với agent workflow.
Nhóm: Đánh giá mốc nào thực sự mở tệp mới, mốc nào chỉ tăng khả năng phục vụ tệp hiện hữu.

9. Viết JTBD cho từng tệp
AI: Chuyển cách viết từ tính năng sang công việc cần hoàn thành.
Nhóm: Kiểm tra mỗi JTBD có tình huống, động lực và outcome; sửa nếu câu vẫn mang dạng “cần một công cụ AI”.

10. Mô tả phương án trước Perplexity
AI: Dựng workflow cũ gồm Google, docs, Stack Overflow, Scholar, Drive/wiki, notes/sheets, email/Slack và tự tổng hợp.
Nhóm: Phỏng vấn hoặc quan sát user thật để xác nhận thứ tự, thời gian và pain của quy trình cũ.

11. Map switching cost vào 4 Forces
AI: Phân tích Push, Pull, Anxiety và Habit.
Nhóm: Đánh giá sức mạnh tương đối của từng lực; phân biệt switching cost của search cá nhân với enterprise/agent workflow.

12. Xác định yếu tố giữ user ở lại
AI: Chia thành ba tầng: thói quen/tốc độ; history/Spaces/file; dữ liệu nội bộ/permission/connector/workflow.
Nhóm: Kiểm tra yếu tố nào đã tồn tại, yếu tố nào mới là tiềm năng; không mặc định mọi dữ liệu đều tạo lock-in mạnh.

13. Viết ba dự đoán 6–12 tháng
AI: Extrapolate từ Computer, MCP/connectors, usage pricing và áp lực từ Big Tech.
Nhóm: Xem lại causal logic, xác suất và dấu hiệu có thể kiểm chứng; cập nhật kết quả sau 6–12 tháng.

14. Kiểm chứng nguồn
AI: Tìm nguồn chính thức của Perplexity, Product Hunt và nghiên cứu liên quan.
Nhóm: Mở nguồn gốc, kiểm tra ngày, nội dung và bối cảnh; không dùng đoạn tổng hợp tìm kiếm thay cho nguồn chính.

15. Soạn memo Word 3–5 trang
AI: Viết, rút gọn, thiết kế bảng và xuất tài liệu Word 5 trang.
Nhóm: Chịu trách nhiệm về lập luận cuối, giọng văn, độ phù hợp với rubric và nội dung được nộp.

16. Kiểm tra bố cục memo
AI: Render toàn bộ tài liệu; kiểm tra số trang, clipping, overlap, bảng và header/footer.
Nhóm: Mở lại bằng Microsoft Word trên thiết bị nộp bài để kiểm tra font, hyperlink và khác biệt renderer.

17. Tạo sơ đồ User/Adoption
AI: Chuyển nội dung thành infographic 16:9 gồm early adopters → cột mốc → user hiện tại, JTBD, switching cost và 4 Forces.
Nhóm: Kiểm tra chính tả tiếng Việt, khả năng đọc trên slide và độ chính xác của từng nhãn.

18. Quyết định nội dung cuối cùng
AI: Hỗ trợ nghiên cứu, tổng hợp, suy luận và trình bày.
Nhóm: Là bên phán đoán cuối, chịu trách nhiệm về fact-check, cách diễn giải, kết luận và mọi nội dung được sử dụng.

GHI CHÚ
- Persona early adopter là suy luận có kiểm soát từ pattern review và cộng đồng, không phải dữ liệu nhân khẩu học chính thức.
- Các dự đoán 6–12 tháng cần được đánh giá lại bằng các tín hiệu kiểm chứng đã nêu.
- Nhóm chịu trách nhiệm cuối cùng về độ chính xác của dữ kiện, cách diễn giải và nội dung nộp bài.


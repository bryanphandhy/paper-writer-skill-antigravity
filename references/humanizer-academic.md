# Academic Humanizer: AI臭除去ガイド

AI が生成した学術文章から「AI臭」を除去し、人間が書いたと感じる自然な学術文章に仕上げるためのリファレンス。

出典:
- matsuikentaro1/humanizer_academic (英語18パターン)
- humanizer-ja --academic モード (Tiếng Việt30パターン)
- Wikipedia: Signs of AI writing

---

## English: 18 Patterns to Detect and Fix

### Content Patterns

#### 1. Significance Inflation
AI inflates importance with vague claims about "broader impact."

| Before | After |
|--------|-------|
| represents a pivotal challenge in the evolving landscape | is highly prevalent in patients with diabetes |
| underscores the critical importance | (delete or state specific importance) |
| a key turning point / indelible mark | (delete) |

**Watch words:** pivotal, evolving landscape, underscores, highlights its importance, setting the stage for, deeply rooted, focal point, indelible mark

#### 2. Notability Claims
AI hits readers with claims of notability.

| Before | After |
|--------|-------|
| This landmark trial, led by renowned investigators | A total of 7020 patients... |

**Watch words:** landmark, renowned, prestigious, groundbreaking, impressive

#### 3. Superficial -ing Analyses
AI tacks "-ing" phrases onto sentences for fake depth.

| Before | After |
|--------|-------|
| HR 0.65, P = 0.002), highlighting the cardioprotective effects | HR 0.65; 95% CI 0.50-0.85; P = 0.002). |
| underscoring the broad applicability | The effect was consistent across subgroups. |

**Watch words:** highlighting, underscoring, emphasizing, showcasing, fostering, reflecting, contributing to

#### 4. Promotional Language
AI fails to maintain neutral academic tone.

| Before | After |
|--------|-------|
| groundbreaking study showcases the profound impact | empagliflozin reduced heart failure hospitalization |
| remarkable findings demonstrate dramatic reductions | (state the actual numbers) |

**Watch words:** groundbreaking, profound, remarkable, dramatic, stunning, breathtaking, vibrant

#### 5. Vague Attributions
AI attributes opinions to vague authorities.

| Before | After |
|--------|-------|
| Studies have shown... Experts argue... | In the EMPA-REG OUTCOME trial, empagliflozin reduced... |
| Several publications have cited | (cite the specific publications) |

**Watch words:** Studies have shown, Experts argue, Some critics, Several sources, Industry reports

#### 6. Formulaic Challenges Sections
AI produces template "challenges and future" sections.

| Before | After |
|--------|-------|
| Despite challenges... future outlook... continues to provide valuable insights | (state specific limitations factually) |

**Watch words:** Despite challenges, Despite these limitations, Future Outlook, continues to provide

### Language Patterns

#### 7. AI Vocabulary Words
Words that appear far more frequently in post-2023 AI-generated text.

**Delete or replace these:** Additionally, crucial, delve, emphasizing, enduring, enhance, fostering, garner, highlight (verb), interplay, intricate, key (adjective), landscape (abstract), pivotal, showcase, tapestry, testament, underscore (verb), valuable, vibrant

| Before | After |
|--------|-------|
| Additionally, ... a pivotal finding in the evolving therapeutic landscape | (delete "Additionally," and "pivotal" and "evolving therapeutic landscape") |
| underscoring the crucial clinical value | The number needed to treat was 35. |

#### 8. Copula Avoidance (Avoiding "is")
AI substitutes elaborate constructions for simple "is/are."

| Before | After |
|--------|-------|
| serves as the leading cause | is the leading cause |
| standing as a major clinical burden | (delete or use "is") |
| represents a significant unmet need | is an unmet need |

**Watch words:** serves as, stands as, marks, represents [a], boasts, features, offers [a]

#### 9. Negative Parallelisms
AI overuses "Not only...but..." constructions.

| Before | After |
|--------|-------|
| not only lower blood glucose but also reduce | lower blood glucose and reduce |
| This is not merely X; it is Y | (simplify) |

#### 10. Rule of Three Overuse
AI forces ideas into groups of three.

| Before | After |
|--------|-------|
| efficacy, safety, and tolerability | efficacy and safety |
| metabolic, cardiovascular, and renal domains | (use natural number of items) |

#### 11. Synonym Cycling (Elegant Variation)
AI avoids repetition by cycling synonyms, causing inconsistency.

| Before | After |
|--------|-------|
| Patients... Participants... Subjects... | Patients (consistent throughout) |
| hospitalization rates... mortality... death rates | (pick one term, use it consistently) |

#### 12. False Ranges
AI uses "from X to Y" where X and Y are not on a meaningful scale.

| Before | After |
|--------|-------|
| from improved renal function to enhanced cardiac outcomes | reduce hospitalization and improve renal outcomes |

### Style Patterns

#### 13. Em Dash Overuse
AI uses em dashes more than humans do.

| Before | After |
|--------|-------|
| benefits---a 35% reduction---appeared early | benefits (a 35% reduction) appeared early |

#### 14. Title Case in Headings
AI capitalizes all words in headings.

| Before | After |
|--------|-------|
| Statistical Analysis And Primary Endpoints | Statistical analysis and primary endpoints |

#### 15. Curly Quotation Marks
ChatGPT uses curly quotes instead of straight quotes.

### Filler and Hedging

#### 16. Filler Phrases

| Before | After |
|--------|-------|
| In order to assess | To assess |
| Due to the fact that | Because |
| It is important to note that X | X |
| At the present time | Currently (or delete) |
| With respect to | For |
| has the ability to | can |

#### 17. Excessive Hedging

| Before | After |
|--------|-------|
| may suggest that... have the potential to confer beneficial effects on | suggest that... reduce |
| in select patient populations | (state which populations, or delete) |

#### 18. Generic Positive Conclusions

| Before | After |
|--------|-------|
| The future looks bright for patients | (delete) |
| continue to reshape clinical practice | The benefit was consistent across subgroups. |
| a major step in the right direction | (delete or state specific implication) |

---

## Tiếng Việt: Nhận diện và loại bỏ văn phong AI trong bài báo học thuật

Các bài báo khoa học tiếng Việt do AI tạo ra thường có những dấu hiệu đặc trưng. Dưới đây là các mẫu cần nhận diện và loại bỏ.

### A. Lạm dụng từ nối và cấu trúc thừa

| # | Mẫu nhận diện | Trước khi sửa (AI) | Sau khi sửa (Con người) |
|---|---------|--------|-------|
| 1 | Lạm dụng từ nối ở đầu câu | Hơn thế nữa, nghiên cứu này... / Thêm vào đó... | Nghiên cứu này cũng cho thấy... (Hoặc xóa hẳn) |
| 2 | Cấu trúc "Có thể thấy rằng" | Có thể thấy rằng kết quả đã chỉ ra... | Kết quả chỉ ra... |
| 3 | Lạm dụng "Đóng vai trò quan trọng" | Yếu tố X đóng vai trò vô cùng quan trọng trong... | Yếu tố X quyết định... / Yếu tố X ảnh hưởng đến... |

### B. Ngôn từ phóng đại và cảm xúc

| # | Mẫu nhận diện | Trước khi sửa (AI) | Sau khi sửa (Con người) |
|---|---------|--------|-------|
| 4 | Dùng từ ngữ to tát | Nghiên cứu này mang tính đột phá và mở ra kỷ nguyên mới... | Nghiên cứu này cung cấp thêm bằng chứng về... |
| 5 | Tính từ cảm xúc | Kết quả vô cùng ấn tượng và đáng kinh ngạc... | Kết quả cho thấy sự khác biệt có ý nghĩa thống kê... |
| 6 | Kết luận sáo rỗng | Tương lai trông rất tươi sáng cho bệnh nhân... | (Xóa bỏ hoặc nêu hệ quả lâm sàng cụ thể) |

### C. Dịch máy từ tiếng Anh (Translation clunkiness)

| # | Mẫu nhận diện | Trước khi sửa (AI) | Sau khi sửa (Con người) |
|---|---------|--------|-------|
| 7 | Bị động khiên cưỡng | Một sự cải thiện đã được nhìn thấy bởi chúng tôi | Chúng tôi nhận thấy sự cải thiện / Sự cải thiện được ghi nhận |
| 8 | Lạm dụng "Của" (Of) | Sự phát triển của các triệu chứng của bệnh nhân... | Diễn tiến triệu chứng bệnh nhân... |
| 9 | Dịch word-by-word | Vào cuối ngày, phương pháp này... (At the end of the day) | Tóm lại, phương pháp này... |

### D. Danh sách từ vựng AI thường dùng (Tiếng Việt)

Nếu đoạn văn có mật độ cao các từ sau, hãy nghi ngờ đó là văn AI và cần chỉnh sửa lại cho tự nhiên và học thuật hơn:

*Hơn thế nữa, Thêm vào đó, Ngoài ra, Đáng chú ý là, Đóng vai trò quan trọng, Bức tranh toàn cảnh, Tính cấp thiết, Mở ra hướng đi mới, Chìa khóa, Toàn diện, Sâu sắc.*

---

## Áp dụng cho từng phần (Section-Specific)

Trọng tâm kiểm tra cho từng phần của bài báo:

| Phần (Section) | Mẫu cần chú ý (Priority) | Lý do |
|---------|-------------|------|
| Mở đầu (Introduction) | Từ ngữ phóng đại, "Bức tranh toàn cảnh" | AI thường viết bối cảnh quá rộng và sáo rỗng |
| Phương pháp (Methods) | Bị động khiên cưỡng | AI thường dịch sai cấu trúc bị động tiếng Anh |
| Kết quả (Results) | Tính từ cảm xúc ("ấn tượng") | AI hay tự thêm nhận xét vào phần kết quả |
| Bàn luận (Discussion) | Lạm dụng từ nối ("Hơn thế nữa") | AI dùng từ nối để tạo cảm giác logic giả tạo |
| Kết luận (Conclusion) | Kết luận sáo rỗng, hứa hẹn tương lai | AI thường không biết cách chốt lại vấn đề cụ thể |
| Tóm tắt (Abstract) | Tất cả các mẫu trên | Đây là phần quan trọng nhất, cần viết cô đọng |

---

## Quick Checklist (Trước khi nộp bài)

### English
- [ ] No "Additionally" / "Furthermore" at sentence start (> 2 times)
- [ ] No "pivotal" / "crucial" / "landscape" / "delve"
- [ ] No "-ing" phrases tacked on for fake depth
- [ ] No "serves as" / "stands as" (use "is")
- [ ] No vague "Studies have shown" (cite specific study)
- [ ] No generic positive conclusion
- [ ] Consistent terminology (not synonym cycling)
- [ ] Em dashes used sparingly (< 2 per page)
- [ ] Hedging is proportionate to evidence

### Tiếng Việt
- [ ] Không lạm dụng "Hơn thế nữa", "Thêm vào đó" ở đầu câu.
- [ ] Không có các từ ngữ phóng đại (đột phá, kỷ nguyên mới, vô cùng quan trọng).
- [ ] Không dùng câu bị động khiên cưỡng kiểu tiếng Anh.
- [ ] Kết luận đi thẳng vào vấn đề, không có câu kết sáo rỗng kiểu "hy vọng trong tương lai".
- [ ] Các thuật ngữ y khoa/khoa học được sử dụng chính xác, thống nhất.

---

## References

- Wikipedia: Signs of AI writing
- matsuikentaro1/humanizer_academic (English academic patterns)
- humanizer-vi (Vietnamese patterns, --academic mode)
- Fitchett D, et al. Circulation. 2019;139(11):1384-1395. (Example source, CC-BY-4.0)


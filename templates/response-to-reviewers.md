# Response to Reviewers Template

## How to Use This Template

1. Copy this template for each revision round
2. Replace placeholders (marked with `[BRACKETS]`) with your content
3. Number every reviewer comment sequentially
4. Include specific page/line numbers for every change
5. Use the cover letter (separate template) for the editor; this document is the detailed point-by-point response

---

## Cover Page

**Manuscript ID:** [MANUSCRIPT-ID]
**Title:** [Full Manuscript Title]
**Journal:** [Journal Name]
**Revision Round:** [First Revision / Second Revision / etc.]
**Date:** [YYYY-MM-DD]

Dear Editor and Reviewers,

We sincerely thank you and the reviewers for the constructive feedback on our manuscript. We have carefully addressed all comments and believe the manuscript has been substantially improved. Below, we provide a detailed point-by-point response to each comment.

**Formatting convention used in this document:**
- **Reviewer comments** are shown in **bold**
- Our responses are in regular text
- Direct quotations from the revised manuscript are shown in > blockquotes
- New or modified text is highlighted with *italics* where applicable

---

## Reviewer 1

### General Comments

**Reviewer 1, General Comment:**
**[Paste the reviewer's general comment here verbatim]**

**Our Response:**
[Your response here. Thank the reviewer for their overall assessment. Address any broad concerns before moving to specific points.]

---

### Specific Comments

#### Comment 1.1

**Reviewer 1, Comment 1:**
**[Paste the specific comment here verbatim]**

**Our Response:**
[Your detailed response]

**Changes Made:**
[Description of what was changed, with specific locations]
- Page [X], Lines [Y-Z]: [Description of change]
- See revised manuscript, Section [X.X]

> [Quote the new/revised text from the manuscript]

---

#### Comment 1.2

**Reviewer 1, Comment 2:**
**[Paste the specific comment here verbatim]**

**Our Response:**
[Your detailed response]

**Changes Made:**
- Page [X], Lines [Y-Z]: [Description of change]

---

## Reviewer 2

### General Comments

**Reviewer 2, General Comment:**
**[Paste the reviewer's general comment here verbatim]**

**Our Response:**
[Your response]

---

### Specific Comments

#### Comment 2.1

**Reviewer 2, Comment 1:**
**[Paste the specific comment here verbatim]**

**Our Response:**
[Your detailed response]

**Changes Made:**
- Page [X], Lines [Y-Z]: [Description of change]

---

## Reviewer 3

*(Copy the same structure as above for each additional reviewer)*

---

## Summary of All Changes

| Section | Change Description | Triggered By |
|---------|-------------------|-------------|
| Abstract | [Brief description] | Reviewer 1, Comment 3 |
| Introduction | [Brief description] | Reviewer 2, Comment 1 |
| Methods | [Brief description] | Reviewer 1, Comment 5; Reviewer 3, Comment 2 |
| Results | [Brief description] | Reviewer 2, Comment 4 |
| Discussion | [Brief description] | Reviewer 1, Comment 7 |
| References | [Brief description] | Reviewer 3, Comment 6 |
| Supplementary | [Brief description] | Reviewer 2, Comment 8 |

---

## Best Practices for Responding to Reviewers

### Tone and Approach

1. **Always thank the reviewer** -- even for harsh or seemingly unfair comments. Every comment is an opportunity to strengthen your paper.
2. **Be respectful and professional.** Never be defensive, dismissive, or sarcastic.
3. **Be specific.** Vague responses like "We have revised the manuscript accordingly" are insufficient. State exactly what changed and where.
4. **Quote your revisions.** Show the reviewer the new text so they do not have to hunt for changes.
5. **Address every single point.** Do not skip or combine comments unless they are genuinely identical.

### Handling Different Comment Types

#### (a) Easy Fixes (Typos, Clarifications, Formatting)

**Strategy:** Fix immediately, respond briefly, show the change.

**Example:**

**Reviewer Comment:**
**"There is a typo in line 142: 'pateints' should be 'patients'."**

**Our Response:**
We thank the reviewer for catching this error. We have corrected the typo.

**Changes Made:**
- Page 6, Line 142: Corrected "pateints" to "patients"

---

#### (b) Disagreements with the Reviewer

**Strategy:** Acknowledge the reviewer's perspective, provide evidence-based reasoning for your position, offer a compromise if possible. Never say "the reviewer is wrong."

**Example:**

**Reviewer Comment:**
**"The authors should use a random forest model instead of logistic regression, as it would likely perform better."**

**Our Response:**
We appreciate the reviewer's suggestion regarding model selection. We chose logistic regression deliberately for the following reasons: (1) our primary goal was interpretability for clinical decision-making rather than maximal predictive performance (Smith et al., 2024); (2) our sample size (n=187) is relatively small, and logistic regression is more robust to overfitting in this setting (Hastie et al., 2009); and (3) the clinical guidelines in this domain require transparent, auditable models (FDA, 2023).

However, following the reviewer's suggestion, we have added a random forest comparison in the supplementary materials (Supplementary Table S3) to demonstrate that the performance difference is not clinically significant (AUC 0.82 vs. 0.84, p=0.31).

**Changes Made:**
- Page 12, Lines 267-270: Added justification for model selection
- Supplementary Table S3: Added random forest comparison results

---

#### (c) Requests for Additional Experiments/Analyses

**Strategy:** If feasible, do the analysis. If not feasible, explain why clearly and offer an alternative.

**Example (Feasible):**

**Reviewer Comment:**
**"The authors should perform a subgroup analysis by age group."**

**Our Response:**
We thank the reviewer for this excellent suggestion. We have performed the requested subgroup analysis, stratifying by age (<65 vs. ≥65 years). The results are presented in the new Table 3 and discussed in the Results section (Page 9, Lines 198-212).

**Example (Not Feasible):**

**Reviewer Comment:**
**"The authors should validate their model on an external dataset."**

**Our Response:**
We agree that external validation would strengthen the study. Unfortunately, no comparable external dataset with the required variables is currently available to our team. We have: (1) added internal validation using 5-fold cross-validation (new Table 4); (2) clearly stated this limitation in the Discussion (Page 14, Lines 312-318); and (3) identified external validation as a priority for future work. We are actively pursuing a collaboration with [Institution] to obtain an independent validation cohort.

---

#### (d) Conflicting Reviewer Opinions

**Strategy:** Acknowledge both perspectives transparently. Explain which approach you chose and why. Let the editor arbitrate if needed.

**Example:**

**Reviewer 1 Comment:**
**"The Discussion is too long and should be shortened."**

**Reviewer 3 Comment:**
**"The Discussion lacks depth and should explore more implications."**

**Our Response to Reviewer 1:**
We thank the reviewer for this feedback. We have streamlined the Discussion by removing redundant comparisons with prior literature (approximately 300 words removed). However, as Reviewer 3 requested additional depth on clinical implications, we have added a focused paragraph on implementation considerations (Page 15, Lines 340-355). The net result is a Discussion that is approximately 150 words shorter but more focused and substantive.

**Our Response to Reviewer 3:**
We appreciate this suggestion and have added a new paragraph discussing clinical implementation implications (Page 15, Lines 340-355). We have balanced this addition with streamlining other parts of the Discussion per Reviewer 1's feedback to maintain an appropriate length.

---

## Common Reviewer Comments and Example Responses

| Common Comment | Response Strategy |
|---------------|-------------------|
| "The sample size is too small" | Acknowledge limitation, provide power analysis, add to limitations section |
| "The literature review is incomplete" | Add missing references, explain your search strategy |
| "The statistical method is inappropriate" | Justify your choice with references, or add the suggested analysis |
| "The clinical significance is unclear" | Add effect sizes, NNT, or clinical context |
| "The writing needs improvement" | Have a native speaker review, or use professional editing service |
| "More details needed in Methods" | Add the requested details, refer to supplementary if space is limited |
| "The figures are unclear" | Redesign with higher resolution, clearer labels, and better color choices |

---

## Phần Tiếng Việt: Mẫu Phản hồi Phản biện

### Định dạng Cơ bản

**Mã số bản thảo:** [MANUSCRIPT-ID]
**Tiêu đề:** [Tiêu đề bản thảo]
**Tên tạp chí:** [Tên tạp chí]
**Lần chỉnh sửa:** [Lần 1 / Lần 2]
**Ngày:** [Ngày, Tháng, Năm]

---

Kính gửi Ban Biên tập và các Phản biện,

Chúng tôi xin chân thành cảm ơn Quý vị đã dành thời gian đọc và đưa ra những nhận xét mang tính xây dựng cho bản thảo của chúng tôi. Chúng tôi đã xem xét kỹ lưỡng tất cả các góp ý và tiến hành chỉnh sửa bản thảo một cách cẩn thận. Dưới đây là phản hồi chi tiết cho từng nhận xét của phản biện.

**Quy ước trình bày trong tài liệu này:**
- **Nhận xét của phản biện** được in **đậm**
- Phản hồi của chúng tôi ở định dạng văn bản thường
- Trích dẫn trực tiếp từ bản thảo đã chỉnh sửa được đặt trong khối trích dẫn (>)

---

### Phản biện 1

#### Nhận xét 1.1

**Phản biện 1, Nhận xét 1:**
**[Sao chép nguyên văn nhận xét của phản biện]**

**Phản hồi của chúng tôi:**
[Cung cấp câu trả lời cụ thể của bạn]

**Các thay đổi đã thực hiện:**
- Trang [X], Dòng [Y-Z]: [Mô tả nội dung thay đổi]

> [Trích dẫn đoạn văn bản mới/đã chỉnh sửa từ bản thảo]

---

### Các Điểm Cần Lưu Ý Khi Trả Lời (Tiếng Việt)

1. **Sử dụng từ ngữ lịch sự, tôn trọng** -- Luôn xưng hô trang trọng với Ban Biên tập và Phản biện.
2. **Luôn bắt đầu bằng sự đồng tình (nếu có thể)** -- "Chúng tôi hoàn toàn đồng ý với nhận xét này..."
3. **Luôn ghi rõ số trang và dòng cụ thể**
4. **Phản biện một cách lịch sự** -- "Chúng tôi hiểu quan ngại của phản biện, tuy nhiên vì những lý do sau..."
5. **Nêu rõ kết quả nếu có phân tích bổ sung**

### Ví Dụ Phản Hồi Các Nhận Xét Phổ Biến

#### Phản hồi về cỡ mẫu nhỏ

**Nhận xét của phản biện:**
**"Cỡ mẫu nghiên cứu quá nhỏ, gây nghi ngờ về khả năng tổng quát hóa của kết quả."**

**Phản hồi của chúng tôi:**
Chúng tôi xin cảm ơn phản biện về nhận xét này. Chúng tôi nhận thức được rằng cỡ mẫu của nghiên cứu (n=XX) là tương đối nhỏ. Tuy nhiên, dựa trên phân tích lực lượng mẫu (power analysis) được thực hiện từ trước, cỡ mẫu cần thiết để đạt độ kết quả 80% cho biến số chính là XX, do đó nghiên cứu của chúng tôi đã đáp ứng tiêu chí này (bổ sung ở Trang [X], Dòng [Y]). Đồng thời, chúng tôi cũng đã ghi rõ hạn chế về cỡ mẫu trong phần Bàn luận (Trang [X], Dòng [Y-Z]).

#### Phản hồi về phương pháp thống kê

**Nhận xét của phản biện:**
**"Không có sự hiệu chỉnh cho so sánh nhiều lần (multiple comparisons)."**

**Phản hồi của chúng tôi:**
Đây là một góp ý rất quan trọng và chúng tôi xin chân thành cảm ơn. Theo gợi ý của phản biện, chúng tôi đã áp dụng hiệu chỉnh Bonferroni và tiến hành phân tích lại. Sau khi hiệu chỉnh, các kết quả chính vẫn không thay đổi (Xem Bảng 2 đã chỉnh sửa). Chúng tôi đã cập nhật phần Phương pháp (Trang [X], Dòng [Y]) và phần Kết quả (Trang [X], Dòng [Y]).

#### Phản hồi về ý nghĩa lâm sàng

**Nhận xét của phản biện:**
**"Mặc dù có ý nghĩa thống kê, nhưng ý nghĩa lâm sàng chưa rõ ràng."**

**Phản hồi của chúng tôi:**
Chúng tôi rất trân trọng nhận xét này. Để làm rõ ý nghĩa lâm sàng, chúng tôi đã bổ sung effect size (Cohen's d = X.XX) và chỉ số NNT (NNT = XX) (Trang [X], Dòng [Y-Z]). Ngoài ra, trong phần Bàn luận, chúng tôi đã viết thêm một đoạn phân tích cụ thể về việc kết quả này có ý nghĩa như thế nào trong thực hành lâm sàng thực tế (Trang [X], Dòng [Y-Z]).

---

## Checklist Before Submitting Response

- [ ] Every reviewer comment has been addressed individually
- [ ] All responses include specific page and line numbers
- [ ] Revised text is quoted where appropriate
- [ ] Tone is respectful and professional throughout
- [ ] Summary table of changes is complete
- [ ] Cover letter (separate document) references this response
- [ ] Co-authors have reviewed and approved the response
- [ ] Track changes are enabled in the revised manuscript
- [ ] Supplementary materials are updated if applicable
- [ ] Response document is formatted per journal requirements

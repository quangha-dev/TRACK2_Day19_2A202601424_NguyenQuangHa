# Reflection — Lab 19

**Tên:** Nguyễn Quang Hà
**Cohort:** A20-K4
**Path đã chạy:** lite

---

## Câu hỏi (≤ 200 chữ)

> Trên golden set 50 queries, mode nào thắng ở loại query nào (`exact` /
> `paraphrase` / `mixed`), và tại sao? Khi nào bạn **không** dùng hybrid
> (i.e. khi nào pure BM25 hoặc pure vector là lựa chọn đúng)?

Tôi đánh giá 50 truy vấn bằng Precision@10. Hybrid thắng toàn cục với 80,8%,
cao hơn Vector 80,4% và BM25 77,8%. Với `exact`, Hybrid đạt 98,0%; nếu chỉ
chọn bộ truy hồi thuần, BM25 (96,7%) vẫn hơn Vector (95,3%) vì token kỹ
thuật xuất hiện nguyên văn. Với `paraphrase`, Vector thắng ở 43,3%, so với
Hybrid 41,3% và BM25 33,3%, nhờ ensemble embedding giữ được nghĩa tiếng
Việt. Với `mixed`, Hybrid thắng ở 97,5%; hai mode thuần cùng đạt 97,0%.

Tôi chọn pure BM25 cho exact query khi cần latency thấp, chi phí nhỏ và khả
năng giải thích cao. Tôi chọn pure Vector khi người dùng thường diễn đạt lại
hoặc corpus đa ngôn ngữ, ít token trùng. Tôi dùng Hybrid làm mặc định cho lưu
lượng hỗn hợp, code-switching hoặc sai chính tả.

---

## Điều ngạc nhiên nhất khi làm lab này

Tôi bất ngờ khi E5-large tăng Vector lên 92,2% nhưng làm Hybrid giảm còn
87,0%; model mạnh hơn chưa chắc tạo hệ thống tốt hơn.

---

## Bonus challenge

- [ ] Đã làm bonus (xem `bonus/`)
- [ ] Pair work với: Không

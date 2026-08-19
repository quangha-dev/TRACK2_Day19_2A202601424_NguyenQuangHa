# Báo cáo nghiệm thu Lab 19

**Sinh viên:** Nguyễn Quang Hà  
**Cohort:** A20-K4  
**Môi trường:** Lite, Qdrant in-memory, Feast SQLite, CPU  
**Phạm vi:** Core NB1–NB4 và Advanced NB5–NB8

## Kết luận

Tôi đã chạy và lưu output cho cả tám notebook. Bộ smoke test in `All checks
passed`; bộ unit test có 43 test đạt. Tôi dùng rubric Codelab 70+30 làm chuẩn
nghiệm thu vì rubric này khớp yêu cầu nộp bài hiện hành.

## Core — 70 điểm

| Notebook | Bằng chứng đã đo | Trạng thái |
|---|---|---|
| NB1 | Corpus và collection có 1.000 vector; top-5 keyword đã in; paraphrase không chứa “cloud” trả 5/5 tài liệu cloud | Đạt |
| NB2 | RRF dùng rank 1-based và `1/(k+rank)`; BM25 77,8%, Vector 80,4%, Hybrid 80,8% | Đạt |
| NB2 slice | Exact: BM25 96,7% > pure Vector 95,3%; paraphrase: Vector 43,3% cao nhất; mixed: Hybrid 97,5% cao nhất | Đạt |
| NB3 | `/search` trả `SearchResponse` có `latency_ms`; P99 hybrid 46,1 ms sau warm-up, thấp hơn ngưỡng 50 ms | Đạt |
| NB4 | Ba feature view đã đăng ký/materialize; `u_001` trả dict hợp lệ; online P99 5,90 ms; PIT join đủ 3 dòng | Đạt |
| Tái lập | `make verify-lite`, `make test`, `make benchmark`, `make notebooks` là chuỗi nghiệm thu bắt buộc | Đạt |

Với NB2, tôi đã so sánh ba lựa chọn trước khi chốt: baseline tiếng Anh cho
paraphrase 24,0%; E5-large cho Vector tổng 92,2% nhưng Hybrid chỉ 87,0%;
MiniLM đơn cho paraphrase 48,0% nhưng làm mixed giảm. Tôi chọn pure-vector
ensemble RRF giữa baseline và MiniLM. Sweep 12 cấu hình cho thấy depth 50,
k=60 đạt 80,8%, cao nhất và giữ hằng số RRF chuẩn.

## Advanced — 30 điểm

| Notebook | Bằng chứng đã đo | Trạng thái |
|---|---|---|
| NB5 | Lọc chặt 3,8%: post-filter recall 0,00, Filtered-ANN 1,00; `fetch_k=500` (50% corpus) mới phục hồi 1,00 | Đạt |
| NB6 | Cùng budget 16 docs: single-shot recall/balance 0,526/0,08; agentic no-filter 0,906/0,93; có-filter 0,823/0,76; context in feature và `doc_ids` | Đạt |
| NB7 | Sweep có saving/false-hit; ngưỡng 0,85 cho 100% saving và 0% false-hit; 0,75 còn 36% false-hit; demo tenant leak/MISS an toàn | Đạt |
| NB8 | `session_id` target-naive gap 0,477, in-fold -0,003; 98,2% dòng latest bị rò; AUC latest/PIT 0,715/0,595; ODFV đổi theo amount | Đạt |
| Kiểm thử | `make test` và `make verify-lite` đều xanh | Đạt |

## Lưu ý trước khi nộp

Tôi chưa làm bonus vì bonus nằm ngoài 100 điểm Core + Advanced. Ảnh chụp màn
hình phải do sinh viên chụp từ Jupyter; danh sách ảnh và lệnh nằm trong
`submission/RUNBOOK.md`.

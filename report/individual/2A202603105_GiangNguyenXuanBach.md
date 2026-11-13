# Báo cáo cá nhân — HoVaTen-MSSV

Đổi tên file theo quy tắc `MSSV_HoTen.md`. Ví dụ: `20241234_NguyenVanAn.md`.

Đoạn video: MOT17-09, 150 frame (frame 1–150), nguồn MOTChallenge, giấy phép CC BY-NC-SA 3.0.

## 0. Thông tin học viên

- Họ tên:Giang Nguyễn Xuân Bách
- MSSV:GiangNguyenXuanBach-2A202603105
- Mã đề (A/B/C): C
- Email:gnxuanbach@gmail.com
- Link repository:https://github.com/gnxuanbach/K5-L2-Day05-GiangNguyenXuanBach-2A202603105-MOTTracking
- Giờ bắt đầu:16h40
- Giờ kết thúc:19h30

## 1. Xem trước đoạn video (CP0)

Ghi **trước khi vẽ**, mỗi người một dòng.

| Mã | Frame xuất hiện | Frame cuối thấy được | Rẽ / dừng / đổi tốc độ ở frame | Bị che ở frame | Ghi chú |
|---|---|---|---|---|---|
| P1 |0 |149 |10 | 40| |
| P2 | 60| 149 |100 |60 | Bị kính và bàn che gần 1/3 người|
| P3 | 0| 149| không có | không có | |
| P4 |0 |105 |37 |103 | |
| P5 |0 |149 | không có |118 | |

## 2. Keyframe và thời gian (CP1, CP4)

Số keyframe lấy từ kết quả `src/check_submission.py`.

| Mã | Số keyframe | Keyframe ở frame | Số frame có mặt | Keyframe / 100 frame | Thời gian (phút) | Chỗ khó |
| --- | --- | --- | --- | --- | --- | --- |
| P1 | 18 | 0, 10, 20, 30, 48, 50, 60, 70, 80, 90, 100, 103, 110, 112, 120, 130, 140, 149 | 142 | 12.7 | 10 | Bị che ở frame 40–47, cần bật cờ outside và occluded chuẩn xác |
| P2 | 11 | 60, 70, 80, 90, 100, 103, 110, 120, 130, 140, 149 | 90 | 12.2 | 7 | Xuất hiện muộn ở frame 60, bị bàn/kính che gần 1/3 người |
| P3 | 21 | 0, 10, 20, 30, 40, 50, 60, 70, 80, 90, 99, 100, 102, 103, 104, 110, 114, 119, 129, 139, 149 | 150 | 14.0 | 10 | Đi từ xa lại gần ở rìa phải, kích thước thay đổi liên tục |
| P4 | 10 | 0, 10, 20, 30, 40, 50, 80, 90, 100, 103 | 106 | 9.4 | 6 | bị che khuất hẳn khỏi khung hình ở frame 106, cần xác định đúng frame cuối |
| P5 | 50 | 0, 10, 20, 30, 36, 37, 38, 39, 40, 44, 46, 48, 50, 54, 55, 60, 65, 68, 69, 70, 74, 76, 78, 80, 86, 90, 95, 99, 100, 101, 102, 103, 104, 105, 106, 108, 110, 113, 114, 115, 117, 118, 119, 127, 129, 132, 133, 134, 135, 136 | 143 | 35.0 | 20 | Ở rất gần camera, di chuyển nhanh, kích thước biến đổi lớn và bị che ở frame 120–126 |
| Tổng | 110 | — | 631 | 17.4 | 53 | — |

Keyframe / 100 frame của cả bài = tổng keyframe ÷ tổng số frame có mặt × 100 = 110 ÷ 631 × 100 = 17.4

Bạn đặt keyframe nhiều nhất ở người nào? Vì sao (người đó rẽ, dừng, lại gần camera hay bị che)?

đặt keyframe nhiều nhất ở người P5, 50 keyframe, mật độ 35.0 KF/100 frame
Lý do: P5 đi ở cự ly rất gần camera, kích thước box chiếm tỉ lệ lớn trên khung hình và biến đổi kích thước nhanh theo từng bước di chuyển. Do chuyển động phi tuyến tính ở cự ly gần và có đoạn bị che khuất hoàn toàn ở frame 120–126


## 3. Đoạn bị che (CP2)

Người bị che: `P1`

| Mốc | Frame |
|---|---:|
| Bắt đầu bị che một phần (bật `occluded`) | 30 |
| Mất hẳn (bật `outside`) | 40 |
| Hiện lại (tắt `outside`) | 48 |
| Thấy rõ trở lại (tắt `occluded`) | 60 |

- Thời gian khuất hẳn: 8 frame (từ frame 40 đến 47) = 0.27 giây.
- Quyết định: giữ cùng ID.
- Lý do (trả lời 3 câu: khuất bao lâu so với 60 frame, ngoại hình có khớp, chỗ hiện lại có đúng hướng và tốc độ):
  1. **Thời gian khuất:** người P1 chỉ bị khuất hẳn 8 frame, ngắn hơn rất nhiều so với ngưỡng quy định của lớp là 60 frame .
  2. **Ngoại hình:** Trang phục, vóc dáng, màu sắc áo quần và phụ kiện hoàn toàn trùng khớp trước và sau khi bị che
  3. **Vị trí và hướng di chuyển:** vị trí xuất hiện trở lại ở frame 48 hoàn toàn liền mạch với hướng đi và tốc độ trước khi bị che ở frame 40

Ảnh chụp màn hình:

![Trước khi che](images/che_1_truoc.png)
![Giữa đoạn che, thấy cờ trên panel object](images/che_2_giua.png)
![Sau khi hiện lại, cùng ID](images/che_3_sau.png)



## 4. Tự review ID (CP3)

Lượt 1 theo người (đi ngược từ frame 149 về 0 trên CVAT), lượt 2 theo cảnh (nhảy 10 frame). Ít nhất 3 dòng; không có lỗi thì ghi một dòng "đã kiểm hai lượt, không lỗi".

Loại lỗi dùng đúng một trong 7 mã: `id_switch`, `fragmentation`, `lost`, `merge`, `false_track`, `drift`, `flag`.

| Frame | Mã người | Loại lỗi | Mô tả một câu | Phát hiện ở lượt | Đã sửa? |
|---:|---|---|---|---|---|
| 35–39 | P1 | `drift` | box đi trước người 1 khoảng do  giảm tốc độ | Lượt 1 | Đã sửa (thêm keyframe và chỉnh lại tọa độ box) |
| 120–126 | P5 | `flag` | không bật cờ outside khi đối tượng bị che mất hoàn toàn | Lượt 1 | Đã sửa (bật outside ở frame 120 và tắt ở 127) |
| 80–90 | P3 | `drift` | box đi trước người 1 khoảng do  giảm tốc độ  | Lượt 1 | Đã sửa (thêm keyframe và chỉnh lại tọa độ box) |

Tổng hợp số lỗi theo loại:

| `id_switch` | `fragmentation` | `lost` | `merge` | `false_track` | `drift` | `flag` |
|---:|---:|---:|---:|---:|---:|---:|
| 0 | 0 | 0 | 0 | 0 | 2 | 1 |

Lỗi nào chỉ lượt 2 (theo cảnh) mới thấy, lượt 1 (theo người) không thấy? Vì sao?

lỗi `drift` do thay đổi tốc độ dễ nhận biết ở lượt 2 hơn. Khi review lượt 1 theo từng người mắt tập trung liên tục vào một đối tượng cụ thể nên khó nhận ra box bị trôi chậm hay lệch tâm

## 5. File xuất và kết quả tự kiểm (CP4)

| Kiểm tra | Kết quả |
|---|---|
| Tên file MOT 1.1 | GiangNguyenXuanBach_mot.zip |
| Tên file CVAT for video 1.1 | GiangNguyenXuanBach_cvat_video.zip |
| Số track ID khác nhau trong `gt/gt.txt` (phải là 5) | 5 |
| Frame `outside` không có dòng trong `gt.txt` (đúng / sai) | đúng |
| Job đã completed trên CVAT máy cá nhân | Đã completed |

Dán phần tóm tắt in ra từ `src/check_submission.py`:


Số frame in theo CVAT (bắt đầu từ 0). Trong gt.txt, frame_id = frame CVAT + 1.

=== File MOT 1.1: GiangNguyenXuanBach_mot.zip ===
  Số track ID: 5   |   Tổng số box: 631
  [OK]        Đúng 5 track ID.

  Track | Frame có mặt | Số frame | Đoạn vắng (outside)
      1 |   0–149      |      143 | 120–126
      2 |   0–149      |      142 | 40–47
      3 |   0–149      |      150 | -
      4 |   0–105      |      106 | -
      5 |  60–149      |       90 | -


=== File CVAT for video 1.1: GiangNguyenXuanBach_cvat_video.zip ===

  Track | Nhãn   | Frame thấy | Keyframe | KF/100 frame | Frame occluded | Lần bật outside
      0 | person |        143 |       50 |         35.0 |             31 |               1
              Track 0: keyframe ở frame [0, 10, 20, 30, 36, 37, 38, 39, 40, 44, 46, 48, 50, 54, 55, 60, 65, 68, 69, 70, 74, 76, 78, 80, 86, 90, 95, 99, 100, 101, 102, 103, 104, 105, 106, 108, 110, 113, 114, 115, 117, 118, 119, 127, 129, 132, 133, 134, 135, 136]
      1 | person |        142 |       18 |         12.7 |             22 |               1
              Track 1: keyframe ở frame [0, 10, 20, 30, 48, 50, 60, 70, 80, 90, 100, 103, 110, 112, 120, 130, 140, 149]
      2 | person |         90 |       11 |         12.2 |             10 |               0
              Track 2: keyframe ở frame [60, 70, 80, 90, 100, 103, 110, 120, 130, 140, 149]
      3 | person |        150 |       21 |         14.0 |             30 |               0
              Track 3: keyframe ở frame [0, 10, 20, 30, 40, 50, 60, 70, 80, 90, 99, 100, 102, 103, 104, 110, 114, 119, 129, 139, 149]
      4 | person |        106 |       10 |          9.4 |              3 |               1
              Track 4: keyframe ở frame [0, 10, 20, 30, 40, 50, 80, 90, 100, 103]

  Tổng: 110 keyframe / 631 frame có mặt = 17.4 keyframe / 100 frame
  [OK]        Đọc được 5 track từ annotations.xml.

=== Tóm tắt ===
  Lỗi: 0   |   Cảnh báo: 0
  Đạt. Dán phần tóm tắt này vào báo cáo mục 5.


## 6. Ba câu kết

1. Nếu được gán lại, bạn sẽ đặt keyframe khác ở đâu? Vì sao?

   tôi hài lòng với keyframe hiện tại và không thấy cần thiết phải đặt keyframe khác

2. Có chỗ nào bạn không chắc "cùng ID hay ID mới"? Bạn đã quyết định và ghi chú thế nào?

   không có chỗ nào vì frame vật khuất ngắn, obj không thay đổi 

3. Một lỗi ID trong job của bạn (nếu không còn sót, chọn lỗi đã sửa) có thể làm xe tự lái dự đoán sai chuyển động của người đó như thế nào? Lỗi đó ảnh hưởng MOTA hay IDF1 nhiều hơn?

job của tôi không mắc lỗi sai ID nào, cả 5 đối tượng P1–P5 đều duy trì đúng duy nhất 1 Track ID xuyên suốt video

Tuy nhiên vị trí có nguy cơ cao nhất là đoạn P5 bị che khuất hoàn toàn ở frame 120–126: Nếu người gán nhãn bất cẩn tạo ra một Track ID mới khi P5 bước ra ở frame 127 (lỗi fragmentation / id_switch):

Ảnh hưởng đến xe tự lái: Hệ thống tự hành sử dụng các thuật toán dự đoán quỹ đạo dựa trên chuỗi lịch sử vị trí và vận tốc. Nếu bị đổi sang ID mới, xe sẽ coi người đó là một chướng ngại vật mới xuất hiện đột ngột với vận tốc ban đầu bằng 0 hoặc chưa xác định, thay vì một người đi bộ đang duy trì quán tính và hướng đi cắt ngang đường, dẫn đến tính toán sai thời gian, có thể khiến xe ra quyết định phanh gấp nguy hiểm hoặc xử lý chậm trễ khi nhường đường
Ảnh hưởng MOTA hay IDF1 nhiều hơn: Lỗi này ảnh hưởng  đến IDF1 nhiều hơn so với MOTA. MOTA chủ yếu đo lường độ chính xác phát hiện ở từng frame độc lập, chỉ bị trừ điểm ở 1 frame xảy ra ID switch, trong khi IDF1 đo lường khả năng liên kết và duy trì nhận dạng danh tính trên toàn bộ chiều dài quỹ đạo . Việc track của P5 bị bẻ gãy làm đôi sẽ làm giảm mạnh số lượng phát hiện được gán đúng ID gốc

## Bonus (nếu làm)

### B1 — Hai người đi sát

...

### B2 — So cách đặt keyframe

| Cách đặt | Số keyframe | Frame trôi nhất | Ghi chú |
|---|---:|---:|---|
| Đều mỗi 30 frame | | | |
| Theo chỗ đổi hướng | | | |

...

### B3 — So với tracker có sẵn

| Frame | Mã người | Tracker làm gì | Nhãn của bạn | Giải thích (đoán rồi sửa / ghép IoU / box score thấp / ngoại hình) |
|---:|---|---|---|---|
| | | | | |
| | | | | |

## 7. Tài liệu tham khảo và công cụ AI đã dùng

Bài giảng và Guideline Lab Ngày 5

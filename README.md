# AnhEmMamDuoi — Jetson AI Racer Challenge 2026

Mã nguồn dự thi **Jetson AI Racer Challenge 2026** của đội **AnhEmMamDuoi**.

## Mục tiêu

Xây dựng xe tự hành trên **JetRacer/Jetson Nano**, sử dụng một camera để hoàn thành hai nội dung:

- **Speed Track:** bám làn ổn định, hoàn thành vòng đua nhanh và duy trì tối thiểu 20 FPS.
- **Smart City:** bám làn, nhận biết đèn giao thông và biển báo để xử lý đúng tình huống.

## Giải pháp

Pipeline chính gồm:

```text
Camera → Nhận diện làn đường → PID điều khiển → Servo/động cơ
       → Nhận diện biển báo, đèn giao thông → FSM quyết định hành vi
```

Hệ thống ưu tiên độ ổn định và an toàn, hỗ trợ chạy offline bằng video, ghi log CSV và phân tích các chỉ số FPS, độ trễ, sai lệch làn.

## Cài đặt

Trên máy phát triển:

```bash
pip install -r requirements.txt
```

Trên Jetson Nano sử dụng môi trường JetPack có sẵn và chỉ cài thêm:

```bash
pip3 install PyYAML
```

## Chạy chương trình

Kiểm thử offline không cần xe:

```bash
python -m src.jetracer_baseline.cli replay --source synthetic --frames 200
python tests/test_smoke.py
```

Kiểm tra phần cứng trước khi chạy:

```bash
python3 tools/check_hardware.py --driver nvidia
```

Chạy bài thi Speed Track:

```bash
python3 -m src.jetracer_baseline.cli run --task speed --driver nvidia --record
```

Chạy bài thi Smart City:

```bash
python3 -m src.jetracer_baseline.cli run --task smartcity --driver nvidia --record
```

> Luôn kê bánh xe khỏi mặt đất khi kiểm tra servo hoặc động cơ lần đầu.

## Tài liệu

- [Phương pháp và giải pháp kỹ thuật](docs/phuong-phap-giai-phap-ky-thuat.md)
- [Quy trình kiểm thử xe](docs/quy-trinh-test-xe.md)
- [Kế hoạch thực nghiệm](docs/ke-hoach-thuc-nghiem.md)

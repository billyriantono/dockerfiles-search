# Tạo image từ baseimage là alpine bản 3.5 
FROM alpine:3.5

# Tiếp theo tiến hành cài đặt cac gói phụ thuộc, cần thiết.
RUN apk add --update py2-pip

# Liệt kê các thư viện cần thiết trong file, copy file vào image fs và cài đặt các thư viện trong file đó
COPY requirements.txt /usr/src/app/
RUN pip install --no-cache-dir -r /usr/src/app/requirements.txt

# Copy các file chương trình vào image
COPY app.py /usr/src/app/
COPY templates/index.html /usr/src/app/templates/

# Cấu hình port mà ứng dụng chạy, flask chạy ở port 5000
EXPOSE 5000

# Cấu hình chương trình mặc định khi chạy container với lệnh CMD
CMD ["python", "/usr/src/app/app.py"]


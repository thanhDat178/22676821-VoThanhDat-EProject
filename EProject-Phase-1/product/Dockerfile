# Sử dụng base image Node.js gọn nhẹ
FROM node:18-alpine

# Đặt thư mục làm việc bên trong container
WORKDIR /app

# Copy file package.json và package-lock.json để tận dụng cache
COPY package*.json ./

# Cài đặt các thư viện cần thiết
RUN npm install

# Copy toàn bộ code của service vào
COPY . .

# Mở port mà service sử dụng (rất quan trọng cho Docker Compose)
EXPOSE 3001

# Lệnh để khởi chạy ứng dụng (dựa theo script "start" trong package.json)
CMD ["npm", "start"]

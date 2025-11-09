# Gunakan image Node.js
FROM node:18-alpine

# Buat direktori kerja di dalam container
WORKDIR /app

# Salin package.json dan package-lock.json
COPY ../package.json ./
COPY ../package-lock.json ./

# Instal dependencies
RUN npm install --omit=dev

# Salin sisa kode backend
COPY . .

# Jalankan server
CMD ["npm", "start"]
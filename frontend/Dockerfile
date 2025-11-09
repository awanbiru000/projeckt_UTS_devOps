# --- Tahap 1: Build Aplikasi React ---
FROM node:18-alpine AS build

# Setel /app sebagai direktori kerja
WORKDIR /app

# Salin package.json dan package-lock.json
# (Sekarang mereka ada di root, bukan di 'src' lagi)
COPY package.json ./
COPY package-lock.json ./

# Instal dependencies
RUN npm install

# Salin *semua* file proyek sisanya
# (Ini akan menyalin 'src', 'public', 'index.html', 'vite.config.js', dll.)
COPY . .

# Jalankan build script
# (Kita tidak perlu --base=./ lagi karena strukturnya sudah standar)
RUN npm run build

# --- Tahap 2: Sajikan dengan NGINX ---
FROM nginx:stable-alpine

# Salin hasil build dari tahap sebelumnya ke folder NGINX
COPY --from=build /app/dist /usr/share/nginx/html

# Salin file konfigurasi NGINX kustom kita
COPY nginx/default.conf /etc/nginx/conf.d/default.conf

# Ekspos port 80
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
FROM node:20-alpine

# 1. สร้าง Group และ User
RUN addgroup -S app && adduser -S -G app app

# 2. สร้าง Directory และตั้งสิทธิ์ให้เรียบร้อย (ทำในฐานะ root)
WORKDIR /app
RUN chown app:app /app

# 3. สลับเป็น User app ทันที
USER app

# 4. Copy package.json โดยระบุเจ้าของเป็น app
# สำคัญ: ต้องใส่ --chown ทุกครั้งที่ COPY เพื่อไม่ให้ไฟล์เป็นของ root
COPY --chown=app:app package*.json ./

# 5. ตอนนี้รัน npm install ได้แล้ว เพราะ User app เป็นเจ้าของ /app
RUN npm install

# 6. Copy ไฟล์ที่เหลือทั้งหมดและตั้งสิทธิ์เป็น app
COPY --chown=app:app . .

EXPOSE 5173

CMD ["npm", "run", "dev", "--", "--host"]
# Simple Task Management System

ระบบจัดการงานแบบง่ายๆ ที่สร้างด้วย Next.js, Docker และ PostgreSQL

## 📋 Requirements

- Docker และ Docker Compose
- Node.js 20+ (สำหรับ development แบบ local)

## 🚀 Quick Start

### Development Mode

1. **คัดลอกไฟล์ environment variables:**
   ```bash
   cp env.example .env
   ```

2. **รันด้วย Docker Compose (Development):**
   ```bash
   docker-compose -f docker-compose.dev.yml up --build
   ```

   หรือใช้ npm script:
   ```bash
   npm run docker:dev
   ```

3. **เข้าถึงแอปพลิเคชัน:**
   - Next.js: http://localhost:3000
   - PostgreSQL: localhost:5432

### Production Mode

1. **สร้างไฟล์ .env และตั้งค่าตามต้องการ**

2. **รันด้วย Docker Compose (Production):**
   ```bash
   docker-compose up --build
   ```

   หรือใช้ npm script:
   ```bash
   npm run docker:prod
   ```

## 🛠️ Development (Local without Docker)

หากต้องการรัน Next.js แบบ local โดยใช้ PostgreSQL จาก Docker:

1. **รันเฉพาะ PostgreSQL:**
   ```bash
   docker-compose -f docker-compose.dev.yml up postgres -d
   ```

2. **รัน Next.js แบบ local:**
   ```bash
   npm install
   npm run dev
   ```

## 📦 Docker Commands

### Development
- `npm run docker:dev` - รัน development environment
- `npm run docker:dev:down` - หยุด development containers
- `npm run docker:dev:logs` - ดู logs

### Production
- `npm run docker:prod` - รัน production environment
- `npm run docker:prod:down` - หยุด production containers
- `npm run docker:prod:logs` - ดู logs

### Database
- `npm run db:reset` - ลบและสร้าง database ใหม่

## 🗄️ Database Connection

### Connection String Format
```
postgresql://[user]:[password]@[host]:[port]/[database]
```

### Default Values
- **User:** postgres
- **Password:** postgres
- **Database:** taskdb
- **Port:** 5432
- **Host:** localhost (local) หรือ postgres (Docker)

## 📁 Project Structure

```
.
├── app/                 # Next.js app directory
├── public/             # Static files
├── Dockerfile          # Production Docker image
├── Dockerfile.dev      # Development Docker image
├── docker-compose.yml  # Production compose file
├── docker-compose.dev.yml  # Development compose file
├── .dockerignore       # Docker ignore file
└── env.example         # Environment variables template
```

## 🔧 Environment Variables

สร้างไฟล์ `.env` จาก `env.example` และปรับแต่งตามต้องการ:

```env
POSTGRES_USER=postgres
POSTGRES_PASSWORD=postgres
POSTGRES_DB=taskdb
POSTGRES_PORT=5432
NEXTJS_PORT=3000
DATABASE_URL=postgresql://postgres:postgres@localhost:5432/taskdb
```

## 🐳 Docker Services

### PostgreSQL
- **Image:** postgres:16-alpine
- **Port:** 5432
- **Volume:** postgres_data (persistent storage)

### Next.js
- **Port:** 3000
- **Environment:** Development หรือ Production

## 📝 Notes

- ข้อมูล PostgreSQL จะถูกเก็บใน Docker volume และจะไม่หายเมื่อ restart container
- สำหรับ production ควรเปลี่ยนรหัสผ่านและค่าความปลอดภัยอื่นๆ
- Development mode จะมี hot-reload และ volume mounting

## 🆘 Troubleshooting

### Port already in use
หาก port 3000 หรือ 5432 ถูกใช้งานแล้ว ให้เปลี่ยนค่าในไฟล์ `.env`

### Database connection error
ตรวจสอบว่า PostgreSQL container ทำงานอยู่:
```bash
docker-compose ps
```

### Clear Docker volumes
```bash
docker-compose down -v
```

## 📄 License

MIT

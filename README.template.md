# {PROJE_ADI}

> **{PROJE_KISA_AÇIKLAMASI}**

[![.NET](https://img.shields.io/badge/.NET-8.0-purple)](https://dotnet.microsoft.com/)
[![License](https://img.shields.io/badge/license-Proprietary-red)](LICENSE)
[![Status](https://img.shields.io/badge/status-active-success)](https://github.com/yourusername/yourproject)

## 📋 İçindekiler

- [Proje Hakkında](#-proje-hakkında)
- [Teknoloji Stack](#-teknoloji-stack)
- [Mimari](#-mimari)
- [Kurulum](#-kurulum)
- [Kullanım](#-kullanım)
- [API Dokümantasyonu](#-api-dokümantasyonu)
- [Database](#-database)
- [Özellikler](#-özellikler)
- [Geliştirme](#-geliştirme)
- [Deployment](#-deployment)
- [Lisans](#-lisans)

---

## 🎯 Proje Hakkında

{PROJE_DETAYLI_AÇIKLAMASI}

### Temel Özellikler

- ✅ RESTful API mimarisi
- ✅ JWT Authentication & Authorization
- ✅ Çoklu dil desteği (TR, EN, DE, ...)
- ✅ Real-time bildirimler (SignalR)
- ✅ Background job sistemi (Quartz.NET)
- ✅ Rate limiting ve DDoS koruması
- ✅ Soft delete ve audit trail
- ✅ API versioning
- ✅ Comprehensive logging (Serilog)
- ✅ Cache management (Redis/Memory)
- ✅ File storage (Azure Blob / Local)
- ✅ SMS/Email notifications
- ✅ Auto-generated API documentation (Swagger)

### Hedef Kitle

{HEDEF_KİTLE_AÇIKLAMASI}

---

## 🛠️ Teknoloji Stack

### Backend Framework

| Teknoloji | Versiyon | Açıklama |
|-----------|----------|----------|
| ASP.NET Core | 8.0 | Web API Framework |
| Entity Framework Core | 9.0 | ORM |
| Maggsoft Framework | 2.x | Custom Enterprise Framework |

### Core Libraries

| Kütüphane | Versiyon | Amaç |
|-----------|----------|------|
| **Maggsoft.Core** | 2.1.7 | Core utilities ve base classes |
| **Maggsoft.Data** | 2.1.7 | Data access abstractions |
| **Maggsoft.Framework** | 2.6.3 | Middleware, helpers, extensions |
| **Maggsoft.Mssql** | 2.1.5 | SQL Server specific implementations |
| **Maggsoft.Mssql.Services** | 2.1.0 | Service layer base classes |
| **Maggsoft.Cache** | 2.1.0 | Caching abstractions |
| **Maggsoft.Cache.MemoryCache** | 2.0.7 | In-memory cache implementation |

### Authentication & Authorization

- **Microsoft.AspNetCore.Identity** (8.0.0)
- **JWT Bearer Token** authentication
- Role-based authorization
- Custom identity error describer (localized)

### Database & ORM

- **Microsoft SQL Server** (2022)
- **Entity Framework Core** (9.0.0)
- **FluentMigrator** (6.2.0) - Database migrations
- Global query filters (soft delete)
- AsNoTracking for performance

### Validation

- **FluentValidation** (11.3.0)
- Localized error messages
- Custom validators
- Async validation support

### Logging

- **Serilog** (8.0.1)
- Console sink (development)
- MSSQL sink (production)
- Structured logging
- Request/Response logging
- User activity logging

### Background Jobs

- **Quartz.NET** (3.8.0)
- Scheduled jobs (cron expressions)
- Event-driven jobs
- Job persistence
- Job monitoring

### Real-time Communication

- **SignalR**
- WebSocket support
- JWT authentication for hubs
- Connection management
- Group messaging

### Caching & Queue

- **StackExchange.Redis** (2.7.17)
- Distributed caching
- Message queue (optional)
- Pub/Sub (optional)

### Object Mapping

- **AutoMapper** (13.0.1)
- Entity ↔ DTO mapping
- ProjectTo for LINQ queries
- Custom resolvers

### API Documentation

- **Swashbuckle.AspNetCore** (7.1.0)
- Swagger UI
- API versioning support
- JWT authentication support
- XML comments

### Security

- **AspNetCoreRateLimit** (5.0.0) - Rate limiting
- **Security headers middleware**
- HTTPS enforcement
- CORS policy
- IP filtering

### Cloud Services (Optional)

- **Azure.Storage.Blobs** (12.25.0) - File storage
- Azure App Service ready
- Environment variable configuration

### Testing & Development

- **Bogus** (35.6.3) - Test data generation
- **xUnit** - Unit testing framework
- **Moq** - Mocking framework
- **k6** - Load testing

---

## 🏗️ Mimari

### Clean Architecture (Modified)

Proje, Clean Architecture prensiplerini Maggsoft Framework ile adapte ederek kullanır:

```
┌─────────────────────────────────────────────────────────┐
│                    Presentation Layer                    │
│  ┌───────────────────────────────────────────────────┐  │
│  │  API Controllers, SignalR Hubs, Validators        │  │
│  │  Middleware, Filters, Services (JWT, Seed, etc.)  │  │
│  └───────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────┘
                           ↓
┌─────────────────────────────────────────────────────────┐
│                   Service Layer                          │
│  ┌───────────────────────────────────────────────────┐  │
│  │  Business Logic Services                          │  │
│  │  Interfaces, Implementations                      │  │
│  │  AutoMapper Profiles, Utilities, Constants        │  │
│  │  Job System, Background Services                  │  │
│  └───────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────┘
                           ↓
┌─────────────────────────────────────────────────────────┐
│                 Data Access Layer                        │
│  ┌───────────────────────────────────────────────────┐  │
│  │  DbContext, FluentMigrations                      │  │
│  │  IMssqlRepository<T> (CRUD operations)            │  │
│  │  Database configurations                          │  │
│  └───────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────┘
                           ↓
┌─────────────────────────────────────────────────────────┐
│                    Data Layer                            │
│  ┌───────────────────────────────────────────────────┐  │
│  │  Entities (POCO classes)                          │  │
│  │  Enums, Value Objects                             │  │
│  │  BaseEntity (Audit fields, Soft delete)           │  │
│  └───────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────┘
                           ↓
┌─────────────────────────────────────────────────────────┐
│                    DTO Layer                             │
│  ┌───────────────────────────────────────────────────┐  │
│  │  Data Transfer Objects                            │  │
│  │  Create, Update, List, Filter, Summary DTOs      │  │
│  └───────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────┘
```

### Dependency Flow

```
API → Services → Mssql (DbContext) → Data (Entities)
                   ↓
API → Dto ← Services (AutoMapper)
```

### Proje Yapısı

```
YourProject/
├── src/
│   ├── Libraries/
│   │   ├── Data/YourProject.Data.Mssql/          # Entities & Enums
│   │   ├── Dto/YourProject.Dto.Mssql/            # Data Transfer Objects
│   │   ├── Mssql/YourProject.Mssql/              # DbContext & Migrations
│   │   └── Mssql.Services/YourProject.Mssql.Services/  # Business Logic
│   └── Presentation/
│       └── Api/YourProject.Api/                   # API Controllers & Config
├── docs/                                          # Documentation
├── tests/                                         # Unit & Integration Tests
├── Directory.Packages.props                       # Central Package Management
├── docker-compose.yml                             # Docker configuration
└── YourProject.sln                                # Solution file
```

---

## 🚀 Kurulum

### Gereksinimler

- ✅ **.NET SDK 8.0** veya üzeri
- ✅ **SQL Server 2022** (veya Docker container)
- ✅ **Redis** (opsiyonel - distributed cache için)
- ✅ **Visual Studio 2022 / Rider / VS Code**
- ✅ **Git**

### 1. Repository'yi Klonlayın

```bash
git clone https://github.com/yourusername/yourproject.git
cd yourproject
```

### 2. Environment Variables Ayarlayın

Windows (PowerShell):
```powershell
$env:DATABASE_CONNECTION_STRING = "Server=localhost;Database=YourProjectDb;User Id=sa;Password=YourStrong!Pass;TrustServerCertificate=True;"
$env:JWT_SECRET_KEY = "YourSuperSecretKeyWithAtLeast32Characters!"
$env:REDIS_CONNECTION_STRING = "localhost:6379"  # Opsiyonel
$env:AZURE_STORAGE_CONNECTION_STRING = "Your_Azure_Connection_String"  # Opsiyonel
```

Linux/macOS:
```bash
export DATABASE_CONNECTION_STRING="Server=localhost;Database=YourProjectDb;User Id=sa;Password=YourStrong!Pass;TrustServerCertificate=True;"
export JWT_SECRET_KEY="YourSuperSecretKeyWithAtLeast32Characters!"
export REDIS_CONNECTION_STRING="localhost:6379"  # Opsiyonel
export AZURE_STORAGE_CONNECTION_STRING="Your_Azure_Connection_String"  # Opsiyonel
```

### 3. Docker ile SQL Server ve Redis Başlatın (Opsiyonel)

```bash
docker-compose up -d
```

`docker-compose.yml`:
```yaml
version: '3.8'

services:
  mssql:
    image: mcr.microsoft.com/mssql/server:2022-latest
    environment:
      - ACCEPT_EULA=Y
      - SA_PASSWORD=YourStrong!Passw0rd
      - MSSQL_PID=Express
    ports:
      - "1433:1433"
    volumes:
      - mssql-data:/var/opt/mssql

  redis:
    image: redis:7-alpine
    ports:
      - "6379:6379"
    volumes:
      - redis-data:/data

volumes:
  mssql-data:
  redis-data:
```

### 4. Projeyi Restore Edin

```bash
dotnet restore
```

### 5. Migration'ları Çalıştırın

Migration'lar uygulama başlarken otomatik çalışır (`app.AddUpMigrate()`).

İsteğe bağlı manuel çalıştırma:
```bash
cd src/Presentation/Api/YourProject.Api
dotnet run -- --migrate
```

### 6. Seed Data Oluşturun

`appsettings.json` içinde:
```json
{
  "SeedData": {
    "Enabled": true
  }
}
```

Uygulama başladığında otomatik olarak seed data oluşturulur.

### 7. Uygulamayı Başlatın

```bash
cd src/Presentation/Api/YourProject.Api
dotnet run
```

veya

```bash
dotnet watch run  # Hot reload için
```

### 8. Swagger UI'ı Açın

Tarayıcınızda açın: **https://localhost:5001** veya **http://localhost:5000**

---

## 💻 Kullanım

### API Authentication

#### 1. Login (Token Alma)

```http
POST /api/Auth/login
Content-Type: application/json

{
  "email": "admin@gmail.com",
  "password": "Super123!"
}
```

Response:
```json
{
  "success": true,
  "data": {
    "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
    "refreshToken": "dGVzdC1yZWZyZXNoLXRva2VuLTEyMzQ1Njc4OTA=",
    "accessTokenExpiration": "2025-01-19T14:30:00Z",
    "refreshTokenExpiration": "2025-01-26T13:30:00Z"
  }
}
```

#### 2. Token ile API Kullanımı

```http
GET /api/Users/profile
Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
```

#### 3. Refresh Token

```http
POST /api/Auth/refresh-token
Content-Type: application/json

{
  "refreshToken": "dGVzdC1yZWZyZXNoLXRva2VuLTEyMzQ1Njc4OTA="
}
```

### API Endpoints (Örnek)

| Endpoint | Method | Auth | Açıklama |
|----------|--------|------|----------|
| `/api/Auth/login` | POST | ❌ | Kullanıcı girişi |
| `/api/Auth/register` | POST | ❌ | Kullanıcı kaydı |
| `/api/Auth/refresh-token` | POST | ❌ | Token yenileme |
| `/api/Users/profile` | GET | ✅ | Profil bilgisi |
| `/api/Users/profile` | PUT | ✅ | Profil güncelleme |
| `/api/Admin/users` | GET | 👑 Admin | Tüm kullanıcılar |
| `/api/Products` | GET | ❌ | Ürün listesi |
| `/api/Products/{id}` | GET | ❌ | Ürün detayı |
| `/api/Orders` | GET | ✅ | Kullanıcının siparişleri |
| `/api/Orders` | POST | ✅ | Sipariş oluştur |

### API Versioning

```http
GET /api/v1/Products
GET /api/v2/Products
X-Api-Version: 1.0
```

### Çoklu Dil Desteği

```http
GET /api/Products
X-Language: tr  # tr, en, de, fr, ar
```

### SignalR Hub Kullanımı (JavaScript)

```javascript
// SignalR bağlantısı
const connection = new signalR.HubConnectionBuilder()
    .withUrl("/hubs/notification", {
        accessTokenFactory: () => localStorage.getItem("accessToken")
    })
    .build();

// Bağlantıyı başlat
await connection.start();

// Bildirim dinle
connection.on("ReceiveNotification", (notification) => {
    console.log("New notification:", notification);
});

// Gruba katıl
await connection.invoke("JoinGroup", "notifications");
```

---

## 📚 API Dokümantasyonu

### Swagger UI

Uygulama çalıştığında Swagger UI otomatik olarak açılır:

- **Local**: http://localhost:5000 veya https://localhost:5001
- **Production**: https://yourapp.com/swagger (restricted)

### API Response Format

#### Success Response

```json
{
  "success": true,
  "message": "İşlem başarılı",
  "data": {
    "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "name": "Product Name"
  },
  "timestamp": "2025-01-19T13:30:00Z"
}
```

#### Error Response

```json
{
  "success": false,
  "message": "Validation hatası",
  "errors": [
    {
      "field": "Email",
      "message": "Email adresi geçersiz"
    }
  ],
  "timestamp": "2025-01-19T13:30:00Z"
}
```

#### Paginated Response

```json
{
  "success": true,
  "data": {
    "items": [...],
    "pageNumber": 1,
    "pageSize": 10,
    "totalPages": 5,
    "totalCount": 50,
    "hasPreviousPage": false,
    "hasNextPage": true
  }
}
```

### HTTP Status Codes

| Kod | Açıklama |
|-----|----------|
| 200 | OK - İşlem başarılı |
| 201 | Created - Kayıt oluşturuldu |
| 204 | No Content - Başarılı ama dönen veri yok |
| 400 | Bad Request - Validasyon hatası |
| 401 | Unauthorized - Kimlik doğrulama gerekli |
| 403 | Forbidden - Yetki yok |
| 404 | Not Found - Kayıt bulunamadı |
| 409 | Conflict - Kayıt zaten var |
| 429 | Too Many Requests - Rate limit aşıldı |
| 500 | Internal Server Error - Sunucu hatası |

---

## 🗄️ Database

### Database Schema

Database schema'sı FluentMigrator ile yönetilir. Migration'lar `src/Libraries/Mssql/YourProject.Mssql/Migrations/` klasöründe bulunur.

### Temel Tablolar

| Tablo | Açıklama |
|-------|----------|
| `AspNetUsers` | Kullanıcı bilgileri (Identity) |
| `AspNetRoles` | Roller (Admin, User, vb.) |
| `AspNetUserRoles` | Kullanıcı-Rol ilişkisi |
| `Languages` | Dil tanımlamaları (tr-TR, en-US) |
| `LocaleStringResources` | Çeviri metinleri |
| `LocalizedProperties` | Entity'lere özel çeviriler |
| `UserActivityLogs` | Kullanıcı aktivite logları |
| `Logs` | Serilog sistem logları |
| `Parameters` | Sistem parametreleri |
| `{YourEntities}` | Projeye özel entity tabloları |

### Migration Oluşturma

1. Yeni migration class'ı oluşturun:

```csharp
[MaggsoftMigration("2025/01/19 14:30:00", "Add User Avatar Column", "v01")]
public sealed class AddUserAvatarColumn : Migration
{
    public override void Up()
    {
        if (!Schema.Table("AspNetUsers").Column("Avatar").Exists())
        {
            Alter.Table("AspNetUsers")
                .AddColumn("Avatar")
                .AsString(500)
                .Nullable();
        }
    }

    public override void Down()
    {
        // Rollback logic (opsiyonel)
    }
}
```

2. Uygulama başladığında otomatik çalışacak.

### Database Backup

```bash
# SQL Server Backup
sqlcmd -S localhost -U sa -P YourStrong!Pass -Q "BACKUP DATABASE [YourProjectDb] TO DISK = N'/var/opt/mssql/backup/YourProjectDb.bak' WITH NOFORMAT, NOINIT, NAME = 'Full Backup', SKIP, NOREWIND, NOUNLOAD, STATS = 10"
```

---

## ✨ Özellikler

### 🔐 Authentication & Authorization

- JWT Bearer Token authentication
- Role-based authorization (Admin, User, Manager, vb.)
- Refresh token mechanism
- Token expiration management
- Password policy enforcement
- Account lockout after failed attempts

### 🌍 Çoklu Dil Desteği (Localization)

- Database-driven localization
- `Language`, `LocaleStringResource`, `LocalizedProperty` entities
- HTTP Header: `X-Language`
- Fallback to default language (tr-TR)
- Localized validation messages
- Localized API responses

### 📝 Logging & Monitoring

- Structured logging (Serilog)
- Console logging (development)
- SQL Server logging (production)
- Request/Response logging
- User activity logging
- Error tracking
- Performance metrics

### 📊 Background Jobs (Quartz.NET)

- Scheduled jobs (cron expressions)
- Event-driven jobs
- Retry mechanism
- Job persistence
- Monitoring dashboard (optional)

**Örnek Jobs:**
- Cleanup old logs (weekly)
- Send scheduled emails
- Process queued tasks
- Data synchronization

### ⚡ Real-time Communication (SignalR)

- WebSocket support
- JWT authentication
- Connection management
- Group messaging
- Broadcast notifications

### 🚦 Rate Limiting

- IP-based rate limiting
- Endpoint-specific limits
- Whitelist support
- Customizable rules
- HTTP 429 response

**Örnek Limitler:**
- Login: 5 istek/dakika
- Register: 3 istek/5 dakika
- API calls: 100 istek/dakika

### 🔒 Security Features

- HTTPS enforcement (production)
- Security headers (X-Frame-Options, CSP, HSTS, vb.)
- CORS policy
- IP filtering
- Environment variable configuration
- SQL injection protection (EF Core)
- XSS protection

### 💾 Caching

- Distributed cache (Redis)
- In-memory cache
- Cache-aside pattern
- TTL (Time-To-Live) management
- Cache invalidation

### 📤 File Upload & Storage

- Azure Blob Storage support
- Local file storage option
- File type validation
- File size validation
- Image optimization (optional)
- CDN integration (optional)

### 📱 SMS & Email Notifications

- SMS provider abstraction (Netgsm, Twilio, vb.)
- Email service (SMTP, SendGrid, vb.)
- Template-based messages
- Retry mechanism
- Delivery tracking

### 🗑️ Soft Delete

- Tüm entity'ler soft delete destekler
- `IsActive`, `IsDeleted` flags
- Filter'larda otomatik excludelenir
- Admin panelinde restore özelliği

### 📜 Audit Trail

- `CreatedDate`, `CreatorUserId`
- `UpdatedDate`, `UpdatedByUserId`, `UpdatedIP`
- Tüm CRUD işlemlerinde otomatik doldurulur
- `BaseService` üzerinden `CurrentUserId` ve `RemoteIp`

### 📄 API Versioning

- URL-based versioning (`/api/v1/products`)
- Header-based versioning (`X-Api-Version: 1.0`)
- Media type versioning
- Deprecated version warning

---

## 👨‍💻 Geliştirme

### Geliştirme Ortamı Kurulumu

1. **Visual Studio 2022 / Rider / VS Code** yükleyin
2. **.NET SDK 8.0** yükleyin
3. **SQL Server** veya Docker ile MSSQL container başlatın
4. **Git** yükleyin
5. Repository'yi klonlayın
6. Environment variables ayarlayın
7. `dotnet restore` çalıştırın
8. `dotnet run` ile uygulamayı başlatın

### Yeni Feature Ekleme

#### 1. Entity Oluşturma

`src/Libraries/Data/YourProject.Data.Mssql/Product.cs`:

```csharp
/// <summary>
/// Ürün entity'si
/// </summary>
public class Product : BaseEntity
{
    public string Name { get; set; }
    public string Description { get; set; }
    public decimal Price { get; set; }
    public int Stock { get; set; }
}
```

#### 2. DTO Oluşturma

`src/Libraries/Dto/YourProject.Dto.Mssql/Product/CreateProductDto.cs`:

```csharp
/// <summary>
/// Ürün oluşturma DTO'su
/// </summary>
public class CreateProductDto
{
    public string Name { get; set; }
    public string Description { get; set; }
    public decimal Price { get; set; }
    public int Stock { get; set; }
}
```

#### 3. Migration Oluşturma

`src/Libraries/Mssql/YourProject.Mssql/Migrations/003_CreateProductTable.cs`:

```csharp
[MaggsoftMigration("2025/01/19 15:00:00", "Create Product Table", "v01")]
public sealed class CreateProductTable : Migration
{
    public override void Up()
    {
        if (!Schema.Table("Products").Exists())
        {
            Create.Table("Products")
                .WithColumn("Id").AsGuid().PrimaryKey()
                .WithColumn("Name").AsString(200).NotNullable()
                .WithColumn("Description").AsString().Nullable()
                .WithColumn("Price").AsDecimal(18, 2).NotNullable()
                .WithColumn("Stock").AsInt32().NotNullable()
                .WithColumn("IsActive").AsBoolean().NotNullable().WithDefaultValue(true)
                .WithColumn("IsDeleted").AsBoolean().NotNullable().WithDefaultValue(false)
                .WithColumn("CreatedDate").AsDateTime().NotNullable()
                .WithColumn("CreatorUserId").AsGuid().Nullable()
                .WithColumn("UpdatedDate").AsDateTime().Nullable()
                .WithColumn("UpdatedByUserId").AsGuid().Nullable()
                .WithColumn("UpdatedIP").AsString(45).Nullable();
        }
    }

    public override void Down() { }
}
```

#### 4. Service Oluşturma

`src/Libraries/Mssql.Services/YourProject.Mssql.Services/Interfaces/IProductService.cs`:

```csharp
public interface IProductService : IService
{
    Task<PagedList<ProductDto>> GetProductsAsync(int pageNumber, int pageSize);
    Task<ProductDto?> GetProductByIdAsync(Guid id);
    Task<Result<ProductDto>> CreateProductAsync(CreateProductDto dto);
    Task<Result<ProductDto>> UpdateProductAsync(Guid id, UpdateProductDto dto);
    Task<Result<bool>> DeleteProductAsync(Guid id);
}
```

`src/Libraries/Mssql.Services/YourProject.Mssql.Services/Services/ProductService.cs`:

```csharp
public class ProductService : BaseService, IService, IProductService
{
    private readonly IMssqlRepository<Product> _productRepository;
    private readonly IMapper _mapper;

    public ProductService(
        IMssqlRepository<Product> productRepository,
        IMapper mapper)
    {
        _productRepository = productRepository;
        _mapper = mapper;
    }

    public async Task<PagedList<ProductDto>> GetProductsAsync(int pageNumber, int pageSize)
    {
        var query = _productRepository.GetQueryable();
        return await query
            .Where(p => p.IsActive && !p.IsDeleted)
            .OrderBy(p => p.Name)
            .ProjectTo<ProductDto>(_mapper.ConfigurationProvider)
            .ToPagedListAsync(pageNumber - 1, pageSize, new List<Filter>());
    }

    public async Task<Result<ProductDto>> CreateProductAsync(CreateProductDto dto)
    {
        var product = _mapper.Map<Product>(dto);
        product.CreatedDate = DateTime.UtcNow;
        product.CreatorUserId = CurrentUserId;

        await _productRepository.InsertAsync(product);
        await _productRepository.SaveChangesAsync();

        return Result<ProductDto>.Success(_mapper.Map<ProductDto>(product));
    }

    // Diğer metodlar...
}
```

#### 5. AutoMapper Profil Güncelleme

`src/Libraries/Mssql.Services/YourProject.Mssql.Services/Mapping/MappingProfile.cs`:

```csharp
public class MappingProfile : Profile
{
    public MappingProfile()
    {
        // Product mappings
        CreateMap<Product, ProductDto>();
        CreateMap<CreateProductDto, Product>();
        CreateMap<UpdateProductDto, Product>();
    }
}
```

#### 6. Validator Oluşturma

`src/Presentation/Api/YourProject.Api/Validators/CreateProductDtoValidator.cs`:

```csharp
public class CreateProductDtoValidator : AbstractValidator<CreateProductDto>
{
    private readonly ILocalizationService _localizationService;

    public CreateProductDtoValidator(ILocalizationService localizationService)
    {
        _localizationService = localizationService;

        RuleFor(x => x.Name)
            .NotEmpty().WithMessage(_localizationService.GetLocalizedString("Validation.ProductNameRequired"))
            .MaximumLength(200);

        RuleFor(x => x.Price)
            .GreaterThan(0).WithMessage(_localizationService.GetLocalizedString("Validation.PricePositive"));

        RuleFor(x => x.Stock)
            .GreaterThanOrEqualTo(0).WithMessage(_localizationService.GetLocalizedString("Validation.StockNonNegative"));
    }
}
```

#### 7. Controller Oluşturma

`src/Presentation/Api/YourProject.Api/Controllers/ProductsController.cs`:

```csharp
[ApiController]
[Route("api/v{version:apiVersion}/[controller]")]
[ApiVersion("1.0")]
public class ProductsController : ControllerBase
{
    private readonly IProductService _productService;

    public ProductsController(IProductService productService)
    {
        _productService = productService;
    }

    /// <summary>
    /// Ürün listesini getirir (sayfalı)
    /// </summary>
    [HttpGet]
    public async Task<IActionResult> GetProducts([FromQuery] int pageNumber = 1, [FromQuery] int pageSize = 10)
    {
        var products = await _productService.GetProductsAsync(pageNumber, pageSize);
        return Ok(products);
    }

    /// <summary>
    /// Belirli bir ürünü getirir
    /// </summary>
    [HttpGet("{id}")]
    public async Task<IActionResult> GetProduct(Guid id)
    {
        var product = await _productService.GetProductByIdAsync(id);
        return product == null ? NotFound() : Ok(product);
    }

    /// <summary>
    /// Yeni ürün oluşturur
    /// </summary>
    [HttpPost]
    [Authorize(Roles = "Admin")]
    public async Task<IActionResult> CreateProduct(CreateProductDto dto)
    {
        var result = await _productService.CreateProductAsync(dto);
        return result.IsSuccess
            ? CreatedAtAction(nameof(GetProduct), new { id = result.Data.Id }, result.Data)
            : BadRequest(result);
    }

    /// <summary>
    /// Ürünü günceller
    /// </summary>
    [HttpPut("{id}")]
    [Authorize(Roles = "Admin")]
    public async Task<IActionResult> UpdateProduct(Guid id, UpdateProductDto dto)
    {
        var result = await _productService.UpdateProductAsync(id, dto);
        return result.IsSuccess ? Ok(result.Data) : BadRequest(result);
    }

    /// <summary>
    /// Ürünü siler (soft delete)
    /// </summary>
    [HttpDelete("{id}")]
    [Authorize(Roles = "Admin")]
    public async Task<IActionResult> DeleteProduct(Guid id)
    {
        var result = await _productService.DeleteProductAsync(id);
        return result.IsSuccess ? NoContent() : BadRequest(result);
    }
}
```

### Kod Standartları

- **Naming Convention**: PascalCase (classes, methods), camelCase (variables)
- **File Organization**: Her class ayrı dosyada
- **Comments**: XML summary açıklamaları (public members için)
- **Validation**: FluentValidation kullanılır
- **Error Handling**: Global exception handler
- **Async/Await**: Tüm I/O işlemler async
- **SOLID Principles**: Takip edilir
- **DRY Principle**: Code duplication önlenir

### Git Workflow

1. **Feature branch oluştur**: `git checkout -b feature/product-management`
2. **Değişiklikleri commit et**: `git commit -m "feat: Add product management"`
3. **Push et**: `git push origin feature/product-management`
4. **Pull request oluştur**: GitHub/GitLab/Bitbucket
5. **Code review**: Takım arkadaşları review eder
6. **Merge**: Main/develop branch'e merge edilir

### Unit Testing

```csharp
public class ProductServiceTests
{
    private readonly Mock<IMssqlRepository<Product>> _mockRepository;
    private readonly Mock<IMapper> _mockMapper;
    private readonly ProductService _service;

    public ProductServiceTests()
    {
        _mockRepository = new Mock<IMssqlRepository<Product>>();
        _mockMapper = new Mock<IMapper>();
        _service = new ProductService(_mockRepository.Object, _mockMapper.Object);
    }

    [Fact]
    public async Task CreateProductAsync_ValidDto_ReturnsSuccess()
    {
        // Arrange
        var dto = new CreateProductDto { Name = "Test Product", Price = 100 };
        var product = new Product { Id = Guid.NewGuid(), Name = "Test Product" };
        _mockMapper.Setup(m => m.Map<Product>(dto)).Returns(product);
        _mockMapper.Setup(m => m.Map<ProductDto>(product)).Returns(new ProductDto());
        _mockRepository.Setup(r => r.InsertAsync(It.IsAny<Product>())).Returns(Task.CompletedTask);
        _mockRepository.Setup(r => r.SaveChangesAsync()).Returns(Task.CompletedTask);

        // Act
        var result = await _service.CreateProductAsync(dto);

        // Assert
        Assert.True(result.IsSuccess);
    }
}
```

---

## 🚀 Deployment

### Azure App Service

#### 1. Azure App Service Oluşturun

```bash
az appservice plan create --name YourProject-AppServicePlan --resource-group YourProjectRG --sku B1
az webapp create --name YourProjectAPI --resource-group YourProjectRG --plan YourProject-AppServicePlan --runtime "DOTNETCORE|8.0"
```

#### 2. Environment Variables Ayarlayın

Azure Portal → App Service → Configuration → Application Settings:

```
DATABASE_CONNECTION_STRING = Server=tcp:yourserver.database.windows.net,1433;Database=YourProjectDb;User ID=yourusername;Password=yourpassword;Encrypt=True;TrustServerCertificate=False;Connection Timeout=30;
JWT_SECRET_KEY = YourSuperSecretKeyWithAtLeast32Characters!
REDIS_CONNECTION_STRING = yourredis.redis.cache.windows.net:6380,password=yourrediskey,ssl=True,abortConnect=False
AZURE_STORAGE_CONNECTION_STRING = DefaultEndpointsProtocol=https;AccountName=youraccount;AccountKey=yourkey;EndpointSuffix=core.windows.net
```

#### 3. Deploy Edin

```bash
# Publish
dotnet publish src/Presentation/Api/YourProject.Api/YourProject.Api.csproj -c Release -o ./publish

# ZIP oluştur
cd publish
zip -r ../YourProject.zip *
cd ..

# Azure'a deploy et
az webapp deployment source config-zip --resource-group YourProjectRG --name YourProjectAPI --src YourProject.zip
```

#### 4. Continuous Deployment (GitHub Actions)

`.github/workflows/deploy.yml`:

```yaml
name: Deploy to Azure

on:
  push:
    branches: [ main ]

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    
    steps:
    - uses: actions/checkout@v2
    
    - name: Setup .NET
      uses: actions/setup-dotnet@v1
      with:
        dotnet-version: '8.0.x'
    
    - name: Restore dependencies
      run: dotnet restore
    
    - name: Build
      run: dotnet build --configuration Release --no-restore
    
    - name: Publish
      run: dotnet publish src/Presentation/Api/YourProject.Api/YourProject.Api.csproj -c Release -o ./publish
    
    - name: Deploy to Azure Web App
      uses: azure/webapps-deploy@v2
      with:
        app-name: 'YourProjectAPI'
        publish-profile: ${{ secrets.AZURE_WEBAPP_PUBLISH_PROFILE }}
        package: ./publish
```

### Docker Deployment

#### 1. Dockerfile Oluşturun

```dockerfile
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ["src/Presentation/Api/YourProject.Api/YourProject.Api.csproj", "src/Presentation/Api/YourProject.Api/"]
# ... diğer projeler
RUN dotnet restore "src/Presentation/Api/YourProject.Api/YourProject.Api.csproj"
COPY . .
WORKDIR "/src/src/Presentation/Api/YourProject.Api"
RUN dotnet build "YourProject.Api.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "YourProject.Api.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "YourProject.Api.dll"]
```

#### 2. Docker Image Oluşturun

```bash
docker build -t yourproject-api:latest .
```

#### 3. Docker Container Çalıştırın

```bash
docker run -d -p 8080:80 \
  -e DATABASE_CONNECTION_STRING="Server=host.docker.internal;Database=YourProjectDb;..." \
  -e JWT_SECRET_KEY="YourSecretKey" \
  --name yourproject-api \
  yourproject-api:latest
```

### Nginx Reverse Proxy (Linux)

`/etc/nginx/sites-available/yourproject`:

```nginx
server {
    listen 80;
    server_name yourapp.com www.yourapp.com;
    
    location / {
        return 301 https://$server_name$request_uri;
    }
}

server {
    listen 443 ssl http2;
    server_name yourapp.com www.yourapp.com;
    
    ssl_certificate /etc/letsencrypt/live/yourapp.com/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/yourapp.com/privkey.pem;
    
    location / {
        proxy_pass http://localhost:5000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection keep-alive;
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
    
    # SignalR WebSocket support
    location /hubs/ {
        proxy_pass http://localhost:5000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
}
```

---

## 📄 Lisans

Bu proje [Lisans Türü] altında lisanslanmıştır. Detaylar için [LICENSE](LICENSE) dosyasına bakın.

---

## 👥 Katkıda Bulunanlar

- **[İsim]** - Proje Lideri
- **[İsim]** - Backend Developer
- **[İsim]** - DevOps Engineer

---

## 📞 İletişim

- **Email**: info@yourproject.com
- **Website**: https://yourproject.com
- **Support**: support@yourproject.com

---

## 📝 Changelog

### [1.0.0] - 2025-01-19

#### Added
- Initial release
- Authentication & Authorization (JWT)
- Çoklu dil desteği
- Background jobs (Quartz.NET)
- Real-time notifications (SignalR)
- Rate limiting
- API versioning
- Comprehensive logging
- Soft delete mechanism
- Audit trail

#### Changed
- N/A

#### Fixed
- N/A

---

## 🙏 Teşekkürler

- [Maggsoft Framework](https://maggsoft.com)
- [Microsoft .NET Team](https://dotnet.microsoft.com/)
- [Serilog](https://serilog.net/)
- [AutoMapper](https://automapper.org/)
- [FluentValidation](https://fluentvalidation.net/)
- [Quartz.NET](https://www.quartz-scheduler.net/)

---

<div align="center">

**🚀 {PROJE_ADI} - Powered by Maggsoft Framework 🚀**

Made with ❤️ by {TEAM_NAME}

</div>


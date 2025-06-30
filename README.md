# SpringBucks Redis 緩存示例 ☕

[![Java](https://img.shields.io/badge/Java-21-orange.svg)](https://www.oracle.com/java/)
[![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.4.5-brightgreen.svg)](https://spring.io/projects/spring-boot)
[![Redis](https://img.shields.io/badge/Redis-Cache-red.svg)](https://redis.io/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

## 專案介紹

SpringBucks Redis 緩存示例是一個基於 Spring Boot 的咖啡訂單管理系統，主要目的是展示如何在企業級應用中整合 Redis 作為緩存層，提升應用程式的效能和響應速度。

本專案透過簡潔的咖啡店訂單場景，演示了：
- **Redis 緩存策略**：實現資料庫查詢結果的智慧快取
- **快取穿透處理**：有效減少資料庫負載
- **Spring Data Redis 整合**：展示現代 Spring 應用的最佳實踐
- **多層架構設計**：清晰的分層架構便於維護和擴展

> 💡 **為什麼選擇此專案？**
> - 🚀 **高效能**：透過 Redis 緩存大幅提升查詢速度
> - 📚 **學習價值**：完整展示 Spring Boot + Redis 整合最佳實踐  
> - 🔧 **易於理解**：清晰的程式碼結構和詳細註解
> - 🏗️ **企業級架構**：採用業界標準的分層設計模式

### 🎯 專案特色

- **智慧快取機制**：自動判斷快取命中，優化資料庫存取
- **完整的咖啡店業務模型**：包含咖啡品項、訂單管理等完整功能
- **Lettuce 連線管理**：採用非阻塞 Redis 客戶端，支援連線池優化
- **JPA/Hibernate 整合**：完整的 ORM 映射和資料持久化
- **H2 記憶體資料庫**：零配置啟動，適合開發和測試環境

## 技術棧

### 核心框架
- **Spring Boot 3.4.5** - 企業級應用開發框架，提供自動配置和依賴注入
- **Spring Data JPA** - 簡化資料存取層開發，支援 JPA 規範
- **Spring Data Redis** - Redis 整合框架，提供 RedisTemplate 和 Repository 支援
- **Hibernate 6.6.13** - 強大的 ORM 框架，處理物件關係映射

### 快取與資料庫
- **Redis** - 高效能記憶體資料庫，作為快取層使用
- **Lettuce** - 非阻塞 Redis Java 客戶端，支援連線池和高併發
- **H2 Database** - 輕量級記憶體資料庫，適合開發和測試環境
- **Apache Commons Pool2** - 連線池管理，優化 Redis 連線效能

### 開發工具與輔助  
- **Lombok** - 減少重複程式碼，自動生成 getter/setter 等方法
- **Joda Money** - 專業的金錢處理函式庫，確保金額計算精確度
- **Maven** - 專案建構和依賴管理工具
- **SLF4J + Logback** - 結構化日誌記錄，便於問題追蹤和除錯

## 專案結構

```
redis-demo/
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   └── tw/fengqing/spring/springbucks/
│   │   │       ├── SpringBucksApplication.java    # 主程式進入點
│   │   │       ├── config/
│   │   │       │   └── RedisConfig.java           # Redis 配置類
│   │   │       ├── model/                         # 資料模型層
│   │   │       │   ├── BaseEntity.java           # 基礎實體類別
│   │   │       │   ├── Coffee.java               # 咖啡實體
│   │   │       │   ├── CoffeeOrder.java          # 訂單實體
│   │   │       │   ├── MoneyConverter.java       # 金錢轉換器
│   │   │       │   └── OrderState.java           # 訂單狀態列舉
│   │   │       ├── repository/                    # 資料存取層
│   │   │       │   ├── CoffeeRepository.java     # 咖啡資料倉庫
│   │   │       │   └── CoffeeOrderRepository.java # 訂單資料倉庫
│   │   │       └── service/                       # 業務邏輯層  
│   │   │           ├── CoffeeService.java         # 咖啡服務（含快取邏輯）
│   │   │           └── CoffeeOrderService.java    # 訂單服務
│   │   └── resources/
│   │       ├── application.properties             # 應用程式配置
│   │       └── schema.sql                         # 資料庫結構定義
│   └── test/
│       └── java/                                  # 測試程式碼
├── target/                                        # 編譯輸出目錄
├── pom.xml                                        # Maven 專案配置檔
├── LICENSE                                        # 授權條款
└── README.md                                      # 專案說明文件
```

## 快速開始

### 前置需求
- **Java 21** 或更高版本
- **Maven 3.6+** 建構工具
- **Redis Server** （本機安裝或 Docker 容器）
- **IDE**：建議使用 IntelliJ IDEA 或 Eclipse

### 安裝與執行

1. **克隆此倉庫：**
```bash
git clone https://github.com/SpringMicroservicesCourse/redis-demo.git
```

2. **進入專案目錄：**
```bash
cd redis-demo
```

3. **啟動 Redis 服務**（如果尚未啟動）：
```bash
# 使用 Docker（推薦）
docker run -d --name redis -p 6379:6379 redis:alpine

# 或使用本機安裝的 Redis
redis-server
```

4. **編譯專案：**
```bash
mvn clean compile
```

5. **執行應用程式：**
```bash
mvn spring-boot:run
```

### 🎉 運行結果
程式啟動後會自動執行示例，您將看到類似以下的輸出：
```
2025-06-30T14:53:34.042  INFO --- CoffeeService : Coffee Found: Optional[Coffee(...name=mocha, price=TWD 150.00)]
2025-06-30T14:53:34.043  INFO --- CoffeeService : Put coffee mocha to Redis.
2025-06-30T14:53:34.051  INFO --- CoffeeService : Get coffee mocha from Redis.
```

**📊 效能對比：**
- **首次查詢**：從資料庫讀取，回應時間較長
- **後續查詢**：從 Redis 快取讀取，回應時間大幅縮短

## 進階說明

### 環境變數
```properties
# Redis 連線設定（選用）
REDIS_HOST=localhost
REDIS_PORT=6379
REDIS_PASSWORD=your-password

# 應用程式設定（選用）  
LOG_LEVEL=INFO
SPRING_PROFILES_ACTIVE=development
```

### 設定檔說明
```properties
# application.properties 主要設定

# JPA/Hibernate 配置
spring.jpa.hibernate.ddl-auto=none                    # 不自動更新資料庫結構
spring.jpa.properties.hibernate.show_sql=true         # 顯示 SQL 語句（開發環境）
spring.jpa.properties.hibernate.format_sql=true       # 格式化 SQL 輸出

# 管理端點暴露（監控用）
management.endpoints.web.exposure.include=*           # 開放所有監控端點

# Redis 設定
redis.host=redis://localhost:6379                     # Redis 伺服器位址
spring.redis.lettuce.pool.maxActive=5                 # 最大活躍連線數
spring.redis.lettuce.pool.maxIdle=5                   # 最大閒置連線數
```

### 核心程式碼說明

#### Redis 快取邏輯 (CoffeeService.java)
```java
/**
 * 智慧查詢咖啡資料，優先從 Redis 快取讀取
 * 快取策略：Cache-Aside Pattern
 */
public Optional<Coffee> findOneCoffee(String name) {
    HashOperations<String, String, Coffee> hashOperations = redisTemplate.opsForHash();
    
    // 1. 先檢查 Redis 快取
    if (redisTemplate.hasKey(CACHE) && hashOperations.hasKey(CACHE, name)) {
        log.info("Get coffee {} from Redis.", name);
        return Optional.of(hashOperations.get(CACHE, name));
    }
    
    // 2. 快取未命中，查詢資料庫
    Optional<Coffee> coffee = coffeeRepository.findOne(
        Example.of(Coffee.builder().name(name).build(), matcher));
    
    // 3. 將查詢結果存入快取
    if (coffee.isPresent()) {
        log.info("Put coffee {} to Redis.", name);
        hashOperations.put(CACHE, name, coffee.get());
        redisTemplate.expire(CACHE, 1, TimeUnit.MINUTES); // 設定過期時間
    }
    
    return coffee;
}
```

#### Redis 配置類 (RedisConfig.java)
```java
/**
 * Redis 連線和序列化配置
 * 使用 Lettuce 客戶端提供高效能非阻塞連線
 */
@Configuration
public class RedisConfig {
    
    @Bean
    public RedisTemplate<String, Coffee> redisTemplate(RedisConnectionFactory factory) {
        RedisTemplate<String, Coffee> template = new RedisTemplate<>();
        template.setConnectionFactory(factory);
        // 注意：生產環境建議設定自訂序列化器
        return template;
    }
    
    @Bean  
    public LettuceClientConfigurationBuilderCustomizer customizer() {
        // 設定讀寫分離：優先從主節點讀取
        return builder -> builder.readFrom(ReadFrom.MASTER_PREFERRED);
    }
}
```

## 參考資源

- [Spring Boot 官方文件](https://spring.io/projects/spring-boot)
- [Spring Data Redis 參考指南](https://docs.spring.io/spring-data/redis/docs/current/reference/html/)
- [Redis 官方文件](https://redis.io/documentation)
- [Lettuce Redis Client](https://lettuce.io/)

## 注意事項與最佳實踐

### ⚠️ 重要提醒

| 項目 | 說明 | 建議做法 |
|------|------|----------|
| **序列化設定** | 預設使用 JDK 序列化，效能不佳 | 生產環境建議使用 JSON 或 Protobuf |
| **快取過期策略** | 避免快取永久存在造成記憶體洩漏 | 設定合理的 TTL（本範例：1分鐘） |
| **連線池配置** | 預設連線池設定可能不適合高負載 | 根據應用需求調整 maxActive/maxIdle |
| **異常處理** | Redis 不可用時的降級策略 | 實作快取降級，確保服務可用性 |
| **資料一致性** | 快取與資料庫的資料同步問題 | 使用適當的快取更新策略 |

### 🔒 最佳實踐指南

- **快取鍵命名規範**：使用有意義的前綴，如 `springbucks-coffee:{name}`
- **快取預熱策略**：應用啟動時預載熱點資料至快取
- **監控與告警**：監控快取命中率、Redis 記憶體使用量等關鍵指標
- **序列化優化**：生產環境使用 GenericJackson2JsonRedisSerializer
- **連線池調優**：根據併發量和回應時間要求調整連線池參數

### 🚀 效能優化建議

```properties
# 生產環境 Redis 連線池優化設定
spring.redis.lettuce.pool.maxActive=20        # 最大連線數
spring.redis.lettuce.pool.maxIdle=10          # 最大閒置連線數  
spring.redis.lettuce.pool.minIdle=5           # 最小閒置連線數
spring.redis.lettuce.pool.maxWait=2000ms      # 最大等待時間
spring.redis.timeout=3000ms                   # 命令執行逾時時間
```

## 授權說明

本專案採用 MIT 授權條款，詳見 [LICENSE](LICENSE) 檔案。

## 關於我們

我們主要專注在敏捷專案管理、物聯網（IoT）應用開發和領域驅動設計（DDD）。喜歡把先進技術和實務經驗結合，打造好用又靈活的軟體解決方案。

## 聯繫我們

- **FB 粉絲頁**：[風清雲談 | Facebook](https://www.facebook.com/profile.php?id=61576838896062)
- **LinkedIn**：[linkedin.com/in/chu-kuo-lung](https://www.linkedin.com/in/chu-kuo-lung)
- **YouTube 頻道**：[雲談風清 - YouTube](https://www.youtube.com/channel/UCXDqLTdCMiCJ1j8xGRfwEig)
- **風清雲談 部落格**：[風清雲談](https://blog.fengqing.tw/)
- **電子郵件**：[fengqing.tw@gmail.com](mailto:fengqing.tw@gmail.com)

---

**📅 最後更新：2025-06-30**  
**👨‍💻 維護者：風清雲談團隊** 
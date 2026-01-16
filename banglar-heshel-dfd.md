# Banglar Heshel - Restaurant Management System
## Data Flow Diagrams (DFD)

---

## DFD Level 0 - Context Diagram

```mermaid
flowchart TB
    Customer([Customer/User])
    Admin([Admin])
    Manager([Manager])
    PaymentGW([Payment Gateway<br/>SSLCommerz])
    CloudStorage([Cloud Storage<br/>Cloudinary])
    
    System[Banglar Heshel<br/>Restaurant Management<br/>System]
    
    Customer -->|Registration Data,<br/>Login Credentials,<br/>Menu Browse Requests,<br/>Food Orders,<br/>Payment Info| System
    System -->|Menu Items,<br/>Order Confirmation,<br/>Token Number,<br/>Order Status| Customer
    
    Admin -->|Manager Registration,<br/>User Management Commands,<br/>Analytics Requests| System
    System -->|System Reports,<br/>User Lists,<br/>Analytics Data| Admin
    
    Manager -->|Menu Management,<br/>Stock Updates,<br/>Payment Verification| System
    System -->|Payment Details,<br/>Stock Levels,<br/>User Information| Manager
    
    System -->|Payment Request| PaymentGW
    PaymentGW -->|Transaction Status,<br/>Payment Confirmation| System
    
    System -->|Image Upload| CloudStorage
    CloudStorage -->|Image URLs| System
    
    style System fill:#DC0000,stroke:#8B0000,stroke-width:3px,color:#fff
    style Customer fill:#4CAF50,stroke:#2E7D32,stroke-width:2px,color:#fff
    style Admin fill:#FF9800,stroke:#E65100,stroke-width:2px,color:#fff
    style Manager fill:#2196F3,stroke:#0D47A1,stroke-width:2px,color:#fff
    style PaymentGW fill:#9C27B0,stroke:#4A148C,stroke-width:2px,color:#fff
    style CloudStorage fill:#00BCD4,stroke:#006064,stroke-width:2px,color:#fff
```

---

## DFD Level 1 - Main System Processes

```mermaid
flowchart TB
    Customer([Customer])
    Admin([Admin])
    Manager([Manager])
    PaymentGW([Payment Gateway])
    CloudStorage([Cloudinary])
    
    P1[1.0<br/>User Management]
    P2[2.0<br/>Menu Management]
    P3[3.0<br/>Order Management]
    P4[4.0<br/>Payment Processing]
    P5[5.0<br/>Stock Management]
    P6[6.0<br/>Authentication<br/>& Authorization]
    P7[7.0<br/>Analytics & Reporting]
    
    D1[(User Database)]
    D2[(Food Item Database)]
    D3[(Order/Payment Database)]
    D4[(Stock Database)]
    D5[(Employee Database)]
    D6[(Transaction Log)]
    
    Customer -->|Registration Info| P1
    P1 -->|User Credentials| Customer
    P1 -->|User Records| D1
    D1 -->|User Data| P1
    
    Customer -->|Login Credentials| P6
    P6 -->|Auth Token| Customer
    P6 -->|Verify User| D1
    D1 -->|User Info| P6
    
    Admin -->|Manager Details| P1
    P1 -->|Manager Records| D5
    D5 -->|Employee Data| P1
    P1 -->|Manager Created| Admin
    
    Customer -->|Browse Menu Request| P2
    Manager -->|Add/Update Menu| P2
    P2 -->|Food Items| D2
    D2 -->|Menu Data| P2
    P2 -->|Menu Display| Customer
    P2 -->|Menu Updated| Manager
    P2 -->|Image Upload| CloudStorage
    CloudStorage -->|Image URLs| P2
    
    Customer -->|Food Order| P3
    P3 -->|Order Details| D3
    D3 -->|Order History| P3
    P3 -->|Order Confirmation| Customer
    P3 -->|Stock Deduction Request| P5
    
    Customer -->|Payment Info| P4
    P4 -->|Payment Request| PaymentGW
    PaymentGW -->|Transaction Status| P4
    P4 -->|Payment Record| D3
    D3 -->|Payment History| P4
    P4 -->|Token Number| Customer
    
    Manager -->|Stock Update| P5
    P5 -->|Stock Records| D4
    D4 -->|Stock Levels| P5
    P5 -->|Transaction Log| D6
    P5 -->|Stock Status| Manager
    P3 -->|Deduct Stock| P5
    P5 -->|Stock Updated| P3
    
    Manager -->|Payment Check Request| P4
    P4 -->|Payment Details| Manager
    
    Admin -->|Analytics Request| P7
    Manager -->|Report Request| P7
    P7 -->|Fetch Orders| D3
    D3 -->|Order Data| P7
    P7 -->|Fetch Stock| D4
    D4 -->|Stock Data| P7
    P7 -->|Analytics Report| Admin
    P7 -->|Reports| Manager
    
    style P1 fill:#4CAF50,stroke:#2E7D32,stroke-width:2px,color:#fff
    style P2 fill:#FF9800,stroke:#E65100,stroke-width:2px,color:#fff
    style P3 fill:#2196F3,stroke:#0D47A1,stroke-width:2px,color:#fff
    style P4 fill:#9C27B0,stroke:#4A148C,stroke-width:2px,color:#fff
    style P5 fill:#F44336,stroke:#B71C1C,stroke-width:2px,color:#fff
    style P6 fill:#009688,stroke:#004D40,stroke-width:2px,color:#fff
    style P7 fill:#FFC107,stroke:#F57F17,stroke-width:2px,color:#333
```

---

## DFD Level 2 - Process 1.0: User Management

```mermaid
flowchart TB
    Customer([Customer])
    Admin([Admin])
    
    P11[1.1<br/>User Registration]
    P12[1.2<br/>Profile Management]
    P13[1.3<br/>Manager Registration]
    P14[1.4<br/>User Listing]
    P15[1.5<br/>User Control]
    
    D1[(User Database)]
    D5[(Employee Database)]
    
    Customer -->|Registration Form| P11
    P11 -->|Validate Data| P11
    P11 -->|Hash Password| P11
    P11 -->|Store User| D1
    P11 -->|Success Message| Customer
    
    Customer -->|Update Profile| P12
    P12 -->|Fetch Current Data| D1
    D1 -->|User Profile| P12
    P12 -->|Update Query| D1
    P12 -->|Updated Profile| Customer
    
    Admin -->|Manager Details| P13
    P13 -->|Create Employee Record| D5
    D5 -->|Manager Stored| P13
    P13 -->|Role Assignment| D1
    D1 -->|User Role Updated| P13
    P13 -->|Manager Created| Admin
    
    Admin -->|View Users Request| P14
    P14 -->|Query Users| D1
    D1 -->|User List| P14
    P14 -->|Display Users| Admin
    
    Admin -->|User Action| P15
    P15 -->|Update/Delete User| D1
    D1 -->|Action Confirmed| P15
    P15 -->|Action Result| Admin
    
    style P11 fill:#66BB6A,stroke:#2E7D32,stroke-width:2px,color:#fff
    style P12 fill:#66BB6A,stroke:#2E7D32,stroke-width:2px,color:#fff
    style P13 fill:#66BB6A,stroke:#2E7D32,stroke-width:2px,color:#fff
    style P14 fill:#66BB6A,stroke:#2E7D32,stroke-width:2px,color:#fff
    style P15 fill:#66BB6A,stroke:#2E7D32,stroke-width:2px,color:#fff
```

---

## DFD Level 2 - Process 2.0: Menu Management

```mermaid
flowchart TB
    Customer([Customer])
    Manager([Manager])
    CloudStorage([Cloudinary])
    
    P21[2.1<br/>Browse Menu]
    P22[2.2<br/>Search Food Items]
    P23[2.3<br/>Add Food Item]
    P24[2.4<br/>Update Food Item]
    P25[2.5<br/>Delete Food Item]
    P26[2.6<br/>Image Management]
    
    D2[(Food Item Database)]
    D4[(Stock Database)]
    
    Customer -->|Browse Request| P21
    P21 -->|Query Menu| D2
    D2 -->|Food Items| P21
    P21 -->|Display Menu| Customer
    
    Customer -->|Search Query| P22
    P22 -->|Search Database| D2
    D2 -->|Matching Items| P22
    P22 -->|Search Results| Customer
    
    Manager -->|New Food Details| P23
    P23 -->|Upload Images| P26
    P26 -->|Image Data| CloudStorage
    CloudStorage -->|Image URLs| P26
    P26 -->|Image URLs| P23
    P23 -->|Store Food Item| D2
    P23 -->|Create Stock Entry| D4
    D4 -->|Stock Initialized| P23
    P23 -->|Item Created| Manager
    
    Manager -->|Update Request| P24
    P24 -->|Fetch Item| D2
    D2 -->|Current Data| P24
    Manager -->|Updated Data| P24
    P24 -->|Update Images| P26
    P26 -->|New Images| CloudStorage
    CloudStorage -->|New URLs| P26
    P26 -->|Updated URLs| P24
    P24 -->|Update Database| D2
    P24 -->|Item Updated| Manager
    
    Manager -->|Delete Request| P25
    P25 -->|Fetch Item| D2
    D2 -->|Item Data| P25
    P25 -->|Delete Images| P26
    P26 -->|Delete from Cloud| CloudStorage
    P25 -->|Remove from DB| D2
    P25 -->|Deletion Confirmed| Manager
    
    style P21 fill:#FF9800,stroke:#E65100,stroke-width:2px,color:#fff
    style P22 fill:#FF9800,stroke:#E65100,stroke-width:2px,color:#fff
    style P23 fill:#FF9800,stroke:#E65100,stroke-width:2px,color:#fff
    style P24 fill:#FF9800,stroke:#E65100,stroke-width:2px,color:#fff
    style P25 fill:#FF9800,stroke:#E65100,stroke-width:2px,color:#fff
    style P26 fill:#FF9800,stroke:#E65100,stroke-width:2px,color:#fff
```

---

## DFD Level 2 - Process 3.0: Order Management

```mermaid
flowchart TB
    Customer([Customer])
    
    P31[3.1<br/>Add to Cart]
    P32[3.2<br/>Cart Management]
    P33[3.3<br/>Place Order]
    P34[3.4<br/>Generate Token]
    P35[3.5<br/>Order Tracking]
    P36[3.6<br/>Stock Deduction]
    
    D2[(Food Item Database)]
    D3[(Order/Payment Database)]
    D4[(Stock Database)]
    
    Customer -->|Select Food| P31
    P31 -->|Fetch Food Details| D2
    D2 -->|Food Info| P31
    P31 -->|Add to Cart| P32
    P32 -->|Cart Stored| Customer
    
    Customer -->|View/Modify Cart| P32
    P32 -->|Update Cart| P32
    P32 -->|Display Cart| Customer
    
    Customer -->|Checkout| P33
    P32 -->|Cart Items| P33
    P33 -->|Create Order| D3
    P33 -->|Order Details| P34
    
    P34 -->|Generate Token| P34
    P34 -->|Token Number| D3
    D3 -->|Order with Token| P34
    P34 -->|Token & Receipt| Customer
    
    P33 -->|Order Items| P36
    P36 -->|Check Stock| D4
    D4 -->|Stock Levels| P36
    P36 -->|Deduct Quantities| D4
    D4 -->|Stock Updated| P36
    P36 -->|Confirmation| P33
    
    Customer -->|Track Order| P35
    P35 -->|Query Orders| D3
    D3 -->|Order History| P35
    P35 -->|Order Status| Customer
    
    style P31 fill:#42A5F5,stroke:#0D47A1,stroke-width:2px,color:#fff
    style P32 fill:#42A5F5,stroke:#0D47A1,stroke-width:2px,color:#fff
    style P33 fill:#42A5F5,stroke:#0D47A1,stroke-width:2px,color:#fff
    style P34 fill:#42A5F5,stroke:#0D47A1,stroke-width:2px,color:#fff
    style P35 fill:#42A5F5,stroke:#0D47A1,stroke-width:2px,color:#fff
    style P36 fill:#42A5F5,stroke:#0D47A1,stroke-width:2px,color:#fff
```

---

## DFD Level 2 - Process 4.0: Payment Processing

```mermaid
flowchart TB
    Customer([Customer])
    Manager([Manager])
    PaymentGW([SSLCommerz<br/>Payment Gateway])
    
    P41[4.1<br/>Initiate Payment]
    P42[4.2<br/>SSLCommerz Integration]
    P43[4.3<br/>Payment Verification]
    P44[4.4<br/>Payment Recording]
    P45[4.5<br/>Token Generation]
    P46[4.6<br/>Manual Verification]
    
    D3[(Payment Database)]
    D1[(User Database)]
    
    Customer -->|Payment Trigger| P41
    P41 -->|Create Transaction| P41
    P41 -->|Transaction ID| P42
    
    P42 -->|Payment Request| PaymentGW
    PaymentGW -->|Payment Page| Customer
    Customer -->|Payment Info| PaymentGW
    PaymentGW -->|Payment Status| P42
    
    P42 -->|Status Data| P43
    P43 -->|Verify Transaction| P43
    P43 -->|Verified Payment| P44
    
    P44 -->|Payment Record| D3
    D3 -->|Transaction Saved| P44
    P44 -->|Generate Token| P45
    
    P45 -->|Create Token| P45
    P45 -->|Token Number| D3
    D3 -->|Token Stored| P45
    P45 -->|Token & Receipt| Customer
    
    Manager -->|Check Payment| P46
    P46 -->|Query by Token| D3
    D3 -->|Payment Details| P46
    P46 -->|Mark Verified| D3
    P46 -->|Verification Result| Manager
    
    style P41 fill:#AB47BC,stroke:#4A148C,stroke-width:2px,color:#fff
    style P42 fill:#AB47BC,stroke:#4A148C,stroke-width:2px,color:#fff
    style P43 fill:#AB47BC,stroke:#4A148C,stroke-width:2px,color:#fff
    style P44 fill:#AB47BC,stroke:#4A148C,stroke-width:2px,color:#fff
    style P45 fill:#AB47BC,stroke:#4A148C,stroke-width:2px,color:#fff
    style P46 fill:#AB47BC,stroke:#4A148C,stroke-width:2px,color:#fff
```

---

## DFD Level 2 - Process 5.0: Stock Management

```mermaid
flowchart TB
    Manager([Manager])
    OrderProc[Order Process]
    
    P51[5.1<br/>View Stock Levels]
    P52[5.2<br/>Manual Stock Adjustment]
    P53[5.3<br/>Stock Transaction Logging]
    P54[5.4<br/>Low Stock Alert]
    P55[5.5<br/>Automatic Stock Deduction]
    
    D4[(Stock Database)]
    D6[(Transaction Log Database)]
    D2[(Food Item Database)]
    
    Manager -->|View Stock Request| P51
    P51 -->|Query Stock| D4
    D4 -->|Stock Levels| P51
    P51 -->|Display Stock| Manager
    
    Manager -->|Adjust Stock| P52
    P52 -->|Fetch Current Stock| D4
    D4 -->|Current Quantity| P52
    Manager -->|New Quantity| P52
    P52 -->|Calculate Difference| P52
    P52 -->|Update Stock| D4
    P52 -->|Log Transaction| P53
    
    P53 -->|Transaction Details| D6
    D6 -->|Transaction Logged| P53
    P53 -->|Log Confirmation| P52
    P52 -->|Update Complete| Manager
    
    P51 -->|Check Thresholds| P54
    P54 -->|Low Stock Items| Manager
    
    OrderProc -->|Order Placed| P55
    P55 -->|Fetch Stock| D4
    D4 -->|Available Quantity| P55
    P55 -->|Deduct Quantity| D4
    P55 -->|Log Sale| P53
    P53 -->|Sale Transaction| D6
    P55 -->|Stock Updated| OrderProc
    
    style P51 fill:#EF5350,stroke:#B71C1C,stroke-width:2px,color:#fff
    style P52 fill:#EF5350,stroke:#B71C1C,stroke-width:2px,color:#fff
    style P53 fill:#EF5350,stroke:#B71C1C,stroke-width:2px,color:#fff
    style P54 fill:#EF5350,stroke:#B71C1C,stroke-width:2px,color:#fff
    style P55 fill:#EF5350,stroke:#B71C1C,stroke-width:2px,color:#fff
```

---

## DFD Level 2 - Process 6.0: Authentication & Authorization

```mermaid
flowchart TB
    User([User/Customer])
    Manager([Manager])
    Admin([Admin])
    Firebase([Firebase Auth])
    
    P61[6.1<br/>User Authentication]
    P62[6.2<br/>Role Verification]
    P63[6.3<br/>Token Management]
    P64[6.4<br/>Password Management]
    P65[6.5<br/>Session Management]
    
    D1[(User Database)]
    D5[(Employee Database)]
    
    User -->|Login Credentials| P61
    P61 -->|Verify Credentials| D1
    D1 -->|User Record| P61
    P61 -->|Hash Comparison| P61
    P61 -->|Generate Token| P63
    
    P63 -->|Create JWT| P63
    P63 -->|Auth Token| User
    
    User -->|Access Request| P62
    P62 -->|Validate Token| P63
    P63 -->|Token Valid| P62
    P62 -->|Check Role| D1
    D1 -->|User Role| P62
    
    Manager -->|Access Request| P62
    P62 -->|Check Employee| D5
    D5 -->|Manager Role| P62
    P62 -->|Access Granted/Denied| Manager
    
    Admin -->|Access Request| P62
    P62 -->|Check Admin Flag| D1
    D1 -->|Admin Status| P62
    P62 -->|Access Granted| Admin
    
    User -->|Change Password| P64
    P64 -->|Verify Old Password| D1
    D1 -->|Current Hash| P64
    P64 -->|Hash New Password| P64
    P64 -->|Update Password| D1
    P64 -->|Password Changed| User
    
    User -->|Logout| P65
    P65 -->|Invalidate Token| P65
    P65 -->|Clear Session| User
    
    style P61 fill:#26A69A,stroke:#004D40,stroke-width:2px,color:#fff
    style P62 fill:#26A69A,stroke:#004D40,stroke-width:2px,color:#fff
    style P63 fill:#26A69A,stroke:#004D40,stroke-width:2px,color:#fff
    style P64 fill:#26A69A,stroke:#004D40,stroke-width:2px,color:#fff
    style P65 fill:#26A69A,stroke:#004D40,stroke-width:2px,color:#fff
```

---

## DFD Level 2 - Process 7.0: Analytics & Reporting

```mermaid
flowchart TB
    Admin([Admin])
    Manager([Manager])
    
    P71[7.1<br/>Sales Analytics]
    P72[7.2<br/>Stock Reports]
    P73[7.3<br/>User Analytics]
    P74[7.4<br/>Payment Reports]
    P75[7.5<br/>Dashboard Generation]
    
    D3[(Payment Database)]
    D4[(Stock Database)]
    D1[(User Database)]
    D6[(Transaction Log)]
    
    Admin -->|Request Sales Report| P71
    Manager -->|Request Sales Report| P71
    P71 -->|Query Payments| D3
    D3 -->|Payment Records| P71
    P71 -->|Calculate Totals| P71
    P71 -->|Sales Report| Admin
    P71 -->|Sales Report| Manager
    
    Manager -->|Request Stock Report| P72
    P72 -->|Query Stock| D4
    D4 -->|Stock Levels| P72
    P72 -->|Query Transactions| D6
    D6 -->|Transaction History| P72
    P72 -->|Stock Report| Manager
    
    Admin -->|Request User Analytics| P73
    P73 -->|Query Users| D1
    D1 -->|User Data| P73
    P73 -->|Query Orders| D3
    D3 -->|Order Data| P73
    P73 -->|User Analytics| Admin
    
    Manager -->|Request Payment Report| P74
    P74 -->|Query Payments| D3
    D3 -->|Payment Details| P74
    P74 -->|Generate Report| P74
    P74 -->|Payment Report| Manager
    
    Admin -->|Dashboard Request| P75
    Manager -->|Dashboard Request| P75
    P75 -->|Aggregate Data| P71
    P75 -->|Aggregate Data| P72
    P75 -->|Aggregate Data| P73
    P75 -->|Aggregate Data| P74
    P75 -->|Dashboard Data| Admin
    P75 -->|Dashboard Data| Manager
    
    style P71 fill:#FFD54F,stroke:#F57F17,stroke-width:2px,color:#333
    style P72 fill:#FFD54F,stroke:#F57F17,stroke-width:2px,color:#333
    style P73 fill:#FFD54F,stroke:#F57F17,stroke-width:2px,color:#333
    style P74 fill:#FFD54F,stroke:#F57F17,stroke-width:2px,color:#333
    style P75 fill:#FFD54F,stroke:#F57F17,stroke-width:2px,color:#333
```

---

## Complete System Overview

```mermaid
flowchart TB
    subgraph External["External Entities"]
        Customer([Customer])
        Admin([Admin])
        Manager([Manager])
        PaymentGW([Payment Gateway])
        CloudStorage([Cloud Storage])
    end
    
    subgraph Core["Core System Processes"]
        P1[User Management]
        P2[Menu Management]
        P3[Order Management]
        P4[Payment Processing]
        P5[Stock Management]
        P6[Authentication]
        P7[Analytics]
    end
    
    subgraph Storage["Data Stores"]
        D1[(User DB)]
        D2[(Food Item DB)]
        D3[(Payment DB)]
        D4[(Stock DB)]
        D5[(Employee DB)]
        D6[(Transaction Log)]
    end
    
    Customer --> P1
    Customer --> P2
    Customer --> P3
    Customer --> P4
    Customer --> P6
    
    Admin --> P1
    Admin --> P7
    Admin --> P6
    
    Manager --> P2
    Manager --> P4
    Manager --> P5
    Manager --> P7
    Manager --> P6
    
    P2 --> CloudStorage
    P4 --> PaymentGW
    
    P1 --> D1
    P1 --> D5
    P2 --> D2
    P3 --> D3
    P4 --> D3
    P5 --> D4
    P5 --> D6
    P6 --> D1
    P6 --> D5
    P7 --> D1
    P7 --> D3
    P7 --> D4
    P7 --> D6
    
    P3 --> P5
    P3 --> P4
    
    style Core fill:#FFE0E0,stroke:#DC0000,stroke-width:2px
    style External fill:#E8F5E9,stroke:#2E7D32,stroke-width:2px
    style Storage fill:#E1F5FE,stroke:#0277BD,stroke-width:2px
```

---

## Key Data Flows Summary

### 1. User Management Flow
- **Registration**: Customer → Registration Form → Validation → User Database
- **Manager Creation**: Admin → Manager Details → Employee Database + User Role Update
- **User Control**: Admin → User Actions → User Database → Action Confirmation

### 2. Menu Management Flow
- **Browse Menu**: Customer → Menu Request → Food Database → Display Menu
- **Add Food**: Manager → Food Details → Image Upload (Cloudinary) → Food Database + Stock Database
- **Update/Delete**: Manager → Food Actions → Database Update → Confirmation

### 3. Order Management Flow
- **Place Order**: Customer → Cart → Order Creation → Payment Database + Stock Deduction
- **Token Generation**: Order → Token Creation → Token Number → Customer
- **Track Order**: Customer → Order Query → Payment Database → Order Status

### 4. Payment Processing Flow
- **Online Payment**: Customer → Payment Init → SSLCommerz → Transaction Verification → Database
- **Token Pickup**: Customer → Pay Outside → Token Number → Manual Verification by Manager
- **Payment History**: Manager → Query Payment → Database → Payment Details

### 5. Stock Management Flow
- **View Stock**: Manager → Stock Query → Stock Database → Stock Levels
- **Adjust Stock**: Manager → Stock Update → Database → Transaction Log
- **Automatic Deduction**: Order Placed → Stock Check → Deduct Quantity → Update Database
- **Low Stock Alert**: System → Check Thresholds → Alert Manager

### 6. Authentication Flow
- **Login**: User → Credentials → Verify → Generate JWT Token → Access Granted
- **Role Check**: Access Request → Verify Token → Check Role → Allow/Deny
- **Session**: Login → Token → Active Session → Logout → Invalidate

### 7. Analytics Flow
- **Sales Report**: Admin/Manager → Query Payments → Calculate → Report
- **Stock Report**: Manager → Query Stock + Transactions → Generate Report
- **Dashboard**: Admin/Manager → Aggregate All Data → Display Analytics

---

## Database Schema Overview

### Primary Tables
1. **User** - Customer registration, authentication
2. **Employee** - Manager/staff records
3. **FoodItem** - Menu items with details
4. **Stock** - Inventory management
5. **Payment** - Order and payment records
6. **StockTransaction** - Stock movement logs

### Key Relationships
- User → Payment (One-to-Many)
- FoodItem → Stock (One-to-One)
- FoodItem → StockTransaction (One-to-Many)
- Payment → CartItems (Embedded Array)
- Employee → User (Role Assignment)

---

## System Features Highlighted in DFD

### Customer Features
- ✅ Browse menu items
- ✅ Search for specific food
- ✅ Place orders
- ✅ Online payment via SSLCommerz
- ✅ Receive token number
- ✅ Track order history
- ✅ Pay outside and use token

### Admin Features
- ✅ Add and manage managers
- ✅ View all registered users
- ✅ Control user accounts
- ✅ View system analytics
- ✅ Access all reports

### Manager Features
- ✅ View registered users
- ✅ Add/modify/remove menu items
- ✅ Manage food images
- ✅ Update stock levels
- ✅ View payment details
- ✅ Verify token-based payments
- ✅ Generate reports
- ✅ Monitor low stock alerts

---

## Technology Integration Points

### Frontend (React.js + Tailwind CSS)
- User interface for all actors
- Real-time cart management
- Responsive design
- State management (Redux)

### Backend (Node.js + Express.js)
- RESTful API endpoints
- Business logic processing
- Middleware for authentication
- Error handling

### Database (MongoDB)
- NoSQL document storage
- Flexible schema
- Efficient queries
- Data persistence

### External Services
- **SSLCommerz**: Payment gateway integration
- **Cloudinary**: Image storage and management
- **Firebase**: Authentication support (optional)

---

## Legend
- **Squares**: Processes (system functions)
- **Circles**: External entities (users, services)
- **Cylinders**: Data stores (databases)
- **Arrows**: Data flows (information movement)
- **Colors**: Different functional areas

---

## Notes on DFD Levels

### Level 0 (Context Diagram)
- Shows entire system as single process
- All external entities
- High-level data flows
- System boundaries

### Level 1
- Major processes (7 main modules)
- All data stores
- External entity interactions
- Inter-process data flows

### Level 2
- Detailed sub-processes for each major process
- Internal logic and workflows
- Database operations
- Business rules implementation

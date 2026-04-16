# AURA Order Management System - Quick Start

## 📂 Files Overview

| File | Purpose | Users |
|------|---------|-------|
| `ar-menu-v2.html` | Customer ordering interface with AR | Customers, Waiters |
| `admin-panel.html` | Kitchen/Manager order dashboard | Kitchen Staff, Managers |
| `README.md` | Full documentation | Everyone |

---

## 🚀 How to Use

### Step 1: Customer Places Order
**File**: `ar-menu-v2.html`

```
1. Open ar-menu-v2.html in browser/tablet
2. Enter table number (optional)
3. Click on a dish to view details
4. For AR items: Click "Place on My Table" to see in AR
5. Adjust quantity with +/− buttons
6. Add special requests if needed (allergies, preferences)
7. Click "Add to Order"
8. In cart: Review items and total
9. Click "Place Order" → Confirmation appears
```

**✨ Features:**
- Multi-language (EN, AR, FR)
- Dark mode
- Search & category filters
- 3D model viewer
- AR placement capability
- Real-time cart calculation

---

### Step 2: Admin Receives & Processes Order
**File**: `admin-panel.html`

```
1. Open admin-panel.html
2. Login with: admin / aura2025
3. Orders appear in "New Orders" tab automatically (every 2 seconds)
4. Click an order to see details
5. Review items and special requests
6. Click appropriate button:
   - ✅ Accept Order (if you want to take the order)
   - 👨‍🍳 Start Preparing (when you start cooking)
   - 📦 Mark Ready for Pickup (when done cooking)
   - 🗑 Reject Order (if you can't fulfill it)
7. Status automatically updates in order list
```

**✨ Features:**
- Real-time order updates every 2 seconds
- Live statistics dashboard
- Filter by status (New, Accepted, Preparing, Completed)
- Color-coded indicators
- Full order details with items and notes
- Multi-status order tracking

---

## 🔄 Order Status Flow

```
CUSTOMER PERSPECTIVE:
┌─────────────────────────────────────────────────┐
│ Customer places order (ar-menu-v2.html)          │
│ → Gets order confirmation with ID               │
│ → Can refresh to see order status if needed     │
└─────────────────────────────────────────────────┘

ADMIN PERSPECTIVE:
┌─────────────────────────────────────────────────┐
│ [NEW ORDER] 🔴                                   │
│ ↓ (Admin clicks Accept)                         │
│ [ACCEPTED] ✅                                   │
│ ↓ (Admin clicks Start Preparing)               │
│ [PREPARING] 👨‍🍳                              │
│ ↓ (Admin clicks Mark Ready)                    │
│ [COMPLETED] ✔️                                 │
│ ↓                                               │
│ Order history maintained                        │
└─────────────────────────────────────────────────┘
```

---

## 🔐 Admin Login

**Default Credentials:**
- **Username**: `admin`
- **Password**: `aura2025`

🔒 **Change password** by editing both HTML files:
1. Find: `const ADMIN_PASS = 'aura2025'`
2. Replace with new password

---

## 📊 Dashboard Statistics

Admin panel shows real-time numbers:
- **New**: Count of pending orders awaiting acceptance
- **Preparing**: Count of orders currently being prepared
- **All Orders**: Total count in current filter

Numbers update automatically every 2 seconds.

---

## 🎨 Customization Quick Tips

### Change Primary Color
In both HTML files, find:
```css
--primary: #ffc107;  /* Yellow */
```
Change to any hex color (e.g., `#00BCD4` for cyan)

### Change Admin Password
In both HTML files, find:
```javascript
const ADMIN_PASS = 'aura2025';
```

### Change Auto-Refresh Rate
In `admin-panel.html`, find:
```javascript
}, 2000);  // Change to 3000 for 3 seconds, etc.
```

### Add More Dishes
In `ar-menu-v2.html`, find `DISHES_DEFAULT` object and add new entries following the existing pattern.

---

## 🌙 Features Toggle

### Dark Mode
- Click moon icon in top-right corner
- Preference auto-saves
- Works on both client and admin sites

### Language
- Click language button (EN/AR/FR)
- Supports: English, Arabic, French
- Preference auto-saves

---

## 💾 Data Storage

All data stored in **browser's localStorage**:
- ✅ Survives browser refresh
- ✅ Survives browser close and reopen
- ✅ Survives device restart
- ❌ Lost if browser cache is cleared

**For production**: Integrate with backend database!

---

## ⚡ Real-Time Features

### How Information Syncs Between Sites

1. **Client creates order**
   - Saves to: `localStorage['aura_orders']`

2. **Admin panel auto-refreshes**
   - Every 2 seconds checks: `localStorage['aura_orders']`
   - Displays new/updated orders immediately

3. **Admin updates order status**
   - Modifies: `localStorage['aura_orders']`
   - Client can see status if they refresh (enhanced in next version)

### Polling Mechanism
- Not real-time WebSocket (requires backend)
- Simple localStorage polling (development-friendly)
- Production should use WebSocket or HTTP polling with server

---

## 📱 Device Recommendations

| Device | Experience | Status |
|--------|-----------|--------|
| iPad/Tablet | ⭐⭐⭐⭐⭐ Optimal | ✅ Recommended |
| Desktop Browser | ⭐⭐⭐ Good | ✅ Works |
| Mobile Phone | ⭐⭐ Limited | ✅ Functional |
| Android Phone | ⭐⭐⭐ Good (AR) | ✅ AR Ready |

---

## 🎯 Use Cases

### Restaurant Setting
```
DINING AREA:
- Tablet on each table with ar-menu-v2.html
- Customers browse and order from their table

KITCHEN:
- iPad/Desktop with admin-panel.html
- Chef sees all orders with status
- Prep based on order sequence
- Mark complete when dish is ready
```

### Order-at-Counter Setting
```
FRONT COUNTER:
- Tablet with ar-menu-v2.html
- Staff enters table/order number
- Display on large screen with AR

KITCHEN:
- Admin panel on multiple displays
- Staff monitors live order queue
- Updates status as items complete
```

---

## 🔧 Troubleshooting

| Issue | Solution |
|-------|----------|
| Orders not showing in admin | Make sure admin site is open; check localStorage in DevTools |
| Admin login rejected | Use: admin / aura2025 (case-sensitive) |
| Auto-refresh not working | Close and reopen admin panel; check browser console |
| AR not working | Use Chrome (Android) or Safari (iOS 12+) |
| Dark mode not saving | Check if localStorage is enabled in browser settings |

---

## 📈 Next Steps / Enhancements

Not included but recommended:

1. **Backend API** - Replace localStorage with real database
2. **WebSocket** - Real-time updates instead of polling
3. **Mobile App** - Native apps for iOS/Android
4. **Payment** - Integrate payment gateway
5. **Analytics** - Track revenue, popular items
6. **Delivery Integration** - Connect with Uber Eats, DoorDash, etc.
7. **Kitchen Display** - Larger screens for kitchen
8. **Customer Portal** - Customers track order status
9. **Inventory** - Track ingredients and stock
10. **Reporting** - Daily/weekly sales reports

---

## 🎓 Learning Resources

### To Modify This System:
- **HTML**: Structure & layout of pages
- **CSS**: Styling, colors, animations
- **JavaScript**: Order logic, data management, UI interactions

### Key JavaScript Concepts Used:
- localStorage API
- Event listeners
- Array methods (map, filter, find)
- Object manipulation
- DOM manipulation

---

## 📞 Support & Documentation

For more detailed information, see `README.md`

Contains:
- Full feature list
- Order workflow diagram
- Data structure specifications
- Deployment guidelines
- Security considerations
- Advanced customization

---

**Happy Managing! 🚀**

Version 1.0 | April 2024

# AURA — Smart Restaurant Order Management System

## 📱 System Overview

This is a complete Android tablet-ready restaurant ordering system with:
- **Client Site** (`ar-menu-v2.html`) - AR menu for customers to place orders
- **Admin Panel** (`admin-panel.html`) - Order management dashboard for kitchen staff and managers

## 🎯 Features

### Client Site (ar-menu-v2.html)
✅ **Augmented Reality Menu**
- 3D food models with AR viewing capability
- Interactive hotspots with nutritional information
- AR placement on tables/surfaces

✅ **Smart Ordering**
- Browse by categories (Salads, Mains, Starters, Desserts)
- Search functionality
- Special requests & allergy notes
- Quantity adjustment
- Real-time cart updates with sub-total, tax, total

✅ **User Experience**
- Dark mode support
- Multi-language support (English, Arabic, French)
- Table number input
- Order confirmation modal
- Responsive design for tablets

### Admin Panel (admin-panel.html)
✅ **Order Management Dashboard**
- Real-time order list with auto-refresh (every 2 seconds)
- Filter by status: All, New, Accepted, Preparing, Completed
- Order status indicators with color coding

✅ **Order Processing**
- View detailed order information
- Accept/Reject new orders
- Track cooking progress (Pending → Accepted → Preparing → Ready)
- Mark orders as completed
- View all items, special notes, and pricing

✅ **Analytics**
- Live statistics for new and preparing orders
- Order counting by status
- Quick order overview

✅ **Security**
- Admin login (default: admin / aura2025)
- Session persistence
- Dark mode toggle

## 🔄 Order Workflow

```
1. CLIENT PLACES ORDER
   ↓
2. ORDER STORED IN BROWSER STORAGE (localStorage)
   ↓
3. ADMIN SEES NEW ORDER (appears in "New Orders" list)
   ↓
4. ADMIN ACCEPTS ORDER
   ↓
5. ORDER STATUS → "ACCEPTED" (customer could see status if they refresh)
   ↓
6. ADMIN CLICKS "START PREPARING"
   ↓
7. ORDER STATUS → "PREPARING" (kitchen working on it)
   ↓
8. ADMIN MARKS "READY FOR PICKUP"
   ↓
9. ORDER STATUS → "COMPLETED"
   ↓
10. ORDER HISTORY MAINTAINED IN STORAGE
```

## 🛠️ How It Works

### Data Storage
- **Orders Database**: Stored in `localStorage` as `aura_orders` (JSON array)
- **Theme Preference**: Stored as `aura_theme` (light/dark)
- **Language Preference**: Stored as `aura_lang` (0=EN, 1=AR, 2=FR)

### Communication Between Sites
Both sites share the same `localStorage` space in the same browser domain:

**Client Site** → Creates orders and saves to `aura_orders` array
**Admin Panel** → Reads/updates `aura_orders` array every 2 seconds

This means:
- ✅ Both sites must be open in tabs in the same browser
- ✅ Admin sees orders immediately upon placement

### Order Object Structure
```javascript
{
  id: "ORD-1234567890",           // Unique order ID
  timestamp: "2024-04-16T...",    // ISO timestamp
  tableNum: "5",                   // Table number
  items: [
    {
      id: "avocado",              // Dish ID
      name: "Avocado Garden",      // Display name
      price: 18,                   // Unit price
      qty: 2,                      // Quantity
      note: "No nuts",             // Special requests
      emoji: "🥑"                  // Display emoji
    }
  ],
  subtotal: 36,                    // Sum before tax
  tax: 3.6,                        // 10% tax
  total: 39.6,                     // Final amount
  status: "pending",               // pending|accepted|preparing|completed|rejected
  customerName: "Guest",           // Customer name
  notes: ""                        // Additional notes
}
```

## 🚀 Usage Guide

### For Customers (Client Site)

1. **Open the Menu**
   - Open `ar-menu-v2.html` on tablet/iPad
   - Enter table number (optional)

2. **Browse & Select Dishes**
   - Tap category buttons (Salads, Mains, etc.)
   - Tap dish card to view details
   - For AR items: Tap to see 3D model, use AR button to place in room

3. **Add to Order**
   - Adjust quantity with +/− buttons
   - Add special requests (e.g., "No nuts")
   - Tap "Add to Order" button

4. **Place Order**
   - Tap cart icon (top right)
   - Review items and pricing
   - Tap "Place Order"
   - Confirmation modal appears with order number

### For Admin/Manager (Admin Panel)

1. **Login**
   - Open `admin-panel.html`
   - Enter credentials (admin / aura2025)
   - Dashboard appears

2. **View New Orders**
   - Pending orders appear in "New Orders" filter
   - Statistics show count of new & preparing orders
   - Orders auto-refresh every 2 seconds

3. **Process Orders**
   - Click on order in list to view details
   - See all items, special notes, customer table, total
   - Click appropriate action button:
     - **Accept Order** → Order moves to "Accepted" status
     - **Start Preparing** → Status changes to "Preparing"
     - **Mark Ready for Pickup** → Status changes to "Completed"

4. **Track Progress**
   - Left sidebar shows all orders with status color indicators
   - Green bar = Accepted
   - Orange bar = Preparing
   - Blue bar = Completed
   - Status badges show current state

## 🎨 Colors & Indicators

| Status | Color | Emoji | Meaning |
|--------|-------|-------|---------|
| Pending (New) | Red | 🔴 | Awaiting restaurant confirmation |
| Accepted | Green | ✅ | Restaurant accepted the order |
| Preparing | Orange | 👨‍🍳 | Kitchen is preparing the order |
| Completed | Blue | ✔️ | Order ready for pickup/delivery |

## 🔐 Admin Credentials

**Default Login:**
- Username: `admin`
- Password: `aura2025`

⚠️ **Security Note**: For production, implement proper backend authentication and database!

## 💾 Data Persistence

- **Survives browser restart**: Yes (saved in localStorage)
- **Survives browser close**: Yes
- **Survives device reboot**: Yes
- **Survives app update**: Yes (if localStorage not cleared)
- **Stored location**: Browser's localStorage (no server)

## 🔄 Real-time Updates

Admin Panel features **auto-refresh every 2 seconds**:
- New orders appear automatically
- Order counts update
- Status changes reflect immediately
- No manual refresh needed

## 📊 Dashboard Statistics

Two key metrics displayed in admin panel:
1. **New Orders** - Count of pending orders
2. **Preparing** - Count of orders being prepared

These update in real-time as orders are processed.

## 🛠️ Customization

### Change Admin Password
Edit `ar-menu-v2.html` and `admin-panel.html`:
```javascript
const ADMIN_USER = 'admin';
const ADMIN_PASS = 'aura2025';  // Change this
```

### Modify Menu Items
Edit `ar-menu-v2.html` in the `DISHES_DEFAULT` object:
- Change prices, descriptions
- Add/remove categories
- Update 3D models (glb URLs)

### Change Refresh Rate
In `admin-panel.html`, modify:
```javascript
startAutoRefresh()
updateInterval = setInterval(() => {
  loadOrders();
}, 2000);  // milliseconds - change this number
```

### Styling
All CSS variables can be customized:
- Colors: `--primary`, `--accent`, `--success`, etc.
- Fonts: `--font-serif`, `--font-sans`
- Shadows: `--shadow-sm`, `--shadow-md`, `--shadow-lg`

## 📱 Responsive Design

- ✅ **Tablet**: Full experience (recommended)
- ✅ **Desktop**: Works but optimized for tablets
- ✅ **Mobile**: Functions but cramped (use portrait orientation)

## 🐛 Troubleshooting

### Orders not appearing in admin panel?
1. Make sure both sites use the same browser tab domain
2. Check if admin browser's localStorage isn't blocked
3. Verify cookies/storage are enabled

### Admin panel shows empty list?
1. Make sure orders were placed on client site
2. Login to admin panel
3. The orders should auto-refresh within 2 seconds

### Auto-refresh not working?
1. Check browser console for errors
2. Verify JavaScript is enabled
3. Try refreshing the page

### AR not working?
1. Use Chrome (Android) or Safari (iOS 12+)
2. Ensure device supports WebXR
3. Check model files are loading (check network tab)

## 📦 Deployment

For production deployment:
1. **Backend Integration**: Replace localStorage with real database (Firebase, PostgreSQL, etc.)
2. **Real-time Updates**: Implement WebSocket instead of polling
3. **Authentication**: Use proper OAuth/JWT tokens
4. **API Endpoints**: Connect to REST/GraphQL API
5. **Multi-Restaurant**: Add restaurant ID/tenant isolation
6. **Order Printing**: Integrate with kitchen display systems (KDS)

## 🔒 Security Considerations

**Current Implementation**: Demo/Development only

**For Production, Add:**
- ✅ Backend authentication
- ✅ Encrypted data transmission (HTTPS)
- ✅ Role-based access control (RBAC)
- ✅ Input validation & sanitization
- ✅ Rate limiting on order submissions
- ✅ Database transactions for data integrity
- ✅ Audit logging for all changes
- ✅ Payment gateway integration

## 📞 Support

**System Architecture:**
- Frontend: Pure HTML/CSS/JavaScript (no dependencies)
- Storage: Browser localStorage
- Communication: localStorage polling
- Real-time: 2-second refresh interval

**Improvements for Production:**
- Implement backend API
- Add database
- Real-time WebSockets
- Mobile app versions
- Payment processing
- Multi-language support enhancement

---

## Quick Start

1. **Customer orders food:**
   - Open `ar-menu-v2.html`
   - Select dishes, add to order
   - Enter table number
   - Click "Place Order"

2. **Admin receives & processes order:**
   - Open `admin-panel.html`
   - Login (admin/aura2025)
   - Click on new order
   - Update status as you prepare
   - Mark complete when ready

3. **Track Everything:**
   - See real-time stats
   - Filter by order status
   - View detailed order info
   - Manage kitchen workflow

---

**Version**: 1.0  
**Last Updated**: April 2024  
**Status**: Production Ready (with backend integration)

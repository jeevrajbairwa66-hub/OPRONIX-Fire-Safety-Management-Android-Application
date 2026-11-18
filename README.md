# OPRONIX — Fire Safety Solutions (Android)

OPRONIX is a complete, native Android application built with Kotlin, Jetpack Compose, and Material 3 for a fire safety products and services enterprise in India.

---

## 🚒 Key Capabilities

1. **Product Catalogue (15 Certified Ranges)**:
   - ABC Stored Pressure Fire Extinguishers (1kg, 2kg, 4kg, 6kg, 9kg)
   - CO2 Clean Agent Extinguishers (2kg, 4.5kg)
   - Mechanical Foam (AFFF) & Water-type extinguishers
   - Optical Smoke & Rate-of-Rise Heat Detectors
   - Microprocessor Fire Alarm Control Panels & Strobe Hooters
   - Automatic Glass Bulb Fire Sprinklers (68°C) & 30m Fire Hose Reels
   - Oblique Fire Hydrant Landing Valves (IS 5290)
   - Photoluminescent Glow Signage, Emergency LED Lights & Fiberglass Blankets
   - Safety stands, brackets, and accessories

2. **Cart & Tax Invoice Checkout**:
   - Dynamic cart quantity adjustments & item deletion
   - Statutory 18% GST calculation on safety equipment
   - Safe logistics freight calculation
   - Promo coupon engine (`FIRESAFE10` for 10% instant discount)
   - Commercial invoice breakdown with shareable summaries

3. **Field Services & Maintenance**:
   - Cylinder refilling, hydro-testing, and pressure verification
   - Smoke detector & alarm panel wiring and setup
   - Comprehensive fire safety audit requests under NBC 2016 Part 4
   - Real-time service booking tracking with assigned safety engineer credentials

4. **Commercial Quotations**:
   - Turnkey project inquiry builder
   - Itemized commercial estimate proposals
   - PDF proposal export & share intent

5. **Annual Maintenance Contracts (AMC)**:
   - Essential, Commercial Pro, and Industrial Enterprise tiers
   - Quarterly audit tracking and scheduled compliance logs

6. **Role-Based Perspectives (Demo Switcher)**:
   - **Customer**: Browse products, order, request audits, view invoices
   - **Field Technician**: View assigned site visits, customer location, update job status (In Progress → Completed)
   - **Administrator**: Executive KPI dashboard, inventory management (Add/Delete/Stock), order dispatch lifecycle, technician assignment, quote approval

7. **Emergency Guidance & Verified Contacts**:
   - Prominent notice for active fire incidents directing users to **101 (Fire Brigade)** and **112 (National Emergency)**
   - Single-tap dialer for OPRONIX Customer Helpdesk (`+91 98290 88888`), WhatsApp Business, and Office Map navigation

---

## 🛠️ Architecture & Tech Stack

- **UI**: 100% Jetpack Compose + Material 3
- **Design Palette**: Fire Red (`#E53935`), Safety Orange (`#FF8A00`), Deep Charcoal (`#101820`)
- **Architecture**: MVVM with Repository Pattern and reactive `StateFlow`
- **Navigation**: Jetpack Navigation Compose
- **Persistence & Cloud**: Switchable architecture with `DemoRepository` (instant offline sandbox) and `FirebaseRepository` (Cloud Firestore & Auth ready)
- **Minimum SDK**: 26 (Android 8.0 Oreo) | **Target SDK**: 36

---

## 📸 Product Image Management & Dual-Mode Storage

OPRONIX includes end-to-end product photo management in the Admin Portal:

1. **Android Photo Picker**: Zero-permission `ActivityResultContracts.PickMultipleVisualMedia(5)` allows admins to choose up to 5 photos from their gallery or device files.
2. **Format & Size Validation**: Validates file types (`JPG`, `JPEG`, `PNG`, `WebP`) and enforces a 5 MB limit per image before upload.
3. **Interactive Previews**: Provides thumbnail preview carousel with Cover/Primary badge on the first photo and individual delete controls.
4. **Dual-Mode Persistence**:
   - **Cloud Mode (Firebase Storage)**: Uploads photos to `product_images/{productId}/{filename}` and saves permanent download URLs to Cloud Firestore.
   - **Demo / Offline Mode**: Copies image byte streams directly to internal persistent app storage (`context.filesDir/product_images/`) and stores permanent `file://` URIs, ensuring images remain associated with products and survive app restarts and process recreation without needing a live cloud backend.
5. **Customer Catalogue Integration**: Product primary image is displayed on `ProductCard`, search results, featured products carousel, shopping cart rows, and admin inventory list. `ProductDetailScreen` features an interactive swipeable gallery with page indicator dots and thumbnail selector.

---

## ☁️ Firebase Cloud Setup Instructions

To connect OPRONIX to live Firebase Authentication, Cloud Firestore, and Cloud Storage:

1. **Create a Firebase Project**:
   - Visit the [Firebase Console](https://console.firebase.google.com/) and create a new project.
2. **Add an Android App**:
   - Set the Package name to match `applicationId` (e.g. `com.aistudio.opronix.frst`).
   - Download `google-services.json` and place it in the `/app` folder.
3. **Enable Cloud Firestore**:
   - In Firebase Console > Build > Firestore Database, create a database in production mode.
   - Deploy `firestore.rules`.
4. **Enable Cloud Storage**:
   - In Firebase Console > Build > Storage, click **Get Started**.
   - Deploy `storage.rules` (included in project root) to enforce 5 MB limit and image content-type checks.
5. **Enable Firebase Authentication**:
   - In Firebase Console > Build > Authentication, enable **Email/Password** and **Google Sign-In**.

---

## 🧪 Unit Tests

Run local unit tests via Gradle:
```bash
gradle :app:testDebugUnitTest
```
Tests cover:
- Cart subtotal, 18% GST statutory calculation, delivery fee, and coupon logic
- Indian phone number (10-digit) and email format validation
- Order placement, tracking notes, and status transition workflows
- Demo repository live CRUD operations
- Product image validation and model multi-image support


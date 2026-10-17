# Captain Delivery (دليفري القبطان) — v4 (English prompts, in user-journey order)

**Important:** the prompts are in English, but the app UI must stay in Arabic. Every string in quotation marks is the exact Arabic copy to use on screen.

Contents:
1. Owner review: what a delivery-company owner would reject in v3, and the fix
2. Operating model v4
3. Master design system (paste first)
4. Customer app prompts, in the order the user sees them (1–13)
5. Company-side prompts that the owner will ask for on day one (14–15)
6. Build order and checklist

---

## 1. Owner review (the delivery-company owner's view of v3)

**Verdict: the owner would reject v3.** It looks tidy but it is a shopping launcher, not a delivery company's app.

| # | What the owner sees | Fix in v4 |
|---|---|---|
| 1 | Orders go to the merchant over WhatsApp. My company is not in the loop, so I earn nothing from the delivery. | Orders enter the company's own system. The company dispatches, delivers and charges the delivery fee. |
| 2 | No dispatch: no captain assignment, no tracking, no ETA. I cannot promise "fast delivery". | Live tracking, ETA, captain card and a dispatch dashboard are back. |
| 3 | The word "captain" was removed from the UI, so my brand is invisible. | "قبطانك" returns as the company's own rider, with consistent brand voice. |
| 4 | Customers add any website. I cannot guarantee stock, quality, pickup or liability. | Partner stores are curated and managed by the company in the dashboard. Customers can only suggest a store. |
| 5 | Delivery fee, time and hours were typed in by random users. | The company sets zones, fees, hours, prep time and minimum order per store. |
| 6 | No customer accounts or phone numbers, so no retention, marketing or analytics. | Phone OTP sign-in at first checkout, with a customer base owned by the company. |
| 7 | Customers mark their own order "received". That is not an operational status. | Statuses are driven by dispatch and the captain app. |
| 8 | Cash on delivery with no reconciliation. | Captain app records cash collected, and the dashboard tracks the balance each captain owes. |
| 9 | Support contact opened the merchant's chat. | Support goes to the company's WhatsApp and phone, set once in app config (empty in the design). |
| 10 | No captain app and no admin panel. | Both are specified below as required deliverables. |
| 11 | Data lived only on the device. | Everything lives in the company backend. |

---

## 2. Operating model v4

- **Three products ship together:** the customer app, the captain app, and the dispatch dashboard (web). Without all three there is no delivery business.
- **Flow:** the customer orders from a partner store, the order reaches the dispatcher, a captain is assigned, picks up from the store, delivers and collects cash, and the customer tracks everything live.
- **Stores** are added and maintained by company staff. Catalogs come from import (where the store's site allows it) or manual entry. The store's own phone or WhatsApp is used by company staff only and is never shown to customers.
- **Pricing and fees:** product prices come from the catalog. The delivery fee is by zone, set by the company. The total shown to the customer is final unless an item becomes unavailable, in which case support contacts the customer.
- **Payment:** cash on delivery in phase 1. Card payment later through a licensed payment gateway sheet (never raw card fields in the app).
- **Support WhatsApp/phone:** one number set by the owner in config. All "contact support" buttons are hidden while it is empty.
- **Order statuses:** "قيد المراجعة" (pending confirmation), "قيد التجهيز", "في الطريق", "تم التسليم", "ملغي".

---

## 3. Master design system (paste this first)

```
Design system for "دليفري القبطان" (Captain Delivery), a fast-delivery company app. Version 4. Follow it strictly in every screen I ask for later, without me repeating it.

Language and direction:
- RTL everywhere, right-aligned. The back arrow points right.
- Fonts: IBM Plex Sans Arabic, fallback Cairo.
- All UI copy is simple Modern Standard Arabic. Prompts are in English; every quoted string is the exact Arabic copy to display.
- Numerals: Eastern Arabic digits (١٢٣) for display (prices, quantities, times, order numbers). Latin digits (123) inside input fields (phone, OTP) with LTR content.
- Currency after the number: "١٨٠ ج.م".
- Terminology: "قبطان" is the company's own delivery rider. "المتجر" is a partner store.

Colors, light mode:
- Primary #0F3D2E. Primary container #E3EFE8.
- Gold #C9A227: decoration, fills, icons and very large headings only.
- Gold text or gold links on light backgrounds: #7A5C00 (about 5.8:1). Never use #C9A227 for small text on light backgrounds.
- Gold container #F6EBC4.
- Page background #FAF7F2. Cards #FFFFFF. Input fields #F1ECE2.
- Primary text: dark black #111111. Secondary text #5F6B66.
- Error #B3261E, error container #F9DEDC.

Colors, dark mode (follows the system automatically):
- Background #0B1F18, surfaces #12302A, fields #1A3D35, text #F3EFE6, secondary text #A9B8B1.
- Primary buttons in dark mode: gold #C9A227 fill with #0B1F18 text (never use primary green as a button fill in dark mode).
- Headings in dark mode use #F3EFE6, not green.
- Gold text is allowed in dark mode (#C9A227). Error #F2B8B5.

Shape and style:
- Cards and fields with 20px radius, no borders, very light shadow (dark mode: no shadow, separate with surface color).
- No gradients anywhere. No emoji. No third-party logos (including WhatsApp): use a generic outline chat-bubble icon.
- Outline icons with a uniform 1.75px stroke.
- Spacing in multiples of 8px, 24px screen margins.
- Touch targets at least 48px, primary buttons 56px, smallest text 13px.
- Background pattern at 5% opacity only: ship's wheel, compass, wave lines and speed lines. No pattern behind long text.

The only allowed exceptions to "no borders":
1. Input fields: 1px #B9AE98 (dark: #3A5A50).
2. Empty "add/suggest" cards: dashed 1.5px #7A5C00 (dark: #C9A227).
3. Focus ring: 2px primary green (dark: gold).

Outputs: ready-to-use code with CSS variables for colors and spacing reused across screens. Every text color must reach at least 4.5:1 contrast.

Confirm you have registered the system and do not create any screen yet.
```

---

## 4. Customer app prompts (in the order the user sees them)

> Every prompt assumes design system v4 is registered. Do not copy any logo, name or illustration from another app. Reference images are for layout only.

### 1. Splash

```
Design the splash screen for the "دليفري القبطان" app, 390×844, following design system v4.

- Solid green #0F3D2E background. Pattern (ship's wheel, waves, speed lines) in gold at 5% opacity.
- Center: an original simple logo: a gold outline ship's wheel with three speed lines crossing it. No frame or box around the logo.
- Below it: "دليفري القبطان" in bold white, then "قبطانك يصلك أسرع" in gold.
- Bottom: a thin gold linear loading indicator.
- Duration 2 seconds, then go to the location screen on first launch, otherwise straight to Home. No onboarding slides.
```

### 2. Location and service area (first launch, and from the address chip later)

```
Design the "delivery location" screen for the "دليفري القبطان" app, 390×844, following design system v4. Shown full-screen on first launch, and as a bottom sheet later from the address chip on Home and from checkout.

Elements:
1. Top bar: back (or close if a sheet) and the title "عنوان التوصيل".
2. Full-width button "استخدام موقعي الحالي" with an outline icon, green container background and green text.
3. Map area: flat solid-shape illustration (roads and blocks, no gradients) with a fixed center pin. No real maps or logos.
4. Empty form fields: "المدينة والحي", "الشارع ورقم المبنى", "الدور والشقة", "علامة مميزة (اختياري)".
5. Label chips: "المنزل", "العمل", "آخر".
6. "حفظ العنوان" button, 56px.
7. "عناويني المحفوظة" list of cards: label, address, "افتراضي" badge, edit and delete icons.

States:
- Outside the service area: a gold-container card "الخدمة غير متاحة في منطقتك بعد" with an optional empty phone field and a button "أبلغني عند توفرها". Saving is disabled.
- No saved addresses: simple line illustration and "لم تُضف أي عنوان بعد".
- Location permission denied: "فعّل الموقع أو أدخل العنوان يدوياً".
- Validation: "هذا الحقل مطلوب" in red under the field.
```

### 3. Home — "المتاجر"

```
Design the Home screen for the "دليفري القبطان" app, 390×844, following design system v4. Layout inspired by the reference image without copying its identity.

Concept: a curated list of partner stores. Tapping a store opens its products divided into sections.

Elements, top to bottom:
1. Header: on the right a tappable chip "التوصيل إلى" with the selected address below it and a small chevron (opens the location screen). On the left an outline bell icon with a gold counter.
2. Wide search field "ابحث عن منتج في كل المتاجر" with a search icon (opens Search).
3. Subheading "المتاجر" in green.
4. Two-column grid of store cards (16px gap). The whole card is tappable, with no "enter" button:
   - 16px-radius square icon in a distinct color (greens, golds and warm browns only) with the store's first letter in bold white. No real logos.
   - Store name on one or two lines.
   - Badge "مفتوح" (light green) or "مغلق" (light red).
   - Secondary line "٣٠ دقيقة · رسوم ١٥ ج.م".
   Sample stores: "أسواق النيل", "هايبر الوادي", "بقالة الحي".
5. Dashed card (exception 2) with an outline "+" and "اقترح متجراً". Tapping opens a bottom sheet with empty fields "اسم المتجر" and "رابط المتجر (اختياري)" and a button "إرسال الاقتراح".
6. "اطلب مجدداً" section (only if past delivered orders exist): horizontal row of small order cards with a "إعادة الطلب" button.
7. Live order bar (only when an order is active): a fixed card above the bottom nav "قبطانك في الطريق · ١٢ دقيقة" with a chevron, opening tracking. Use the status text that matches the order stage.
8. Bottom navigation, four outline tabs from right to left: "المتاجر" (active), "طلباتي", "السلة" (with counter), "حسابي".

No welcome banner. No decorative art taking space from content.

States:
- No stores in the area: line illustration and "لا توجد متاجر متاحة في منطقتك حالياً".
- Loading: warm gray skeleton cards with opacity pulse only.
- Error: "تعذّر تحميل المتاجر" with a "إعادة المحاولة" button.
```

### 4. Global search

```
Design the Search screen for the "دليفري القبطان" app, following design system v4.

- Active search field (keyboard open) with a cancel button and the placeholder "ابحث عن منتج في كل المتاجر".
- Before typing: "عمليات البحث الأخيرة" as chips with a "مسح" action.
- Results grouped under each store name (green subheading). Each result: small image, name, size, price, and a 48px "+" button. Mark the cheapest with a badge "الأقل سعراً".
- Closed stores: result is dimmed with a "مغلق" badge.
- No results: "لا نتائج لـ«…»" and the hint "جرّب كلمة أخرى".
- Loading: skeleton. Error: "تعذّر البحث، حاول مرة أخرى".
```

### 5. Store screen

```
Design the "Store" screen for the "دليفري القبطان" app, 390×844, following design system v4. Opens when a store card is tapped.

Elements:
1. Top bar: back (arrow pointing right), store name, in-store search icon.
2. Store info card with solid cells and outline icons: "مفتوح" or "مغلق" with hours, delivery time, delivery fee, minimum order.
3. Sticky horizontal category chips: "الكل", then the store's sections (for example "الجبن", "المشروبات", "الألبان", "الخضروات", "المخبوزات"). Active chip: #0F3D2E fill with white text (dark mode: gold fill with dark text).
4. Consecutive sections: green section title and a two-column product grid.
5. Product card: 16px-radius image (line placeholder), name, size, price "١٢٫٥٠ ج.م", and a 48px circular "+" button. After adding, the button becomes a stepper (− ١ +).
6. Floating cart bar at the bottom when this store's items are in the cart: "عرض السلة · ٣ منتجات · ١٢٠ ج.م".

States:
- Closed: banner "المتجر مغلق الآن، يفتح الساعة ٩ صباحاً" and add buttons disabled.
- Unavailable product: dimmed with a "غير متوفر" badge.
- Loading: skeleton with opacity pulse only. Error: "تعذّر فتح المتجر، حاول مرة أخرى" with "إعادة المحاولة".
```

### 6. Product details

```
Design the "Product details" screen for the "دليفري القبطان" app, 390×844, following design system v4, with a layout close to the reference image.

Top bar: back (arrow pointing right), category name, outline heart icon (favorite), cart icon with counter.

Elements, top to bottom:
1. Product image in a 20px card with solid #F6EBC4 background, 16:9, with a "متوفر" badge at the top right.
2. Name in large bold on the right, price on the left in bold ("١٨٠ ج.م", with the old price struck through if discounted), and the size or weight below in secondary text.
3. A "من: [store name]" line, tappable to return to the store.
4. Delivery strip (light green card): delivery time and delivery fee.
5. "الوصف" and "التفاصيل" with green subheadings. Show only fields that exist in the product data (description, weight, origin, shelf life). No hand-written marketing feature bullets.
6. Quantity: label "الكمية" on the right, (− ١ +) stepper on the left, 48px targets, minimum 1.
7. Small outline secondary button "اسأل الدعم عن هذا المنتج" with a generic chat-bubble icon. It opens the company support chat and is hidden when the support number is not configured. There is no phone-number input for the customer.
8. Fixed bottom bar: total on the right (price × quantity), and on the left one primary button "أضف إلى السلة", 56px. No "buy now" button.

States:
- Unavailable: badge "غير متوفر" in light red; the button is disabled and reads "غير متوفر".
- Store closed: button disabled, reads "المتجر مغلق الآن".
- Loading: skeleton. Error: "تعذّر تحميل المنتج، حاول مرة أخرى".
- After adding: bottom snackbar "تمت الإضافة إلى السلة" with a "عرض السلة" action.
```

### 7. Cart

```
Design the "Cart" screen for the "دليفري القبطان" app, 390×844, following design system v4. The cart is grouped by store, and each store is a separate order with its own fee and minimum.

Elements, top to bottom:
1. Top bar: back (arrow pointing right), title "السلة", and on the left "تفريغ السلة" in #7A5C00.
2. For each store, a grouped card:
   - Header: store icon square and name.
   - Product rows: 16px image, name and size, price "١٨٠ ج.م", a (− ١ +) stepper with 48px targets, and an outline delete icon. Swipe left to delete.
   - Empty field "أضف ملاحظة للطلب (اختياري)".
   - Summary: "المجموع الفرعي", "رسوم التوصيل", thin divider, "الإجمالي" in bold.
   - If under the minimum: a solid progress bar and "أضف ٢٠ ج.م لتصل إلى الحد الأدنى للطلب".
   - Button "إتمام طلب هذا المتجر", 56px, disabled until the minimum is reached.
3. No combined total and no global checkout button.

States:
- Empty: line illustration, "سلتك فارغة", and a "تصفح المتاجر" button.
- Item out of stock: red badge "غير متوفر" and a "إزالة" button; excluded from the total.
- Store closed: banner "المتجر مغلق الآن" and the checkout button disabled.
- After delete: snackbar "تم حذف المنتج" with "تراجع".
- Loading: skeleton with opacity pulse only.
```

### 8. Sign-in (appears only at the first checkout)

```
Design the sign-in flow for the "دليفري القبطان" app, 390×844, following design system v4. Phone-based OTP only (no passwords). It appears when the user confirms their first order, or opens "طلباتي" or "حسابي" while signed out. One unified flow for sign-in and sign-up.

Screen 1, "phone number":
- Close "×" at the top left (returns to where the user was).
- Logo (ship's wheel), title "أهلاً بك في دليفري القبطان" in green, and "أدخل رقم هاتفك لنرسل لك رمز التحقق" in secondary text.
- Empty "رقم الهاتف" field with a separate "+20" prefix box and LTR content; label above the field.
- Button "إرسال رمز التحقق", full width, 56px, disabled until the number is complete.
- Footer text: "بالمتابعة فأنت توافق على الشروط والأحكام وسياسة الخصوصية" (links in #7A5C00).

Screen 2, "verification code":
- Back, title "أدخل رمز التحقق", text "أرسلنا رمزاً من ٦ أرقام إلى رقمك" with a "تغيير الرقم" link.
- Six empty square boxes (1px border exception), auto-advance, paste support and SMS auto-fill.
- Timer "إعادة الإرسال بعد ٠٠:٤٥", then a "إعادة إرسال الرمز" link.
- Auto-submits on completion with a spinner.
- Error: "الرمز غير صحيح" in red with a light shake.

Screen 3, "your name" (new users only): title "كيف نناديك؟", empty field "الاسم الكامل", button "ابدأ".

States: too many attempts "تجاوزت عدد المحاولات، حاول بعد ١٥ دقيقة"; network failure "تعذّر الاتصال، حاول مرة أخرى"; invalid number "الرجاء إدخال رقم هاتف صحيح". After success, return the user to the screen they came from.
```

### 9. Checkout and order placed

```
Design the "Checkout" screen for the "دليفري القبطان" app, 390×844, following design system v4. It belongs to one store and is a single scrollable page.

Elements, top to bottom:
1. Top bar: back (arrow pointing right), title "إتمام الطلب", store name below in secondary text.
2. "عنوان التوصيل" card: the selected address with a "تغيير" action in #7A5C00. If missing: "حدّد عنوان التوصيل".
3. "بياناتك" card: name and phone from the account, with "تعديل".
4. "وقت التوصيل" card: "أسرع وقت (خلال ٣٠ دقيقة)" and "موعد محدد". The active option has a light green background and a check.
5. "طريقة الدفع" card: "الدفع عند الاستلام" (selected). A disabled "بطاقة بنكية" option with a "قريباً" badge. Add a note "جهّز المبلغ عند الاستلام".
6. "ملخص الطلب" card: items and quantities, subtotal, delivery fee, total in bold. An empty "كود الخصم" field with an "تطبيق" button.
7. Small line: "سيؤكد فريقنا طلبك خلال دقائق".
8. Fixed bottom bar: total on the right, and on the left the button "تأكيد الطلب", 56px.

Behavior: if signed out, open the sign-in flow first, then return here.

Order placed screen: green circle with an outline check, "تم استلام طلبك", the order number, and the text "سنبدأ التجهيز فور التأكيد". Buttons: "تتبع الطلب" and a text button "العودة إلى المتاجر".

States:
- Missing address: "حدّد عنوان التوصيل أولاً".
- Below minimum: "الحد الأدنى للطلب من هذا المتجر ٥٠ ج.م".
- Store closed: "المتجر مغلق الآن".
- Invalid promo code: "كود الخصم غير صالح".
- Loading: the button shows a spinner with "جارٍ تأكيد الطلب".
- Failure: "تعذّر إتمام الطلب، حاول مرة أخرى" with a "إعادة المحاولة" button.
```

### 10. Live order tracking

```
Design the "Order tracking" screen for the "دليفري القبطان" app, 390×844, following design system v4.

Elements, top to bottom:
1. Top bar: back (arrow pointing right), title "تتبع الطلب", order number in secondary text.
2. Prominent ETA card: "الوصول المتوقع خلال ١٨ دقيقة" in large bold green, and "يصل بين ٦:٤٠ و٦:٥٥" below.
3. Live map area (about one third of the screen): flat solid shapes (roads and blocks, no gradients), a destination pin and an outline scooter icon for the captain on the route. No real maps or logos.
4. Order stages (vertical timeline, outline icons, solid connector line):
   - "تم استلام الطلب"
   - "المتجر يجهّز طلبك"
   - "قبطانك في الطريق إليك"
   - "تم التسليم"
   Completed: green circle with a check. Current: gold circle with an opacity pulse. Upcoming: gray. Time beside each stage.
5. "قبطانك" card (from stage 3): circle with the first letter of his name (no real photos), name and vehicle type, and round outline "اتصال" and "الدعم" buttons with 48px targets.
6. Outline button "تواصل مع الدعم" (hidden if the support number is not configured).
7. Collapsible "تفاصيل الطلب" card: items and quantities, address, payment method, total.
8. Text button "إلغاء الطلب" in red, shown only up to the preparation stage, with a confirmation dialog "هل تريد إلغاء الطلب؟".

States:
- After delivery: "تم تسليم طلبك", five outline stars, optional empty comment field, and a "إرسال التقييم" button.
- Delay: light gold badge "تأخر الطلب قليلاً، نعتذر عن ذلك".
- Cancelled: "تم إلغاء الطلب" with a "إعادة الطلب" button.
- Connection lost: "تعذّر تحديث الموقع" with "إعادة المحاولة".
- Loading: skeleton with opacity pulse only.
```

### 11. My orders

```
Design the "My orders" screen for the "دليفري القبطان" app, 390×844, following design system v4. It is a main tab in the bottom navigation.

Elements, top to bottom:
1. Title "طلباتي" on the right and an outline search icon on the left.
2. Two solid pill tabs: "الحالية" and "السابقة". Active: #0F3D2E with white text (dark: gold with dark text).
3. Order card:
   - Right: store icon in a light green square, store name in bold, then "طلب رقم ٢٤١٠" and "١٤ أكتوبر، ٦:١٢ م".
   - Left: status badge: "قيد المراجعة" and "قيد التجهيز" (light gold), "في الطريق" (green), "تم التسليم" (light green), "ملغي" (light red).
   - Product summary line "جبنة رومي × ٢، عصير برتقال × ١" with "+٢ منتجات أخرى" if longer.
   - Thin divider, then "الإجمالي ٣٩٥ ج.م".
   - Action by status: "تتبع الطلب" for current orders, outline "إعادة الطلب" for delivered ones, and a #7A5C00 link "قيّم الطلب" for delivered and unrated orders.
4. Tapping a card opens order details: items with prices, address, payment, financial summary, status timeline, and a "إعادة الطلب" button.
5. Past orders grouped under subheadings "هذا الشهر" and "الشهر الماضي".
6. Bottom navigation with "طلباتي" active.

States:
- Signed out: "سجّل الدخول لمتابعة طلباتك" with a "تسجيل الدخول" button.
- No current orders: line illustration, "لا توجد طلبات حالية", and a "تصفح المتاجر" button. No past orders: "لم تُجرِ أي طلب بعد".
- Reorder: "تمت إضافة المنتجات إلى السلة", and if an item is unavailable: "بعض المنتجات غير متوفرة حالياً".
- Loading: skeleton. Error: "تعذّر تحميل الطلبات" with "إعادة المحاولة".
```

### 12. Notifications

```
Design the "Notifications" screen for the "دليفري القبطان" app, 390×844, following design system v4. No tabs.

Elements:
1. Top bar: back (arrow pointing right), title "الإشعارات", and on the left "تحديد الكل كمقروء" in #7A5C00.
2. Groups with subheadings: "اليوم", "أمس", "هذا الأسبوع".
3. Notification card: outline icon in a light green circle on the right, bold title, text up to two lines, and small secondary time on the left. Unread: small gold dot and a white background. Read: calmer background, no dot.
4. Sample items: "تم استلام طلبك", "قبطانك في الطريق إليك", "تم تسليم طلبك، قيّم تجربتك", "تأخر الطلب قليلاً، نعتذر عن ذلك".
5. Tapping an order notification opens "Order tracking". Swipe left deletes, with the snackbar "تم حذف الإشعار" and "تراجع".

States:
- Empty: line illustration and "لا توجد إشعارات حتى الآن".
- First-time permission card: "فعّل الإشعارات لتتابع طلبك" with a "تفعيل" button and a text button "لاحقاً".
- Loading: skeleton. Error: "تعذّر تحميل الإشعارات" with "إعادة المحاولة".
```

### 13. Account

```
Design the "Account" screen for the "دليفري القبطان" app, 390×844, following design system v4.

Elements, top to bottom:
1. Title "حسابي" on the right.
2. Profile card: 72px circle with the first letter of the name (no photos), name, phone number (LTR), and an outline "تعديل" button on the left.
3. Grouped list card, each row with an outline icon in a light green square on the right, the label, and a small chevron pointing left:
   - "بياناتي الشخصية"
   - "عناويني المحفوظة"
   - "المفضلة"
   - "طرق الدفع" with a "قريباً" badge
   - "الإشعارات" with a toggle
4. Support card (shown only if the support number is configured): "تواصل معنا" with two outline buttons "مراسلة الدعم" and "اتصال".
5. Second card: "المساعدة", "الشروط والأحكام", "سياسة الخصوصية", "عن التطبيق" with the version number.
6. Full-width outline red button "تسجيل الخروج" and a small text link "حذف الحساب".
7. Bottom navigation with "حسابي" active.

No stats strip. Light and dark appearance follows the system automatically, with no in-app toggle.

Sub-screens: "تعديل البيانات" (name, phone, save button "حفظ التعديلات"), "عناويني المحفوظة" (same design as the location screen), "المفضلة" (two-column product grid).

States:
- Signed out: card "سجّل الدخول لمتابعة طلباتك وإدارة بياناتك" with a "تسجيل الدخول" button.
- Logout confirmation: "هل تريد تسجيل الخروج؟" with "خروج" and "إلغاء".
- Delete account: red warning dialog "سيتم حذف حسابك وجميع بياناتك نهائياً" requiring the word "حذف" to be typed.
- Save success: snackbar "تم حفظ التعديلات".
```

---

## 5. Company-side prompts (required: without these there is no delivery business)

### 14. Captain app (the company's riders)

```
Design the "Captain app" (تطبيق القبطان) for the delivery company's riders, 390×844 mobile, following design system v4 (RTL, same colors, same rules; Arabic copy). Riders use it outdoors, so use large touch targets and high contrast.

Screens:
1. Sign-in: phone number then OTP (same pattern as the customer sign-in), with an "أدخل رمز الدعوة" first-time step if needed.
2. Home:
   - Header: greeting with the name, and a large online/offline toggle "متصل" / "غير متصل".
   - Today cards: "عدد التوصيلات", "الأرباح", and "مبلغ عندك للتسليم للشركة" (cash balance) in gold-container cards.
   - When offline: "أنت غير متصل، فعّل الاتصال لاستقبال الطلبات".
3. Incoming order (full-screen card with a 30-second countdown ring): store name and pickup distance, delivery distance, delivery fee earned, cash to collect, and two buttons: "قبول" (primary 56px) and "رفض".
4. Active delivery, a stepper with one primary button per step:
   - Step 1 "الذهاب إلى المتجر": store name, address, "فتح الخريطة" and "اتصال بالمتجر" buttons, then the button "وصلت إلى المتجر".
   - Step 2 "استلام الطلب": checklist of items to confirm, then "تم الاستلام من المتجر".
   - Step 3 "الذهاب إلى العميل": customer name, address with floor and notes, "فتح الخريطة" and "اتصال بالعميل", then "وصلت إلى العميل".
   - Step 4 "التسليم": amount to collect in large type, confirm "تم تحصيل المبلغ"، and the button "تم التسليم". A "تعذّر التسليم" option opens reasons (العميل لا يرد، عنوان خاطئ، رفض الاستلام).
5. History and earnings: day and week tabs, list of completed deliveries with fee and cash collected, and the cash balance with the note "سلّم المبلغ للشركة" (no payment feature in phase 1).

States: new order sound and banner when the app is in the background, lost connection banner "لا يوجد اتصال"، and a confirmation dialog before rejecting an order.
```

### 15. Dispatch dashboard (web, for company staff)

```
Design the company "Dispatch dashboard" (لوحة التشغيل), web, 1440 wide, RTL, following design system v4 tokens (same colors, no gradients, no emoji, outline icons, 8px spacing, light and dark). Arabic copy. Density is higher than the mobile apps, but keep 13px minimum text and clear contrast.

Layout: right-hand sidebar with sections "الطلبات", "الخريطة", "المتاجر", "القباطنة", "المناطق والرسوم", "العملاء والعروض", "التقارير", and a top bar with search, a notification bell, and the staff member's name.

Pages:
1. Orders board (default): five columns "قيد المراجعة", "قيد التجهيز", "في الطريق", "تم التسليم", "ملغي". Order cards show number, store, area, total, age timer, and a late indicator in gold. Clicking a card opens a side drawer: customer details, items, address, payment, status timeline, the buttons "تأكيد الطلب" and "تعيين قبطان" (list of online captains with distance and active orders), "اتصال بالعميل", "اتصال بالمتجر", "تغيير الحالة", and "إلغاء الطلب" (with a required reason).
2. Live map: online captains and open orders as flat markers, filters by status, and click-to-assign.
3. Stores: only the owner role can add, edit or delete stores and catalogs; dispatchers see the list read-only and can only toggle open/closed. Customers cannot add stores anywhere in the customer app. Table with name, status, hours, commission %, minimum order, prep time, and an open/closed toggle. "إضافة متجر" form (owner only): name, address, site link, ops phone or WhatsApp (staff-only, never shown to customers), hours, commission %, minimum order, prep time. Catalog tab: "استيراد من الموقع" (with detection states: success, not importable → manual) or manual entry of sections and products (name, price, size, image, availability toggle).
4. Captains: table with name, phone, status, deliveries today, and cash balance; "إضافة قبطان", and a "تسوية الحساب" action that zeroes the cash balance after remittance.
5. Zones and fees: map with drawable service zones, delivery fee per zone, free-delivery threshold, and estimated delivery time per zone.
6. Customers and offers: customer list with order counts and total spend, ratings and comments, and promo codes (code, discount, expiry, usage limit).
7. Reports: date range, orders count, revenue (delivery fees plus commissions), average delivery time, cancellation reasons, top stores, and a cash reconciliation table by captain. Export to CSV.

States: empty lists with line illustrations, a new-order sound and highlight on the board, validation messages in red, confirmation dialogs for destructive actions, and role-based access (owner, dispatcher) shown as a "الصلاحيات" setting.
```

---

## 6. Build order and checklist

**Build order:** design system, Home, Store, Product details, Cart, Location, Sign-in, Checkout, Tracking, My orders, Account, Search, Notifications, Splash, then the Dispatch dashboard and Captain app (these two must be built in parallel with the customer app, since tracking depends on them).

**Checklist before handing over:**
- [ ] Primary text is `#111111` in light mode and `#F3EFE6` in dark mode.
- [ ] Gold text on light backgrounds is always `#7A5C00`.
- [ ] Primary buttons in dark mode are gold.
- [ ] No gradients, no emoji, no third-party logos.
- [ ] Borders only in the three registered exceptions.
- [ ] Eastern Arabic digits for display, Latin digits in inputs.
- [ ] "قبطان" appears only as the company's own rider; stores are "المتاجر".
- [ ] The support number is an empty config value; all support buttons are hidden while it is empty.
- [ ] Only the owner role can add or edit stores, catalogs, fees, zones and hours, and only in the dashboard. Customers cannot add stores; the "اقترح متجراً" card only sends a suggestion to the dashboard (remove it if you want no customer input at all).
- [ ] The customer app, captain app and dashboard are all delivered.
- [ ] All touch targets are at least 48px and the smallest text is 13px.

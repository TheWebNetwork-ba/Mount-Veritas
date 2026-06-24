# Mount Veritas — Agent Handoff Document
**Last updated by:** Claude Sonnet 4.6  
**Repo:** `TheWebNetwork-ba/Mount-veritas` (main branch)  
**Live store:** getvossa.com | Admin: mwbhpe-1b.myshopify.com  
**Storefront password:** `veritas-drop-2026`

---

## 1. WHO YOU'RE WORKING WITH

**G** (also goes by Lucca) is operations co-founder of Mount Veritas. He owns the storefront, fulfillment, suppliers, and production. His co-founder **Vitto Pessanha** (CEO) owns strategy, marketing, and finance. G is non-technical and visual-first — all code goes through Claude. Major decisions route through Vitto.

### How G works (strict — follow this)
- **One decision per turn.** Never present multiple decisions at once.
- **Visual-first.** Show an on-brand preview before building anything new.
- **Single-select options** with a starred recommendation and one-line reason.
- **Map structure first, then build section by section.** Draft → review → correct → finalize.
- **Short and direct.** No verbose explanations, no filler, no "corny" language.
- **Push back is expected.** When something doesn't work, G will say so and expect fast course correction — own mistakes without over-apologizing.
- **Code delivery:** Always deliver the full updated file, never just a snippet.
- **Phased builds.** One phase confirmed before the next begins.

### Frameworks G references
- **Hormozi** — business structure, offers, operating systems
- **Kennedy** — direct response, messaging, copywriting
- **Brunson** — funnels, value ladders
- **Ralston** — personal brand

---

## 2. BRAND SYSTEM (LOCKED — NEVER DEVIATE)

### Identity
- **Name:** Mount Veritas (abbreviated MV)
- **Website:** getvossa.com (brand domain) / Shopify handle: mwbhpe-1b.myshopify.com
- **Tagline / positioning:** "The uniform of the climb"
- **Core slogans:** "SEE IT. BELIEVE IT. OBTAIN IT." and "MADE IN IMAGINATION."
- **Target customer:** The "believer-builder" — 18–30, faith + abundance mindset, wears OVO/Essentials/Fear of God, buys clothing as a physical declaration of who they're becoming

### Brand personality
- **Sage leads** (grounded truth, never preachy)
- **Hero drives** (the climb, the step, the action)
- **Magician underlies** (quiet becoming)
- **Energy:** Nike-coded — bold, cinematic, kinetic. Never passive or zen-coded
- **Voice:** Low-key, high-quality, authoritative. Quiet luxury in the style of Aimé Leon Dore and OVO. No hype, no exclamation marks, fewer words carrying more weight

### Design tokens (CSS variables — these are the only correct values)
```css
--black:     #0d0d0b   /* primary background */
--smoke:     #ECE9E2   /* primary text / light elements */
--smoke-dim: #9b988f   /* secondary text / muted */
--gold:      #ffb800   /* small accents only — never dominant */
--radius:    6px       /* unified border radius */
```

### Typography
- **Abril Fatface** — hero titles ONLY
- **Fira Sans Condensed** — everything else (body, labels, buttons, nav)

### Copy rules
- All copy in sentence case (NOT title case)
- No exclamation marks
- No hype language
- Fewer words = more power

### Brand rules (non-negotiable)
- **No discounts** — incentive is always early access. The ONLY exception is the `BASECAMP` code (10% off first order, currently active in Shopify).
- **Scarcity must be honest** — momentum/identity urgency for permanent pieces; real stock/time scarcity for seasonal only.
- **Premium voice, never desperate.**

---

## 3. THE ECOSYSTEM (BIGGER PICTURE)

Mount Veritas is **Phase 1** — the physical expression of the brand.

- **Phase 1 (NOW):** Mount Veritas — premium faith-based streetwear. Launch collection "Base Camp." Storefront live at getvossa.com.
- **Phase 2 (NEXT):** The Web Network — a real-life multiplayer game where members climb a shared mountain across four life domains: Health, Wealth, Love, Happiness. Includes an internal AI guide called **Sherpa** (also called Jarvis).
- **Phase 3 (FUTURE):** Summits, in-person events, and scale. Content engine runs across all phases.

The overarching master brand is **The Web Network**. MV is the physical gateway into it.

---

## 4. STORE INFRASTRUCTURE

### Shopify
- **Store URL:** getvossa.com / mwbhpe-1b.myshopify.com
- **Plan:** Basic (important constraint — see Section 6)
- **Theme:** Custom lean theme, built from Dawn 15.4.1, heavily customized
- **Live theme ID:** `gid://shopify/OnlineStoreTheme/160338444539`
- **Customer accounts:** **New customer accounts** are active at `account.getvossa.com` — this disables classic `/account/login` and the `create_customer` Liquid form. Password-based auth does not work natively.

### GitHub (source of truth for all theme code)
- **Repo:** `TheWebNetwork-ba/Mount-veritas`
- **Branch:** `main`
- **Sync:** The repo is directly connected to the live Shopify theme — pushes to main deploy automatically
- **How to push code:** Use GitHub REST API directly via bash:
  - GET the file first to get the current `sha`
  - PUT with new base64-encoded content + sha
  - Endpoint: `https://api.github.com/repos/TheWebNetwork-ba/Mount-veritas/contents/{path}`
  - Auth header: `Authorization: Bearer {PAT}`
- **PAT:** Ask G for a fresh PAT at the start of every new session. Previous PAT should be revoked by G.
- **NEVER zip upload** — that wipes all Customize settings (connected products, images, text blocks). Always push via API.

### Email
- **Current sender:** getvossa@gmail.com (needs custom domain email configured after domain swap)
- **Platform:** Shopify native stack — Shopify Flow (tagging brain) + Shopify Email / Messaging / Marketing Automations (senders)
- **Klaviyo:** Uninstalled, parked as future upgrade for branching logic at scale

### Affiliate app
- **BixGrow** is installed
- **Portal URL:** `https://Mountveritas.bixgrow.com` (login and register)
- BixGrow has NO public API for programmatic affiliate creation — no workaround exists
- BixGrow handles its own email automations (welcome, approval, denial, referral) — no Shopify Flow needed for these

---

## 5. COMPLETE THEME FILE MAP

Every file in the repo and what it does:

### layout/
| File | Purpose |
|------|---------|
| `theme.liquid` | Master layout — nav, footer, cart drawer HTML, early access upsell, package protection upsell, payment icons, discount code field, redirect handlers |

### assets/
| File | Purpose |
|------|---------|
| `mv-styles.css` | All CSS — brand tokens, layout, nav, footer, PDP, cart, accordions, pair product, affiliate pages, account pages |
| `mv-script.js` | All JS — product row carousel, PDP variant picker, qty selector, accordion toggle, size chart drawer, zoom, cart drawer open/close/render, upsell show/hide, mvCuAdd (add to cart from card), discount code field |

### sections/
| File | Purpose |
|------|---------|
| `mv-home.liquid` | Homepage — hero, "Most Worn" product row (horizontal scroll), Mountain collection grid, brand statement |
| `mv-product.liquid` | Full PDP — image gallery + thumbnails, variant chips, qty, add to cart, payment button, accordion blocks (Details/Shipping/Size & Fit), pair product, size chart drawer, zoom |
| `mv-cart.liquid` | Cart PAGE (not drawer) — mirrors drawer with upsells + payment icons |
| `mv-affiliate.liquid` | Affiliate landing page — two CTA buttons to BixGrow portal |
| `mv-affiliate-register.liquid` | Custom affiliate registration form (routes to BixGrow, NOT Shopify) |
| `mv-account-login.liquid` | Branded sign-in page (blocked by new accounts — see Section 6) |
| `mv-account-register.liquid` | Branded register page (blocked by new accounts — see Section 6) |
| `mv-collection.liquid` | Collection grid |
| `mv-faq.liquid` | FAQ section rendered below product on PDP |
| `mv-password.liquid` | Waitlist gate page with email capture form |
| `mv-popup.liquid` | Popup section (stub — not used yet) |

### templates/
| File | Purpose |
|------|---------|
| `index.json` | Homepage — renders `mv-home` section |
| `product.json` | Product page — renders `mv-product` (main) with 3 accordion blocks (Details/Shipping/Size & Fit) + `mv-faq` below with 3 FAQ items |
| `cart.liquid` | Cart page — `{% section 'mv-cart' %}` |
| `collection.json` | Collection page — renders `mv-collection` |
| `404.liquid` | Custom branded 404 |
| `password.json` | Storefront password page — renders `mv-password` |
| `page.liquid` | Default page template |
| `page.my-account.liquid` | Customer dashboard (blocked — see Section 6) |
| `page.account-login.liquid` | Branded login (blocked — see Section 6) |
| `page.account-register.liquid` | Branded register (blocked — see Section 6) |
| `page.affiliate.liquid` | Affiliate landing — `{% section 'mv-affiliate' %}` |
| `page.affiliate-gate.liquid` | Tag-check redirect page with `{% layout none %}` |
| `page.affiliate-dashboard.liquid` | Blank dashboard shell (placeholder) |
| `page.affiliate-register.liquid` | Affiliate registration form |
| `customers/` | Shopify native account templates |

### config/
| File | Purpose |
|------|---------|
| `settings_schema.json` | Theme settings — includes Cart group: early access upsell product picker (cart_ea_product, cart_ea_label), package protection product picker (cart_pp_product), footer affiliate URL |

### Shopify Pages (page record + template file must both exist)
| Handle | Template suffix | Purpose |
|--------|----------------|---------|
| `affiliate` | `affiliate` | BixGrow portal landing |
| `affiliate-gate` | `affiliate-gate` | Server-side tag check |
| `affiliate-dashboard` | `affiliate-dashboard` | Placeholder dashboard |
| `affiliate-register` | `affiliate-register` | Affiliate registration form |
| `my-account` | `my-account` | Customer dashboard (blocked) |
| `account-login` | `account-login` | Sign in (blocked) |
| `account-register` | `account-register` | Register (blocked) |

---

## 6. KNOWN PLATFORM CONSTRAINTS

These are hard limits — do not try to work around them without understanding the implications:

1. **New customer accounts** — Shopify's new account system (active at `account.getvossa.com`) disables the classic `create_customer` Liquid form and password-based auth entirely. Any registration flow that depends on native Shopify account creation will fail. The custom account pages exist in the repo but are functionally blocked until this is resolved.

2. **Basic plan checkout** — The Basic plan does not allow checkout customization (no custom Liquid, no checkout extensions). Branding via Checkout settings UI only (logo, colors). No code access to checkout.

3. **Shopify Flow + embedded apps** — Flow and the Messaging app editors block automated browser clicks. They CANNOT be operated by a browser agent. All automation builds must be done manually by G with step-by-step instructions written by the agent.

4. **BixGrow has no public API** — Cannot programmatically create affiliates, approve them, or sync them to Shopify customer tags. Everything goes through the BixGrow portal UI.

5. **`storefrontAccessTokenCreate` mutation** — Blocked by the Shopify MCP tool for security. Use bash + curl to GitHub REST API as fallback for file operations.

6. **GitHub 100-file upload cap** — If uploading many assets at once (e.g. 188 asset files), split into two commits of ~94 files each. Each folder must be named exactly `assets` so GitHub merges additively.

7. **`return_to` redirect after account creation** — Shopify's `return_to` param is ignored in practice for new accounts. Client-side workarounds (sessionStorage flag + theme.liquid detection) are needed.

8. **Spam protection is OFF** — Was turned off to fix captcha on the waitlist form. Keep it off.

9. **Zip uploads create a fresh theme** and wipe all customizer-connected products, images, and text. Direct GitHub pushes via REST API is the ONLY correct workflow.

---

## 7. WHAT'S BEEN BUILT (COMPLETED)

### Storefront
- [x] Full custom theme built from Dawn 15.4.1 — all native Dawn code stripped, replaced with MV-branded components
- [x] Storefront password page with waitlist email capture (`contact[tags]=waitlist`)
- [x] Homepage with hero, "Most Worn" horizontal product row (carousel + touch swipe), Mountain collection grid, brand statement
- [x] Product page — gallery, thumbnails, variant chips, qty, add to cart, buy it now, accordions (Details/Shipping/Size & Fit), pair product add-on, size chart drawer, zoom
- [x] Cart drawer — line items, subtotal, early access upsell card, package protection row, payment icons (8 providers), discount code field
- [x] Discount code — applies via `/discount/{code}?redirect=/checkout` (Shopify's native redemption URL, guaranteed to work)
- [x] Cart page mirrors drawer
- [x] Custom branded 404 page
- [x] Collection page

### Affiliate portal
- [x] `/pages/affiliate` — MV-branded landing with two buttons: Sign In and Join (both route to BixGrow)
- [x] BixGrow portal customized (dark theme, gold accents, MV copy) — signup, login, thank-you, dashboard pages
- [x] "Affiliates" customer segment: `customer_tags CONTAINS 'affiliate'`
- [x] `/pages/affiliate-gate` — invisible tag-check page
- [x] `/pages/affiliate-dashboard` — placeholder (blank white shell)
- [x] Decision locked: affiliate registration goes through BixGrow's native portal, not a custom Shopify form

### Cart upsells (connect via Customize → Theme settings → Cart)
- [x] Early access upsell card — hides if product already in cart
- [x] Package protection row — hides if already in cart

### Product metafield definitions (created in Shopify)
- [x] `custom.pair_product` (type: `product_reference`) — set per product to show "Make it a Pair" add-on
- [x] `custom.size_chart` (type: `file_reference`) — set per product to show size chart in drawer

### Discount
- [x] `BASECAMP` — 10% off first order, active in Shopify

### Email automations (foundations only)
- [x] Customer tags `ea-paid` and `ea-optin` created
- [x] Flow A active: customer-created → tag
- [x] Flow B active: order with early-access → tag
- [x] Early Access product exists (ID: `9348324262139`, Draft, $0.00 — price not yet set, needed before launch)
- [x] 28-automation lifecycle plan complete as a document

---

## 8. WHAT'S PENDING (PRIORITIZED)

### Pre-launch blockers

**1. Set price on Early Access product**
- Shopify Admin → Products → "Early Access" → set the price
- Product ID: `9348324262139`
- Keep as Draft until launch day
- This gates the entire email automation system

**2. Lock BC1TH colorways**
- Black + Bone (warm off-white) are nearly confirmed — one decision away from final lock
- Bone = warm off-white (not pure white, not cream)
- Once locked, the manufacturer spec sheet is ready to go out

**3. Lock branding/artwork placement method on garments**
- Embroidery vs screen print vs woven labels — decision pending with Vitto

**4. Manufacturer search (Turkey + Portugal)**
- Primary: Turkey | Secondary: Portugal
- Pakistan (Nofal Apparel) confirmed NOT viable on cost — thread on hold, do not restart
- Outreach emails always go under Vitto Pessanha's name, brand-neutral, never referencing G

### Customize connections (G does in browser — agent writes instructions)

**5. Connect "Most Worn" products on homepage**
- Shopify Customize → Homepage → "Most Worn" section → add real products

**6. Connect Mountain collection cards on homepage**
- Customize → Homepage → Mountain section → assign collections

**7. Connect Early Access upsell in cart**
- Customize → Theme settings → Cart → "Early access upsell product"

**8. Connect Package Protection product in cart**
- Customize → Theme settings → Cart → "Package protection product"

**9. Set pair_product metafield per product**
- Products → (open product) → Metafields → Pair product → select the paired item
- Without this, "Make it a Pair" section doesn't render (it's data-driven, not code)

### Pages — still need to be created

**10. Create three blank pages**
- Contact us (`/pages/contact-us`)
- Client services (`/pages/client-services`)
- Legal notices (`/pages/legal-notices`)

### Email & automations

**11. Build automation sequences**
- G builds manually in Shopify Flow editor; agent writes step-by-step instructions
- Priority order: Waitlist welcome → Drop announcement → Checkout abandonment (7-message series)
- Existing Flows A and B have off-brand placeholder copy — needs replacing

**12. Configure custom domain email sender**
- After domain swap: Shopify → Settings → Notifications → configure custom sender

**13. Add SMS channel**
- Layer in after email is stable (Shopify native or Postscript)

### Account system (blocked — resolve constraint first)

**14. Resolve new customer accounts blocker**
Two proposed paths, still unresolved:
- **Path A (simpler):** Use Shopify's new accounts portal with a redirect flow — sessionStorage flag to detect post-login redirect in theme.liquid
- **Path B (more powerful):** Fully custom code-based access system, no Shopify auth dependency — token-based, stored in customer metafields. Better for Phase 2 Web Network memberships.

**15. Build affiliate dashboard content**
- Currently blank white shell
- Needs: referral link display, commission stats, tier status, copy button
- Wait until account system is resolved

---

## 9. FULL AUTOMATION PLAN (18 AUTOMATIONS)

All on native Shopify stack. Manual build by G with step-by-step instructions from agent.

| # | Name | Trigger | Condition | Action |
|---|------|---------|-----------|--------|
| 1 | Waitlist welcome | Customer created | tag = `waitlist` | Email: "You're on the list" |
| 2 | Drop announcement | Manual trigger | tag = `waitlist` | Email: announce the drop |
| 3 | Early access grant | Order paid | product = EA product | Tag `ea-paid`; email: "Access granted" |
| 4 | Order confirmation | Order paid | any | Email: order confirmed |
| 5 | Shipping notification | Fulfillment created | any | Email: your order is moving |
| 6 | Delivery confirmation | Fulfillment delivered | any | Email: it arrived |
| 7 | Post-purchase follow-up | 7 days after delivery | any | Email: how are you wearing it |
| 8 | Review request | TBD days after delivery | any | Email: leave a review (timing TBD with G) |
| 9 | Checkout abandonment M1 | 15 min after abandonment | any | Email: you left something |
| 10 | Checkout abandonment M2 | 1 hr | any | Email: still thinking |
| 11 | Checkout abandonment M3 | 1 day | any | Email: last chance copy |
| 12 | Checkout abandonment M4 | 2 days | any | Email |
| 13 | Checkout abandonment M5 | 3 days | any | Email |
| 14 | Checkout abandonment M6 | 4 days | any | Email |
| 15 | Checkout abandonment M7 | 7 days | any | Email: final message |
| 16 | Win-back | Every 30 days, no purchase | tag != ea-paid | Email: we haven't seen you |
| 17 | VIP grant | 15-20 orders | any | Tag `vip`; email: store credit for 1 shirt |
| 18 | Elite grant | 30+ orders | tag = `vip` | Tag `vip-elite`; email: early drop access |

5 automations require an app or onsite tracking (not yet selected):
- Browse abandonment x2
- Back-in-stock notification
- Delivery status triggers x2

---

## 10. LAUNCH COLLECTION — PRODUCT SPECS

### Base Camp — 4 pieces in 2 sets

| Code | Piece | Set |
|------|-------|-----|
| BC1TL | Tee | Set 01 Light |
| BC1SL | Short | Set 01 Light |
| BC2HH | Hoodie | Set 02 Heavy |
| BC2PH | Pants | Set 02 Heavy |

### Model code anatomy: `[collection][set][garment][weight]`
- Collection: BC (Base Camp) / TC / AS / SU
- Garment: T (tee) / S (short) / H (hoodie) / P (pants)
- Weight: L (lightweight) / H (heavyweight)
- NOTE: L in model code = lightweight. L in size chart = Large. Two separate systems, no conflict.

### BC1TH spec (locked, quote-ready)
- 100% combed ring-spun cotton, 250 gsm
- Soft enzyme / garment wash finish
- Boxy fit
- **Drop shoulder construction (NOT set-in sleeve — non-negotiable)**
- Side-seamed body, double-needle hems, ribbed crew neck with back-neck tape
- Colorways: Black + Bone (warm off-white) — one decision from lock

---

## 11. PHYSICAL BRAND ELEMENTS (ALL PENDING — PRE-SHIPMENT)

- [ ] Serialized member number system (every customer gets a unique number — coexists with model code on tag)
- [ ] Metal membership card or framable certificate
- [ ] Unboxing ceremony: wax seal, printed tissue, signature scent, designed box interior
- [ ] Creed/verse inside collar
- [ ] Numbered/letterpress hangtags
- [ ] Debossed leather patches

---

## 12. CANVA ASSET LIBRARY

| File | Canva ID | Contents |
|------|----------|---------|
| Main brand project | `DAGLQ-Im3Eg` | 106 pages — all brand assets |
| Website build | `DAG_1F3E03Y` | 420 pages — full site mockup |
| Logos | `DAGcTTFxjO0` | Logo variations |
| TWN/MV logos | `DAG0bSrr11k` | The Web Network + MV combined logos |

Search broad first to map the library, then targeted to confirm specific files.

---

## 13. CONNECTED TOOLS (MCP AVAILABLE)

- Shopify MCP — storefront, products, discounts, pages, flows, segments
- GitHub REST API (via bash) — all theme file reads and writes
- Canva MCP — brand asset creation and editing
- Figma — "Mount Veritas — Brand Parts Inventory" file in G's workspace
- Google Drive — brand docs (had auth issues in earlier sessions — verify before use)
- Slack — comms
- Higgsfield — video generation
- n8n — automation workflows (connected, not yet used for MV)

---

## 14. SUPPLIER STATUS

| Supplier | Region | Status |
|---------|--------|--------|
| Nofal Apparel | Pakistan | ON HOLD — not viable, do not restart |
| TBD | Turkey | Primary target |
| TBD | Portugal | Secondary target |

Outreach always under Vitto Pessanha's name. Brand-neutral. Never reference G.

---

## 15. QUICK REFERENCE — SHOPIFY IDs

| Item | ID |
|------|-----|
| Store | mwbhpe-1b.myshopify.com |
| Live theme | gid://shopify/OnlineStoreTheme/160338444539 |
| Early Access product | gid://shopify/Product/9348324262139 |
| Discount: BASECAMP | gid://shopify/DiscountCodeNode/1817054085371 |
| Metafield: pair_product | gid://shopify/MetafieldDefinition/190100472059 |
| Metafield: size_chart | gid://shopify/MetafieldDefinition/190100373755 |
| Segment: Affiliates | customer_tags CONTAINS 'affiliate' |

### Customer tags in use
`waitlist` / `ea-paid` / `ea-optin` / `affiliate` / `vip` / `vip-elite`

---

## 16. WHAT TO DO FIRST IN A NEW SESSION

1. Ask G for a fresh GitHub PAT (previous one should be revoked)
2. Read this file and the full repo structure before touching anything
3. Ask G ONE question: what's the priority today?
4. Do not batch decisions — one at a time, always

---

*End of handoff. Read this top to bottom before doing anything. Do not ask G to repeat context that is documented here.*

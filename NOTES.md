# NOTES

Status: final state after the two accessibility fixes (Prompt 13). The full QA suite was re-run on these exact files in Chromium only; section 4 lists what was run, what was not, and the limitations that remain. Seven product images and the hero are crops of an AI-generated reference image; `p108.webp` was edited from the existing reference image, with a sixth tin added as a purple recolour (section 3), so it is not a fresh AI render. The exact prompt for the reference image was not retained: it is marked **UNAVAILABLE** in `PROMPTS.md` (Prompt 5) and is not reconstructed.

## 1. What I changed
- **Bugs (root causes):** prices come only from `PRODUCTS` (cart stores `{id, qty}`); count shows units; `+` was string concatenation; `remove` used `splice(i)` and deleted every later line; the cart click listener was re-added on every render; quick view used a stale loop index; filter/sort/search overwrote each other (now one `state` + one `view()`); sort comparators returned booleans; search had no stale-response guard (now debounced + sequence token); `indexOf` truthiness bug in search; the wishlist heart toggled every card; empty `localStorage` crashed the first visit; corrupt storage is validated and clamped; the coupon stacked and ignored cap, minimum and Gifts; shipping used the pre-discount subtotal; pincode never handled rejection and could stay on "Checking..." (now always settles, 6 s timeout); newsletter used `alert`; popup auto-opened.
- **Rules R1-R8** are in `calc()`, `add()`, `setQty()`, `view()` and the pincode handler. Only the final total is rounded. Free shipping uses the post-discount amount against the ₹599 threshold.
- **Design:** rebuilt to BRAND.md (tokens in `:root`, Fraunces + Inter in one Google Fonts link with `display=swap`, 8px spacing, one 12px radius, section order from BRAND.md section 8, FAQ accordion, inline newsletter, no looping motion, `prefers-reduced-motion` honoured).
- **UX:** toast instead of alerts, cart drawer with steppers and inline coupon messages, shipping progress bar, quick view as a native `<dialog>`, Enter applies the coupon.
- **Accessibility fixes (final pass, Prompt 13):** two small changes in `index.html`, nothing else. (1) After a category chip is activated, the chips are re-rendered, which used to drop keyboard focus to the page body; the click handler now puts focus back on the chip that was activated. (2) The footer email, phone and Instagram links are now `display:inline-block;min-height:24px`; their clickable height went from 19 px to 25.6 px (width was already over 24 px), with the same text, links and layout.
- **Technical:** removed jQuery, animate.css, Font Awesome, `marquee`, blink and `@import`. JSON-LD (OnlineStore, 8 Products, FAQPage) is generated from `PRODUCTS` and the approved FAQ text.

## 2. What the AI got wrong (me, in this work)
- I wrote a line in an earlier draft of this file about a bug that never existed. I caught it on review and deleted it.
- I assumed I could generate AI images. I had no image tool (section 3).
- Image `width`/`height` attributes stretched and cropped every product image on mobile (CSS `height` was not `auto`). Found only by looking at screenshots.
- At 360px the header wrapped badly (cart button on its own row). Found in a screenshot.
- Card prices were not aligned across cards, and filter chips fell back to a serif font. Both found in screenshots.
- Review cards were cream on cream, so they looked unframed. Screenshot.
- Every card had a primary button, which breaks the BRAND.md rule of one primary per view. I made card "Add to cart" secondary. Found by rereading BRAND.md against the screenshots.
- axe-core flagged: low-contrast success text, the announcement outside a landmark, and `role="dialog"` on `<aside>`. All fixed.
- Lighthouse flagged an aria-label that did not contain the visible "Sold out" text. Fixed.
- The title was 48 characters; BRAND.md wants 50-60. Now 54.
- Two hex colours were outside `:root`. Moved to tokens.
- Visual bugs seen in a screenshot of the open cart: the close button stretched full width, the toast covered the Checkout button, and a discount showed as ₹84.8. All fixed (toast moved to the top and dismissed when the cart opens; fractional amounts show two decimals).
- Several of my test-harness lines were wrong (a placeholder print, and Playwright calling a function I assigned). Those results are not reported.

## 3. Images
**Source:** all product, hero and logo visuals are based on one AI-generated reference image (a collage supplied by the project owner, 1536x1024). `p108.webp` was additionally edited by me afterwards (see below). The tool is stated by the owner as ChatGPT image generation; the PNG has no metadata that proves it, and I did not generate it. The exact prompt was not retained, so it is marked UNAVAILABLE and not logged (PROMPTS.md, Prompt 5).

**What I did to it (Claude):**
- **Products (p101-p107.webp):** cropped each panel (330x330 px for the seven tins), upscaled about 2.4x with an EDSR x2 super-resolution model (OpenCV `dnn_superres`, weights from a public GitHub repo), resized with Lanczos to 800x800, lightly sharpened, and saved as WebP (quality 80). 42-53 KB each. The real detail is still about 330 px, so they are soft on high-DPI screens.
- **Gift box (p108.webp):** first cropped from the reference image (374x374 px panel) and upscaled the same way as the others. It then showed five tins, so in the final fix I edited that image with OpenCV: I cut out the five tins, made them slightly narrower, re-spaced them, and added a sixth tin as a purple recolour of the green tin (so it repeats the green tin's label art). The old tin tops behind the row were covered with a flat dark shadow tone. This is a photo edit, not a fresh AI render, and no image-generation tool was used. 800x800 WebP, 59 KB.
- **Hero (hero-banner.webp):** a 650x305 window of the tea-garden scene, same upscaling, 1600x750 WebP, 85 KB. No text in the image. The page CSS shows it at 16:9 (`object-fit:cover`), which trims the sides.
- **Logo (logo.svg):** not AI-generated. I rebuilt the logo from the reference image by hand as a horizontal lockup (mountain and leaf mark, "Mistvale", "TEA CO." with rules). The text is converted to outlines from Fraunces, so it renders without a web font. Transparent background, 14 KB. The stacked layout of the original was changed to a horizontal one so it is legible at header height.
- **Code changes for the new assets:** header logo height 32px to 48px (CSS), logo width/height attributes 176x40 to 233x58, hero alt text updated. No application logic changed.

**Known problems with the images:**
- The final gift box image (p108) was edited from the existing reference image: it originally showed five tins, and I cut them out, re-spaced them and added a sixth tin as a purple recolour of the green tin (OpenCV; no image generator available). The sixth tin repeats the green tin's label art, and the area behind the tins is a flat dark fill, so detail is limited when zoomed in. It is a photo edit, not a fresh AI render.
- The tins print "NET WT. 100g" and the gift card says "A journey of fine teas". Neither comes from `PRODUCTS`.
- The earlier Pillow drawings were not AI-generated and are no longer in the project.

## 4. Final QA (re-run after the last changes, Prompt 13, on the final files)
Everything below was run against the files in this ZIP, served over local HTTP (`http://localhost`). Tools: Playwright 1.56 with headless Chromium, axe-core 4.13.0, Lighthouse 13.5.0. Nothing here was run in Firefox, WebKit, on a real phone, or on a real network.

**Layout and images (360, 768 and 1280 px):** each page was scrolled top to bottom so the lazy images load. All 10 `<img>` elements (8 products, hero, logo) loaded with no broken image at all three widths. There was no horizontal overflow at any width, and none with the cart open or the quick view open. I counted six tins in `p108.webp` by eye and looked at its product card at 1280 px (the tins are small there but clearly six).

**Search, category, sort:** 240 combinations (12 search strings, 5 categories, 4 sorts) matched an independently computed expected list. Sold-out products were last in every sort, category and search. Changing one control kept the other two.

**Stale and rapid search:** a slow earlier request did not overwrite a newer query; three fast successive queries ended on the last one; clearing the box restored all 8 products.

**Cart and sold-out products:** 12 rapid Add clicks cap at 5; triple-click on the gift box gives 3; 30 scripted `add()` calls cap at 5; the sold-out button is disabled and `add(107)` adds nothing; `+` is disabled at the limit; `-`, remove, triple-click `-`, double-click remove, empty cart (Checkout disabled), and persistence across reload.

**Coupon and shipping:** 10 UI cases checked against exact fraction arithmetic (₹399 minimum, ₹349 below minimum, the ₹150 cap, gift-only cart, gift plus tea, discount pushing the total under the free-shipping line, no coupon above and below ₹599, lower/mixed-case codes, applying twice gives identical totals), plus an invalid and an empty code. `calc()` was also compared with exact fractions on 32,768 cart/coupon combinations (7 in-stock products, quantity 0 to 3, coupon on and off) with 0 mismatches. No real cart in that set lands within ₹1 of the ₹599 line, so I tested the boundary separately by changing prices in memory inside the test browser only (no file changed): after-discount ₹599 gives free shipping, ₹598 adds ₹49, and 665.56 versus 665.5 with the coupon gives the same split; subtotals of ₹1,649 and ₹1,650 both give a ₹150 discount.

**Pincode:** 734001, 700001, 110001, 400001 and 560001 give 2, 3, 4, 4 and 5 days; 999999 is not serviceable; 12345, 000000, abcdef, empty and "12 345" show the pincode error; typing 7 digits is cut to 6; API rejections (`INVALID_PINCODE` and a generic error) end in a message; a hung API shows "Checking…" and settles after 6.1 s with the retry message and the button enabled again.

**Checkout payload:** the real form submit was intercepted (nothing was sent to the URL). It was a POST to `https://mistvale.example/cart/checkout` with `items=[{"id":104,"qty":2},{"id":108,"qty":1}]` and `coupon=WELCOME10`; a cart without a coupon sent `coupon=` empty.

**localStorage:** empty storage; corrupt JSON; five wrong types (`"str"`, `null`, `123`, `{"a":1}`, `true`); an array of junk entries; negative, float, huge, text, null, sold-out and duplicate quantities (clamped or dropped); an invalid and a valid stored coupon; a 4 MB corrupt string; a 60,000-entry array (de-duplicated to 6 lines); `getItem` throwing; `setItem` throwing (quota), where the cart kept working in memory. No page error in any case and the grid always showed 8 products.

**Keyboard and focus:** Enter on the cart button opens it and focuses Close; 18 Tab/Shift+Tab presses stayed inside the open cart; Escape closes it and returns focus to the cart button; clicking the overlay closes it; quick view opens with Enter, closes with Escape and focus returns to its button; the sold-out quick view has a disabled Add button; Enter and Space work on category chips, and focus now stays on the chip that was activated (keyboard only: Tab to the chips, then 9 Enter activations across all 5 chips and a Space press, at 360, 768 and 1280 px, with the 3px focus ring still visible and the next Tab moving on in order); the sort works from the keyboard; Enter adds to cart; the newsletter and FAQ work from the keyboard. A full Tab walk found 43 stops and every one has a visible focus style (checked by computed outline/box-shadow, plus a screenshot of one control).

**Accessibility (axe-core):** 0 violations on 12 runs (360, 768 and 1280 px; page, cart open with an item, quick view open, no-results state). axe also listed three "needs manual review" items that I did not resolve: an `aria-label` on the quantity `<span>`, the colour contrast of the "−" glyph button (non-text content), and the contrast of a quick-view paragraph (axe could not determine the background). Automated checks only; no screen reader was used. Lighthouse accessibility: 100 on both runs. I also ran axe's `target-size` rule explicitly at the three widths: 0 violations, both before and after the footer fix (axe treats links inside a line of text as exempt, so this rule did not catch the 19 px footer links; my own measurement did).

**Lighthouse 13.5.0 (headless Chromium, local HTTP, not a real device or network):** the first run was done while the functional suite was running in the background: mobile Performance 99, Accessibility 100, Best Practices 96, SEO 100 (LCP 1.8 s, CLS 0, TBT 40 ms). A second run with nothing else running: mobile 98, 100, 96, 100 (LCP 2.4 s, CLS 0, TBT 0 ms); desktop 100, 100, 96, 100 (LCP 0.6 s, CLS 0, TBT 0 ms). Mobile LCP and Performance vary from run to run (the earlier pass measured 99 and 1.8 s); I did not investigate the variation, and the two code changes do not touch images or fonts. The only console error behind the Best Practices score is the Google Fonts 403 described below.

**Schema / SEO:** I parsed the JSON-LD and checked it structurally: 1 OnlineStore, 8 Products whose name, price, INR currency and availability match `PRODUCTS`, `aggregateRating` only on the two products that have rating data, and a FAQPage whose six questions and answers are identical to the visible FAQ. No external validator (Google Rich Results, validator.schema.org) could be reached from this sandbox, so this is **not** a Google validation. Title 54 characters, description 156, one h1, canonical, 6 Open Graph and 3 Twitter tags, `lang="en"`, every `<img>` has `alt`.

**Console and network:** across every run there were no page errors, no other console errors, and no failed or 4xx/5xx requests other than the Google Fonts stylesheet.

**Google Fonts:** the site loads Fraunces and Inter from one `fonts.googleapis.com` link (`display=swap`), and I did not change it. In this sandbox that request returns HTTP 403. I checked the cause: `fonts.googleapis.com`, `fonts.gstatic.com` and `example.com` all return 403 with the header `x-deny-reason: host_not_allowed` from the sandbox's outbound allow-list, so the 403 comes from the sandbox, not from the site. Because the stylesheet could not load, every screenshot and Lighthouse run used fallback fonts. **Not verified:** that the fonts load and look right on a real network. The link follows the Google Fonts css2 format as far as I know, but I did not confirm it against the live service.

**What changed in code in this pass:** `index.html` differs from the previous submission by two lines only: one CSS rule for the footer links and one statement in the category-chip click handler. The `API` block, the `PRODUCTS` array (ids, names, prices, stock, images), the footer legal paragraph, the checkout form (id, action, POST, `items` and `coupon` fields) and all images are byte-identical to the previous submission, and the email, phone and Instagram `href`s and text are unchanged (checked in the browser). There are no external scripts or libraries and no CSS/JS files. I could not compare against the original starter files, because they are not in the project files; earlier statements that the code matched the original came from an earlier session and were not re-checked here.

**Footer links, measured:** at 360, 768 and 1280 px the email, phone and Instagram links are each 25.6 px high (they were 19 px) and 197, 146 and 81 px wide; all five probe points inside each link land on that link, the target areas do not overlap each other, and the footer height and address-block position are identical to the previous build. At 360 px the phone number no longer breaks across two lines, because the link is now one block. I first tried vertical padding, but at 360 px the three links stack and their padded areas overlapped by 16 px, so I replaced it with the `min-height` version.

**Remaining accessibility notes:** the three axe "needs manual review" items above are still open. I did not use a screen reader.

**Could not be tested:** Firefox and WebKit (not installed), a real phone, a screen reader, fonts on a real network, an external JSON-LD validator, and any comparison with the original starter files or the original assessment brief (neither is available to me).

**Limitations that remain:** the accessibility notes above; `p108.webp` is a photo edit, so its sixth tin repeats the green tin's label art and the area behind the tins is a flat fill; the other product images are upscaled from about 330 px and look soft on high-DPI screens (section 3).

## 5. Countdown (assessment says to test it)
I removed it and did not restore it. The original counted to 2025-11-01 for a "Diwali Sale". That date has passed, so the original would show negative numbers (read from the code; I did not run the original). Nothing in `PRODUCTS` or `BRAND.md` supports a sale, a sale price or an end date, so any working countdown would need an invented date or claim, which the brief forbids. So there is nothing to test. If the team gives me a real offer and end date, I would add a countdown that stops at zero.

## 6. Questions for the team
- Free-shipping threshold: the code said ₹599, the banner said ₹499. I used ₹599.
- Is there a real sale and end date? (see section 5)
- "Shark Tank", "4.9/5 by 10,000+" and the "best tea in the world" lines are unsupported; I removed them. The three review quotes have no source; I kept them verbatim and show no ratings for them.
- Footer copyright said 2020 and "MistVale"; I used "© 2026 Mistvale Tea Co.". Is 2026 right, or should it read 2019-2026?
- The original quick view had 100g/250g sizes but no price per size; I removed them.
- Canonical and Open Graph URLs use https://mistvale.example/.
- Prompt 5, the exact prompt for the reference image, was not retained and is marked UNAVAILABLE. If the team has it, it can be pasted verbatim.
- The gift box image was edited to show six tins; should it be properly regenerated later? Is "100g" the correct pack weight shown on the tins?
- The hero says "Founded in 2019" (from BRAND.md).

## 7. Time spent
I did not measure it; I cannot give an honest hour count.

## 8. Extras
None.

## 9. With more time
Higher-resolution AI images (the current ones are upscaled from about 330 px), testing in Firefox/WebKit and on a phone, a screen-reader pass, Lighthouse with real fonts, size options, wishlist, URL-persisted filters, and a countdown once a real offer exists.

## 10. Submission contents
The ZIP contains `index.html`, `images/` (p101-p108.webp, hero-banner.webp, logo.svg), `NOTES.md` and `PROMPTS.md`, all at the root, with no other files. `README.md` and `BRAND.md` are deliberately not included: the final file structure given in the original master prompt (recorded as Prompt 1 in `PROMPTS.md`) lists only those four items and says not to add unrelated files. The original assessment brief and starter ZIP are not in the project files, so that is based on the prompt, not on the brief itself, and I did not create or invent either file.

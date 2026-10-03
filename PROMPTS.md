# PROMPTS

Prompts 1-4 and 6-13 are taken verbatim from the conversation between the user and Claude (claude.ai). Their "Tool" is Claude (Prompts 1-4: Claude Sonnet 4.6, as recorded at the time; Prompts 6-13: Claude Sonnet 5.5). Prompt 5 is the image-generation prompt for the reference image; its tool is as stated by the project owner, and its exact wording is **unavailable** (see Prompt 5). No other AI tool prompts are recorded here.

---

## Prompt 1

- Tool: Claude (Claude Sonnet 4.6, claude.ai)
- Type: code
- Prompt:

> I am giving you the complete starter ZIP for a developer assessment called **"Rescue the Mistvale Tea Store"**.
> 
> Your job is to take the existing starter project and turn it into a polished, production-quality tea store while following the assessment brief EXACTLY.
> 
> ## IMPORTANT WORKING RULES
> 
> 1. First inspect the entire ZIP before changing anything.
> 2. Read `README.md` and `BRAND.md` completely before making design or code decisions.
> 3. Inspect the complete `index.html`, including all HTML, CSS, JavaScript, `PRODUCTS`, and the `API` object.
> 4. Do NOT blindly redesign it with a generic AI ecommerce template.
> 5. Follow the Mistvale brand rules closely.
> 6. Preserve all factual information from the provided files.
> 7. Do not invent reviews, ratings, awards, press mentions, statistics, company claims, product facts, or other unsupported information.
> 8. Work within the assessment's 4-hour target and do not over-engineer unnecessary features.
> 
> ## HARD CONSTRAINTS — DO NOT BREAK THESE
> 
> - The store must remain a single `index.html`.
> - ALL CSS must remain inside `index.html`.
> - ALL JavaScript must remain inside `index.html`.
> - Images must be inside `images/`.
> - Do NOT introduce React, Vue, Angular, Tailwind, Bootstrap, jQuery, Font Awesome, animate.css, or any other framework/library.
> - Plain HTML, CSS and JavaScript only.
> - Google Fonts are allowed.
> - Do NOT change any `PRODUCTS` id, name, or price.
> - Product prices must always be calculated from the `PRODUCTS` data, never from displayed text.
> - Do NOT modify the `API` object between `API START` and `API END`.
> - Fix how the frontend uses the API, but do not modify the API implementation.
> - Do NOT change the approved legal text in the footer.
> - Keep the checkout form exactly as required:
>   - `id="checkout-form"`
>   - action=`https://mistvale.example/cart/checkout`
>   - method=`POST`
>   - fields named `items` and `coupon`
> - On checkout:
>   - `items` must contain JSON such as `[{"id":101,"qty":2}]`
>   - `coupon` must contain the applied coupon or an empty value.
> 
> ## BUSINESS RULES
> 
> Implement and test all of these carefully:
> 
> ### R1 — Prices
> Prices in `PRODUCTS` are per pack and include GST.
> 
> Always calculate totals from `PRODUCTS`.
> 
> ### R2 — Quantity
> A shopper can buy at most 5 units of a product.
> 
> Never allow quantity greater than the product's stock.
> 
> Sold-out products cannot be added.
> 
> ### R3 — Coupon
> Coupon:
> 
> `WELCOME10`
> 
> Rules:
> 
> - case-insensitive
> - 10% discount
> - applies only to eligible products
> - maximum discount ₹150
> - subtotal must be at least ₹399
> - products in category `Gifts` are NOT eligible
> - only one coupon per order
> - applying the same coupon twice must not change the result
> 
> Make sure the discount calculation handles carts containing both eligible and ineligible products correctly.
> 
> ### R4 — Shipping
> 
> Shipping = ₹49.
> 
> Shipping becomes FREE when the amount AFTER discount reaches the free-shipping threshold.
> 
> Do not calculate free shipping from the pre-discount subtotal.
> 
> ### R5 — Currency / rounding
> 
> Only round the FINAL total to the nearest rupee.
> 
> Display all money using:
> 
> `₹`
> 
> and Indian digit grouping.
> 
> Example:
> 
> `₹1,23,456`
> 
> Do not prematurely round intermediate calculations.
> 
> ### R6 — Sold out
> 
> Sold-out products:
> 
> - cannot be added to cart
> - must always appear LAST in every sort order
> 
> ### R7 — Search/filter/sort
> 
> Search, category filter and sort must work together.
> 
> Changing one must preserve the others.
> 
> The displayed results must always match the CURRENT search input.
> 
> Test combinations such as:
> 
> - search + category
> - search + sort
> - category + sort
> - search + category + sort
> 
> ### R8 — Pincode delivery
> 
> Use the existing:
> 
> `API.checkPincode()`
> 
> Do not modify the API.
> 
> The UI must correctly show:
> 
> - delivery time in days
> - not serviceable
> - helpful error for invalid pincode
> 
> It must NEVER remain stuck on:
> 
> `Checking…`
> 
> Handle loading, success, invalid input, API errors and slow responses correctly.
> 
> ## BUG HUNT
> 
> Do not only fix obvious bugs.
> 
> Actually interact with the store and look for bugs involving:
> 
> - first visit with empty localStorage
> - empty cart
> - adding the same product multiple times
> - rapid clicks
> - expensive products
> - quantity limits
> - stock limits
> - removing products
> - changing quantities
> - coupon applied twice
> - coupon after cart changes
> - coupon with Gifts
> - subtotal exactly around ₹399
> - discount exactly around ₹150
> - free shipping before/after discount
> - search while typing quickly
> - search + filter + sort
> - sold-out products
> - sorting with sold-out products
> - quick view
> - newsletter
> - countdown
> - delivery check
> - refreshing the page
> - corrupted/invalid localStorage data
> - mobile layout
> - keyboard navigation
> - focus states
> 
> Fix root causes instead of adding superficial patches.
> 
> ## DESIGN REQUIREMENTS
> 
> Transform the store into a modern, premium and trustworthy tea brand.
> 
> IMPORTANT:
> 
> Do NOT produce a generic "AI ecommerce website".
> 
> The design must clearly follow the exact rules in `BRAND.md`.
> 
> Pay attention to:
> 
> - typography
> - spacing
> - color palette
> - visual hierarchy
> - button styles
> - hover states
> - focus states
> - disabled states
> - cards
> - navigation
> - responsive layout
> - CTA hierarchy
> - subtle purposeful animation
> - premium tea-brand feel
> - mobile usability
> 
> The final result should look intentionally designed for Mistvale Tea Co.
> 
> ## SHOPPING UX
> 
> Think like a real customer using the store on a phone.
> 
> Improve:
> 
> - product discovery
> - search
> - filtering
> - sorting
> - quick view
> - product information
> - add-to-cart feedback
> - cart editing
> - quantity controls
> - remove controls
> - coupon experience
> - shipping progress
> - checkout flow
> - delivery check
> - newsletter experience
> 
> Avoid annoying alerts where a better inline/toast UI is appropriate.
> 
> Make cart updates immediately understandable.
> 
> ## ACCESSIBILITY
> 
> Ensure:
> 
> - semantic HTML
> - keyboard navigation
> - visible focus states
> - accessible buttons
> - proper labels
> - appropriate ARIA where required
> - sufficient contrast
> - meaningful alt text
> - dialog/quick-view keyboard behavior
> - Escape closes dialogs where appropriate
> - focus handling for modals
> - no keyboard traps
> 
> Test the major interactions using keyboard only.
> 
> ## RESPONSIVE DESIGN
> 
> The page must work from:
> 
> `360px`
> 
> through desktop widths.
> 
> There must be NO horizontal/sideways scrolling.
> 
> Pay special attention to:
> 
> - navigation
> - hero
> - product grid
> - filters
> - search
> - product cards
> - quick view
> - cart
> - checkout
> - footer
> 
> Test at several mobile and desktop viewport sizes.
> 
> ## SEO
> 
> Implement complete basic SEO including:
> 
> - meaningful `<title>`
> - meta description
> - canonical URL if appropriate based on provided information
> - semantic heading hierarchy
> - Open Graph metadata
> - appropriate image metadata
> - JSON-LD
> 
> Include structured data for:
> 
> - Organization
> - Products
> - FAQ
> 
> Only use facts actually provided by the starter kit / BRAND.md / PRODUCTS.
> 
> Do not invent facts for schema.
> 
> ## FAQ
> 
> Create a useful real FAQ section based ONLY on information available in the provided materials.
> 
> Add valid FAQ structured data matching the visible FAQ content.
> 
> ## IMAGES
> 
> Replace placeholder images with proper AI-generated assets.
> 
> Need:
> 
> - 8 product images
> - 1 hero banner
> - 1 clean Mistvale Tea Co. logo
> 
> The product images must:
> 
> - match their actual product descriptions
> - have a consistent visual style
> - use consistent dimensions/aspect ratio
> - feel premium
> - work together visually
> - be optimized for web
> 
> Prefer SVG for the logo if appropriate.
> 
> Do not generate unsupported product claims or visual details that contradict the actual product descriptions.
> 
> Optimize images for reasonable web performance.
> 
> ## PERFORMANCE
> 
> Keep the site lightweight.
> 
> Avoid unnecessary JavaScript and unnecessary dependencies.
> 
> Optimize images.
> 
> Avoid excessive animations.
> 
> Use efficient DOM updates.
> 
> Avoid layout shifts where practical.
> 
> ## OPTIONAL BONUS FEATURES
> 
> Only add extras AFTER the required brief is working correctly.
> 
> Possible extras include:
> 
> - recently viewed products
> - wishlist
> - URL-persisted filters/sort
> - product detail view
> - recommendations
> - size options
> - gift message
> 
> Do not add features merely to make the code larger.
> 
> Every extra must respect the original constraints and business rules.
> 
> ## PROMPTS.md — VERY IMPORTANT
> 
> Create `PROMPTS.md`.
> 
> Every AI prompt used during this task must be logged.
> 
> The prompt must be recorded EXACTLY as typed.
> 
> Do NOT clean it up afterward.
> 
> Do NOT paraphrase it.
> 
> Include both coding prompts and image prompts.
> 
> Use this format:
> 
> ## Prompt 1
> 
> - Tool: [tool name]
> - Type: code | image | other
> - Prompt:
> 
> > [EXACT PROMPT]
> 
> - Outcome: accepted | modified | rejected
> - Why: [short explanation]
> 
> Continue sequentially.
> 
> If you use multiple AI tools, record each tool separately.
> 
> Dead-end prompts must also be recorded.
> 
> IMPORTANT: Keep the prompt wording exactly as actually used.
> 
> ## NOTES.md
> 
> Create a concise but honest `NOTES.md`.
> 
> Include:
> 
> 1. What I changed
>    - bugs
>    - design
>    - UX
>    - images
>    - technical improvements
> 
> 2. What the AI got wrong
>    - give specific examples
>    - explain how the mistakes were detected
>    - explain what was corrected
> 
> 3. Images
>    - which tool generated each image
>    - any crop/resize/compression/conversion performed
> 
> 4. How I tested it
>    - browsers
>    - viewport sizes
>    - keyboard testing
>    - accessibility checks
>    - Lighthouse/performance checks if performed
> 
> 5. Questions for the team
>    - anything ambiguous
>    - anything where a temporary decision had to be made
> 
> 6. Time spent
>    - honest estimate
> 
> 7. Extra features added
> 
> 8. With more time I would...
> 
> Do not claim tests were performed if they were not actually performed.
> 
> Do not claim a feature works if you did not verify it.
> 
> ## TESTING
> 
> Before declaring the task complete, systematically test:
> 
> 1. Product rendering
> 2. Search
> 3. Category filtering
> 4. Sorting
> 5. Search + filter + sorting together
> 6. Sold-out behavior
> 7. Add to cart
> 8. Quantity changes
> 9. Quantity maximum 5
> 10. Stock limits
> 11. Remove item
> 12. Empty cart
> 13. Coupon eligibility
> 14. Gifts excluded from coupon
> 15. ₹399 minimum
> 16. ₹150 discount cap
> 17. Duplicate coupon application
> 18. Shipping threshold after discount
> 19. Currency formatting
> 20. Final rounding
> 21. Pincode delivery
> 22. Pincode errors
> 23. Quick view
> 24. Newsletter
> 25. Countdown
> 26. Checkout form payload
> 27. localStorage persistence
> 28. corrupted localStorage handling
> 29. keyboard navigation
> 30. modal focus/escape behavior
> 31. mobile at 360px
> 32. tablet
> 33. desktop
> 34. horizontal overflow
> 35. SEO metadata
> 36. JSON-LD validity
> 37. FAQ schema
> 38. image loading/performance
> 
> ## FINAL FILE STRUCTURE
> 
> The final ZIP should contain:
> 
> yourname-mistvale.zip
> 
> ├── index.html
> ├── images/
> ├── NOTES.md
> └── PROMPTS.md
> 
> Do not include unnecessary dependencies, build folders, node_modules, framework files, or unrelated files.
> 
> ## FINAL REVIEW
> 
> Before finishing, perform a final code review specifically checking:
> 
> - No framework/library was introduced.
> - CSS remains inside `index.html`.
> - JS remains inside `index.html`.
> - `API` object is unchanged.
> - `PRODUCTS` IDs/names/prices are unchanged.
> - Footer legal text is unchanged.
> - Checkout contract is preserved.
> - No unsupported factual claims were added.
> - All required business rules are implemented.
> - Sold-out products are last in every sort.
> - Coupon logic is correct.
> - Shipping logic is correct.
> - Final rounding is correct.
> - Search/filter/sort state is consistent.
> - Pincode cannot get permanently stuck.
> - Mobile has no horizontal overflow.
> - Accessibility is handled.
> - SEO/schema is present.
> - Images are optimized.
> - `PROMPTS.md` contains every prompt exactly as used.
> - `NOTES.md` is honest and complete.
> 
> Do not stop after making the page "look good".
> 
> The goal is a **tested, trustworthy, polished Mistvale Tea Co. store that satisfies the assessment brief and its constraints.**
> 
> Start by inspecting the entire ZIP and report the files you found, the current architecture, the major bugs you identified, and the design rules you extracted from `BRAND.md`. Then proceed with the implementation.

- Outcome: modified
- Why: Claude completed the rebuild and all business-rule fixes. It did not produce AI-generated images (no image-generation tool is available to Claude in this environment) and instead drew them procedurally with Python/Pillow. The initial code had bugs that were caught and fixed in later rounds.

---

## Prompt 2

- Tool: Claude (Claude Sonnet 4.6, claude.ai)
- Type: other
- Prompt:

> all error are remove??

- Outcome: modified
- Why: Claude ran a Playwright regression and reported what was and was not verified. Several checks were still pending. Claude honestly said the project was not complete.

---

## Prompt 3

- Tool: Claude (Claude Sonnet 4.6, claude.ai)
- Type: code
- Prompt:

> Do not tell me that the project is complete yet.
> Perform one final QA pass on the current Mistvale store before submission.
> First, take screenshots of the page at:
> 
> * 360px
> * 768px
> * 1280px
> 
> Inspect the screenshots yourself for:
> 
> * broken layout
> * spacing problems
> * typography
> * overlapping elements
> * poor CTA hierarchy
> * inconsistent card heights
> * image quality
> * visual bugs
> * mobile navigation issues
> * horizontal overflow
> 
> Then perform a full keyboard-only test:
> 
> * Tab through the entire page
> * Shift+Tab
> * Enter/Space on interactive controls
> * Search
> * Filters
> * Sort
> * Product quick view
> * Add to cart
> * Quantity controls
> * Remove item
> * Coupon
> * Checkout
> * Newsletter
> * Cart close
> * Quick-view close
> * Escape behavior
> * Verify visible focus states
> * Verify there are no keyboard traps
> 
> Test rapid interactions:
> 
> * Rapidly click Add to Cart multiple times
> * Rapidly click + quantity
> * Rapidly click remove
> * Type quickly into search
> * Change search + category + sort rapidly
> * Verify stale search responses cannot overwrite newer results
> 
> Test the store in at least Chromium and one additional browser if available.
> Run a contrast/accessibility check if available.
> Run Lighthouse if available and record the actual result. Do not invent a score.
> Validate the JSON-LD/schema if a validator is available. Check:
> 
> * Organization
> * Product
> * FAQPage
> 
> Check the page with an empty cart and fresh localStorage.
> Check the page with corrupted localStorage.
> Verify the checkout form payload again.
> Verify that:
> 
> * API object is unchanged
> * footer legal text is unchanged
> * PRODUCTS ids/names/prices are unchanged
> * no framework/library has been introduced
> * all CSS and JS remain inside index.html
> * images are inside images/
> 
> Also inspect whether removing the countdown created any inconsistency with the assessment requirement. The brief explicitly says the countdown should be tested, so do not silently ignore this requirement. If the original countdown can be safely retained without inventing unsupported facts, restore/fix it. If it cannot be safely retained, document the reason clearly in NOTES.md.
> Do not claim a test passed unless you actually performed it.
> If you find any bug, fix it and rerun the relevant test.
> After all testing, update NOTES.md with:
> 
> * actual tests performed
> * actual results
> * bugs found and fixed
> * tests that genuinely could not be performed
> 
> Do not fabricate any testing, scores, screenshots, browser results, or findings.
> Finally, re-create the ZIP only after the QA pass is complete.

- Outcome: accepted
- Why: Claude ran screenshots, keyboard tests, rapid-interaction tests, axe-core, and Lighthouse (over local HTTP) and fixed every bug it found. It reported actual scores (not invented ones) and documented what it could not test.

---

## Prompt 4

- Tool: Claude (Claude Sonnet 4.6, claude.ai)
- Type: other
- Prompt:

> Before doing anything else, fix `PROMPTS.md`.
> Use the exact prompts I actually sent during this conversation/project, in the exact original wording.
> Do NOT invent prompts.
> Do NOT paraphrase prompts.
> Do NOT shorten prompts.
> Do NOT improve their grammar.
> Include:
> 
> 1. The original master prompt I sent when I gave you the assessment ZIP.
> 2. Every subsequent prompt I sent you during this project, including the final QA/testing prompt.
> 3. Any image-generation prompts that were actually used.
> 
> For each prompt use the required format:
> Prompt N
> 
> * Tool: [actual tool]
> * Type: code | image | other
> * Prompt:
> 
> [EXACT ORIGINAL PROMPT]
> 
> * Outcome: accepted | modified | rejected
> * Why: [short honest explanation]
> 
> If you do not have the exact original wording of a prompt, DO NOT fabricate it. Mark that prompt as unavailable and tell me which exact prompt I need to provide.
> After updating PROMPTS.md, re-create the ZIP.

- Outcome: accepted
- Why: This prompt. Claude wrote PROMPTS.md from the verbatim conversation history and re-created the ZIP.

---

---

## Prompt 5

- Tool: ChatGPT image generation
- Tool note: stated by the project owner. The PNG carries no metadata, so the tool cannot be verified from the file.
- Type: image
- Asset: Mistvale Tea Co. reference image
- Prompt:

> **UNAVAILABLE.** The exact original image-generation prompt was not retained. It was not provided in the Claude conversation or in any project file, and it is deliberately not reconstructed or invented here.

- Outcome: accepted
- Why: Generated the visual reference used for the final Mistvale product, hero and branding assets.

---

## Prompt 6

- Tool: Claude (Claude Sonnet 5.5, claude.ai)
- Type: other
- Prompt:

> Before making any changes, perform a strict verification of the image requirements in the current Mistvale project.
>
> Do NOT generate, replace, edit, or redesign anything yet.
>
> Inspect the actual files in the current project and verify the following:
>
> 1. Product images
> - Identify all 8 product images currently used by the store.
> - Give me their exact filenames.
> - Confirm whether each image is:
>   a) an actual AI-generated image,
>   b) a real/photo asset,
>   c) a procedural/programmatically generated image,
>   d) a placeholder, or
>   e) unknown/unverifiable.
> - Check whether each image matches the corresponding product.
> - Check whether all 8 images have a consistent visual style.
> - Check dimensions, aspect ratio and file format.
> - Check approximate file size.
> - Check whether the images are actually referenced by the current `index.html`.
>
> 2. Hero image
> - Identify the exact hero image filename.
> - Determine whether it is AI-generated, photographic, procedural, placeholder, or unknown.
> - Check whether it is actually used by the current store.
> - Check its dimensions, aspect ratio, format and approximate file size.
> - Check whether its visual content is appropriate for Mistvale Tea Co. and consistent with `BRAND.md`.
>
> 3. Logo
> - Identify the exact logo file.
> - Determine whether it is AI-generated, hand-written/vector-created, photographic, placeholder, or unknown.
> - Check whether it is actually used by the store.
> - Check dimensions, format and approximate file size.
> - Check whether it follows the Mistvale branding requirements.
>
> 4. Compare against the assessment brief
> The brief requires:
> - 8 product images
> - 1 hero banner
> - 1 clean logo for "Mistvale Tea Co."
> - images should be created with AI
> - image prompts must be logged in `PROMPTS.md`
>
> Do not assume an image is AI-generated just because it looks polished.
> Do not call a procedural Pillow/Python drawing AI-generated.
> Do not infer the generation tool if the project files do not prove it.
>
> 5. PROMPTS.md verification
> Check whether `PROMPTS.md` contains actual image-generation prompts.
>
> For each image prompt:
> - identify the prompt number
> - identify the tool
> - identify whether it is a code or image prompt
> - verify whether the prompt corresponds to an image actually present in the project
>
> If there are no real image-generation prompts, clearly say so.
>
> 6. Final verdict
>
> Return a table:
>
> | Asset | Filename | Used in store? | Type | AI-generated verified? | Matches product/brand? | Size/format | Status |
> |------|----------|----------------|------|------------------------|-------------------------|-------------|--------|
>
> Then give me:
>
> - Product images: PASS / FAIL
> - Hero: PASS / FAIL
> - Logo: PASS / FAIL
> - Image prompts in PROMPTS.md: PASS / FAIL
> - Overall image requirement: PASS / FAIL
>
> Do not modify any files.
>
> Do not invent evidence.
> Do not claim AI generation unless it can actually be verified from the project/history.
> If something cannot be verified, mark it as "Unknown / cannot verify" rather than guessing.
>
> At the end, tell me exactly what still needs to be done before submission.

- Outcome: accepted
- Why: Claude inspected the project without changing it. It reported that all 10 assets were procedural drawings or a hand-written SVG, that none was AI-generated, and that PROMPTS.md had no image prompts.

---

## Prompt 7

- Tool: Claude (Claude Sonnet 5.5, claude.ai)
- Type: code
- Prompt:

> I am attaching an AI-generated Mistvale Tea Co. reference image.
>
> Use this attached image as the source/reference for the final image assets in the current Mistvale Tea Store project.
>
> IMPORTANT:
> - Do not change the existing application logic.
> - Do not modify the API object.
> - Do not modify PRODUCTS ids, names or prices.
> - Do not change the checkout contract.
> - Do not introduce any framework or library.
> - Keep the existing filenames/references.
>
> The attached image contains:
> - Mistvale Tea Co. logo
> - Mistvale tea-garden hero scene
> - Assam Breakfast Black Tea
> - Darjeeling First Flush
> - Kashmiri Kahwa
> - Masala Chai Blend
> - Nilgiri Green Tea
> - Chamomile & Tulsi
> - Hibiscus Rose Infusion
> - Tea Lover's Sampler Gift Box
>
> ## TASK
>
> Use the attached AI-generated image to create the final image assets required by the store.
>
> Create/replace:
>
> images/p101.webp  → Assam Breakfast Black Tea
> images/p102.webp  → Darjeeling First Flush
> images/p103.webp  → Kashmiri Kahwa
> images/p104.webp  → Masala Chai Blend
> images/p105.webp  → Nilgiri Green Tea
> images/p106.webp  → Chamomile & Tulsi
> images/p107.webp  → Hibiscus Rose Infusion
> images/p108.webp  → Tea Lover's Sampler Gift Box
>
> images/hero-banner.webp → use the tea-garden hero section from the attached image
>
> images/logo.svg → create a clean vector logo based on the Mistvale logo shown in the attached image.
>
> ## IMAGE QUALITY
>
> For each product:
> - minimum 800×800 px
> - square 1:1
> - WebP
> - optimized for web
> - preserve the premium photorealistic style of the attached image
> - preserve the product-specific ingredients and colours
> - keep consistent lighting and background treatment
> - do not use generic placeholder graphics
> - do not recreate the old Pillow illustrations
>
> Hero:
> - approximately 1600×750 px
> - wide composition
> - preserve the misty tea-garden aesthetic
> - no unnecessary text embedded in the hero image
>
> Logo:
> - SVG
> - clean vector
> - transparent background
> - complete visible wordmark: "Mistvale Tea Co."
> - preserve the mountain/leaf concept and green brand palette
> - suitable for the website header
>
> ## IMPORTANT ABOUT THE SOURCE
>
> The attached image was generated with an AI image-generation tool.
>
> Do not claim that you generated the image yourself.
>
> Use the attached image as the AI-generated source/reference for this project.
>
> If you crop individual product panels from the source image, make sure the final assets are properly resized and optimized. Do not simply leave tiny cropped panels at low resolution.
>
> If a higher-quality extraction is possible, use the best available source region for each asset.
>
> ## PROMPTS.md
>
> Update PROMPTS.md with the exact image-generation prompt that was used to create the attached AI reference image.
>
> Do NOT invent a different prompt.
>
> If the exact original image-generation prompt is not available in the current conversation/project files, explicitly tell me that it is unavailable instead of fabricating it.
>
> For the image prompt entry use:
>
> ## Prompt 5
>
> - Tool: ChatGPT image generation
> - Type: image
> - Asset: Mistvale Tea Co. reference image
> - Prompt:
>
> > [EXACT ORIGINAL IMAGE-GENERATION PROMPT IF AVAILABLE]
>
> - Outcome: accepted
> - Why: Generated the visual reference used for the final Mistvale product, hero and branding assets.
>
> For Prompt 6 onward, only add prompts that are actually used.
>
> ## FINAL CHECK
>
> After replacing the assets:
>
> 1. Verify all 8 product images load.
> 2. Verify hero loads.
> 3. Verify logo loads.
> 4. Verify filenames match the existing code.
> 5. Verify dimensions.
> 6. Verify WebP format for product/hero images.
> 7. Verify SVG logo contains "Mistvale Tea Co."
> 8. Verify the old procedural Pillow images are no longer being used.
> 9. Verify PROMPTS.md is honest and contains only prompts actually used.
> 10. Do not change working application logic.
>
> Then recreate the final ZIP.
>
> Do not claim that an asset is AI-generated unless the attached source actually came from an AI image-generation tool.

- Outcome: modified
- Why: Claude cropped the 8 product panels and the hero from the attached AI reference image, upscaled them (about 2.4x, with a super-resolution model, so detail is limited to the source resolution), and rebuilt the logo as vector. Limitations: the gift-box panel shows five tins while the product text says six; the exact reference-image prompt was unavailable.

---

## Prompt 8

- Tool: Claude (Claude Sonnet 5.5, claude.ai)
- Type: other
- Prompt:

> FINAL FIX — DO NOT JUST VERIFY. MODIFY THE PROJECT.
> The current ZIP is almost ready. Make only these final fixes:
> 1. Fix `p108` gift-box image
>
> * Replace/regenerate `images/p108.webp`.
> * It must clearly show exactly 6 tea tins/tea products, because the existing product description says “Six of our favourite teas”.
> * Keep the same Mistvale visual style, packaging style, lighting, background and overall design as the current reference assets.
> * Keep the required filename `p108.webp`.
> * Final size must remain 800×800 WebP.
> * Do not modify the product name, price, `PRODUCTS` data, API, checkout logic, or other application logic.
>
> 2. Fix `PROMPTS.md` Prompt 5
>
> * I will provide the exact original image-generation prompt separately if available.
> * Do NOT invent or reconstruct an original prompt.
> * If the exact original prompt is genuinely unavailable, keep it explicitly marked `UNAVAILABLE` rather than fabricating one.
>
> 3. Do not make unnecessary changes
>
> * Do not redesign the website.
> * Do not change product IDs, names, prices, API, checkout, or business logic.
> * Do not change filenames.
> * Do not replace the other 7 product images, hero, or logo unless absolutely required.
>
> 4. Final verification
> Check that:
>
> * `p108.webp` exists and is exactly 800×800 WebP.
> * It visibly contains exactly 6 tins.
> * It loads correctly in the website.
> * No old procedural image is being used.
> * `PROMPTS.md` is honest and contains no fabricated prompt.
> * Existing code/API/PRODUCTS/checkout remain unchanged.
>
> Important: Actually make the required changes. Do not only generate a verification report.
> After completing the changes, create the final ZIP again.

- Outcome: modified
- Why: Claude has no image-generation tool, so `p108.webp` was not newly AI-generated. Claude edited the existing p108 photo with OpenCV: it cut out the five tins, made them slightly narrower, added a sixth tin (a recoloured copy of the green tin, now purple), and covered the old tin tops behind the row with a dark shadow tone. The result shows six tins, but it is an edit of the existing picture, not a fresh render, and the extra tin repeats the green tin's label artwork. Prompt 5 was left as `UNAVAILABLE` because no original prompt was provided.

---

## Prompt 9

- Tool: Claude (Claude Sonnet 5.5, claude.ai)
- Type: other
- Prompt:

> FINAL SUBMISSION AUDIT — DO NOT MODIFY ANY FILE
> Inspect the current `yourname-mistvale.zip` and verify the complete submission one final time.
> Check:
>
> 1. All 8 product images load.
> 2. `p108.webp` visibly contains exactly 6 tins.
> 3. Hero and logo load.
> 4. All required filenames and dimensions are correct.
> 5. `PROMPTS.md` contains all prompts that are actually available and does not fabricate unavailable prompts.
> 6. `NOTES.md` accurately describes the final state, including the fact that p108 was edited rather than regenerated.
> 7. No old procedural/Pillow images are referenced.
> 8. `PRODUCTS`, API, checkout and business logic are unchanged.
> 9. No broken image requests or console errors.
> 10. Check the ZIP structure and confirm all required files are included.
>
> Do not change anything. Give me only a final PASS/FAIL checklist and list any remaining submission risks. Do not claim a requirement is satisfied if the evidence does not support it.

- Outcome: accepted
- Why: This was an audit only. Claude read the ZIP and made no modifications to the project: no file inside it was changed. It reported a checklist with some items passing and some partial (the `NOTES.md` p108 wording, the Google Fonts 403 in the sandbox, no `README.md` or `BRAND.md` in the ZIP), and listed remaining risks, including that Prompt 5 is unavailable.

---

## Prompt 10

- Tool: Claude (Claude Sonnet 5.5, claude.ai)
- Type: other
- Prompt:

> FINAL CLEANUP ONLY — DO NOT REDESIGN
> Make only these final administrative fixes:
>
> 1. Update `NOTES.md` so every reference to `p108.webp` accurately says that the final image was edited from the existing reference image, with a sixth tin added as a purple recolour. Remove/replace any older statement saying that p108 is simply a straight crop.
> 2. Keep Prompt 5 in `PROMPTS.md` as `UNAVAILABLE` because the exact original image-generation prompt was not retained. Do not invent or reconstruct it.
> 3. Add the final audit prompt to `PROMPTS.md` as Prompt 9, clearly stating that it was an audit only and made no project modifications.
> 4. Do not modify `index.html`, `PRODUCTS`, API, checkout, images, logo, hero, or application logic.
> 5. Rebuild the ZIP with the same root structure.
> 6. Rename the final ZIP to `Harsh-Vardhan-Maurya-Mistvale.zip`.
> 7. Do not claim any unverified tests were performed.

- Outcome: modified
- Why: Administrative cleanup only. Claude rewrote the p108 references in `NOTES.md`, kept Prompt 5 as `UNAVAILABLE`, added Prompt 9, and rebuilt the ZIP under the new name. It did not change `index.html`, the images, or any application logic.

---

## Prompt 11

- Tool: Claude (Claude Sonnet 5.5, claude.ai)
- Type: other
- Prompt:

> FINAL SUBMISSION COMPLETION PASS — COMPLETE ALL REMAINING ITEMS
>
> Do not just audit and report. Actually complete the remaining submission work wherever possible.
>
> 1. PROMPTS.md
> - Add the exact cleanup prompt you received as Prompt 10.
> - Keep Prompt 5 as UNAVAILABLE / "was not retained".
> - Do NOT invent any missing image-generation prompt.
> - Make sure PROMPTS.md now records every prompt actually used in this workflow.
>
> 2. ORIGINAL BRIEF / REQUIRED FILES
> - Inspect the original assessment brief and/or starter ZIP if available in the project/files.
> - Determine definitively whether README.md and/or BRAND.md are required in the final submission.
> - If they are required and the original versions/content are available, include them in the final ZIP.
> - If they are NOT required, leave them out.
> - Do not invent either file or invent missing brand information.
>
> 3. FULL FINAL QA
> Run the complete available QA suite again AFTER all final changes:
> - 360px viewport
> - 768px viewport
> - 1280px viewport
> - Full page image loading
> - No horizontal overflow
> - Search + category filtering
> - Sorting
> - Cart add/remove/quantity limits
> - Sold-out products
> - Coupon rules
> - Shipping calculation
> - Pincode validation
> - Checkout payload
> - localStorage empty/corrupt/oversized cases
> - Escape key / cart / quick view
> - Rapid clicks / stale search handling
> - Keyboard navigation and visible focus
> - axe-core accessibility check
> - Lighthouse
> - JSON-LD/schema validation if available
> - Console errors
> - Network failures
>
> Do not claim a test passed unless you actually ran it.
>
> 4. GOOGLE FONTS
> - Test the site with normal network access if the environment allows it.
> - Determine whether the previous Google Fonts 403 was only caused by the sandbox.
> - If it cannot be tested because of the environment, document it honestly in NOTES.md as unverified.
> - Do not remove or replace the Google Fonts setup just to hide the error.
>
> 5. FINAL ASSET CHECK
> Verify:
> - p101–p108 = 800×800 WebP
> - hero = 1600×750 WebP
> - logo loads
> - p108 visibly contains exactly six tins
> - no old procedural/Pillow images are referenced
> - all image paths in index.html exist
> - no broken image requests
>
> 6. FINAL NOTES
> Update NOTES.md so it contains only accurate final-state information.
> Clearly disclose:
> - p108 was edited rather than freshly AI-generated
> - Prompt 5 was unavailable/not retained
> - which tests were actually run
> - which tests could not be run and why
> - any remaining limitations
>
> 7. FINAL ZIP
> - Keep the required root structure.
> - Remove temporary/unnecessary files.
> - Use the final filename:
>   Harsh-Vardhan-Maurya-Mistvale.zip
> - Make sure there is only one final ZIP.
> - Run an integrity check on the final ZIP.
>
> IMPORTANT:
> Do not modify application logic, PRODUCTS, API, checkout, prices, product IDs, or business rules unless the original brief explicitly requires it.
> Do not fabricate prompts, tests, files, brand rules, or results.
>
> At the end, give me a final table with:
> PASS / FAIL / UNVERIFIED
> for every requirement, and clearly list anything that still prevents submission.

- Outcome: modified
- Why: Claude searched the project files for the original brief and starter ZIP and found neither. It decided that `README.md` and `BRAND.md` are not required, based on the file structure in Prompt 1, and left them out. It then re-ran the QA suite on the final files and recorded the results in `NOTES.md`. It added Prompts 10 to 12 here and rebuilt the ZIP. Application code, `PRODUCTS`, the API, checkout and all images were not changed in this pass.

---

## Prompt 12

- Tool: Claude (Claude Sonnet 5.5, claude.ai)
- Type: other
- Prompt:

> continue

- Outcome: accepted
- Why: Sent while Prompt 11 was still being worked on, to let Claude carry on. It added no new instructions.

---

## Prompt 13

- Tool: Claude (Claude Sonnet 5.5, claude.ai)
- Type: other
- Prompt:

> FINAL ACCESSIBILITY FIX — ONLY THESE 2 ISSUES
>
> Fix only the two verified accessibility findings. Do not redesign anything and do not modify PRODUCTS, API, prices, checkout, business rules, or image assets.
>
> 1. CATEGORY CHIP FOCUS
> - When a category chip/button is focused and activated with Enter, keyboard focus must remain on that same category chip after the UI/filter update.
> - Do not allow focus to fall back to document.body.
> - Preserve visible focus styling.
> - Verify with keyboard only and test multiple category chips.
>
> 2. FOOTER LINKS
> - Fix the footer email, phone and Instagram link hit areas so they satisfy the applicable accessibility target-size requirement.
> - Prefer increasing the clickable/hit area with padding or an appropriate inline-link technique without changing the visual design significantly.
> - Do not change the actual email, phone or Instagram URLs/text.
> - Verify the resulting clickable area.
>
> AFTER FIXING:
> - Re-run the relevant keyboard/accessibility tests.
> - Re-run axe-core.
> - Re-run Lighthouse.
> - Re-run the full functional suite to make sure these changes did not break anything.
> - Test at 360px, 768px and 1280px.
> - Do not claim PASS unless actually tested.
>
> Update NOTES.md with the actual changes and test results.
>
> Add this exact prompt to PROMPTS.md as the next prompt number.
>
> Rebuild:
> Harsh-Vardhan-Maurya-Mistvale.zip
>
> Do not make any other changes.

- Outcome: modified
- Why: Claude changed two things in `index.html`: the category-chip click handler now puts focus back on the activated chip, and the footer email, phone and Instagram links became `inline-block` with `min-height:24px`. Its first footer attempt, vertical padding, made the stacked links overlap at 360 px, so it replaced that. It re-ran the keyboard and footer tests, axe-core, Lighthouse and the full functional suite, recorded the results in `NOTES.md`, and rebuilt the ZIP. `PRODUCTS`, the API, checkout, prices and all images were not changed.

---

## Image provenance

- The only image-generation prompt is Prompt 5, and its text is unavailable (see above).
- `p108.webp` was later edited by Claude (Prompt 8) to show six tins. That edit is a photo manipulation, not AI generation, and no prompt was used for it.
- Prompt 1 (Why) records that the earlier Pillow drawings were procedural, not AI-generated. Those drawings were superseded by Prompt 7 and are no longer in the project.
- Seven product images (p101-p107) and the hero are crops of the AI reference image from Prompt 5, resized with a super-resolution upscaler and converted to WebP. `p108.webp` started as the same kind of crop and was then edited (Prompt 8) to show six tins. The logo is a hand-built SVG based on the logo in that reference image, not itself AI-generated.

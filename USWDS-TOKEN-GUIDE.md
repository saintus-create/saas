# USWDS Token Reference Guide

## Typography Tokens

### Headings (use for h1-h6)
```vue
<h1 class="text-heading-2xl">48px</h1>  <!-- Main page title -->
<h2 class="text-heading-xl">40px</h2>    <!-- Section title -->
<h3 class="text-heading-lg">32px</h3>    <!-- Subsection title -->
<h4 class="text-heading-md">24px</h4>    <!-- Card title -->
<h5 class="text-heading-sm">20px</h5>    <!-- Small section title -->
<h6 class="text-heading-xs">17px</h6>    <!-- Minimal title -->
```

### Body Text
```vue
<p class="text-body-lg">18px</p>   <!-- Lead paragraph -->
<p class="text-body-md">17px</p>   <!-- Default body text -->
<p class="text-body-sm">15px</p>   <!-- Secondary text -->
<p class="text-body-xs">13px</p>   <!-- Captions, footnotes -->
```

### Quick Sizes (for special cases)
```vue
text-3xs  <!-- 13px -->
text-2xs  <!-- 14px -->
text-xs   <!-- 15px -->
text-sm   <!-- 16px -->
text-md   <!-- 17px -->
text-lg   <!-- 18px -->
text-xl   <!-- 20px -->
text-2xl  <!-- 24px -->
text-3xl  <!-- 32px -->
text-4xl  <!-- 40px -->
text-5xl  <!-- 48px -->
```

---

## Color Tokens

### USWDS Blue (Primary)
```vue
bg-blue-50   <!-- #005ea2 - Primary buttons, links -->
bg-blue-60   <!-- #1a4480 - Hover states -->
bg-blue-70   <!-- #162e51 - Header/footer -->
text-blue-50 <!-- Links, primary text -->
```

### USWDS Navy (Secondary)
```vue
bg-navy-80   <!-- #1e2d4e - Header background -->
bg-navy-90   <!-- #162e51 - Footer background -->
text-navy-60 <!-- Dark text -->
```

### USWDS Red (Errors)
```vue
text-red-50  <!-- #b50909 - Error messages -->
bg-red-5     <!-- #f9eded - Error background -->
```

### USWDS Green (Success)
```vue
text-green-50 <!-- #00a91c - Success messages -->
bg-green-5    <!-- #e7f4e4 - Success background -->
```

### Light Blues (Backgrounds)
```vue
bg-blue-10   <!-- #d9e8f6 - Secondary button fill -->
bg-blue-20   <!-- #aacdec - Hover state -->
```

---

## Standard Usage Pattern

### Page Structure
```vue
<!-- Page title -->
<h1 class="text-heading-2xl font-bold text-blue-70">Page Title</h1>

<!-- Section title -->
<h2 class="text-heading-xl font-bold text-blue-70">Section</h2>

<!-- Body text -->
<p class="text-body-md text-gray-70">Content here</p>

<!-- Primary button -->
<UButton class="bg-blue-50 hover:bg-blue-60 text-white" />

<!-- Secondary button -->
<UButton class="bg-blue-10 hover:bg-blue-20 text-blue-70" />

<!-- Error message -->
<p class="text-body-sm text-red-50">Error occurred</p>

<!-- Success message -->
<p class="text-body-sm text-green-50">Success!</p>
```

### Login/Signup Pages
```vue
<!-- Form heading -->
<h1 class="text-heading-md font-bold text-[#1b1b1b]">Sign in</h1>

<!-- Label -->
<label class="text-body-sm font-semibold">Email address</label>

<!-- Input -->
<UInput class="text-body-md" />

<!-- Help text -->
<p class="text-body-sm text-neutral-600">Help text here</p>
```

---

## Key Rules

1. **Always use heading tokens for h1-h6**, not text-4xl, text-3xl, etc.
2. **Always use body tokens for paragraph text**, not text-md, text-sm (unless special case)
3. **Use USWDS color tokens**, not arbitrary hex values like `bg-[#005ea2]`
4. **Keep text-box-trim** as-is (already approved)
5. **Font family**: Always 'Public Sans' for USWDS compliance

---

## Before vs After

### ❌ Before (Inconsistent)
```vue
<h1 class="text-4xl">Title</h1>
<p class="text-base">Body</p>
<UButton class="bg-[#005ea2]" />
```

### ✅ After (USWDS Standard)
```vue
<h1 class="text-heading-2xl">Title</h1>
<p class="text-body-md">Body</p>
<UButton class="bg-blue-50" />
```

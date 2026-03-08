# next/image — "resolved to private ip" Error

## Error
```
upstream image https://....supabase.co/storage/v1/object/public/avatars/...
resolved to private ip ["64:ff9b::6812:260a","64:ff9b::ac40:95f6"]
```

## Why it happens

`next/image` fetches and optimizes images **server-side** by default.
When the URL resolves to a **NAT64 address** (`64:ff9b::` prefix — an IPv4-to-IPv6 mapping),
Next.js blocks it as an SSRF security measure. Nothing to do with the bucket being public or private.

## Fix

Add `unoptimized` to skip server-side fetching — the browser fetches the URL directly instead.

```tsx
// ❌ Breaks — Next.js server tries to fetch → blocked
<Image src={supabaseAvatarUrl} width={72} height={72} />

// ✅ Works — browser fetches directly, no SSRF check
<Image src={supabaseAvatarUrl} width={72} height={72} unoptimized />
```

Also wrap in a clipping div for a proper circle:

```tsx
<div className="size-[72px] rounded-full overflow-hidden border-2 border-primary/30">
  <Image src={url} width={72} height={72} unoptimized className="w-full h-full object-cover" />
</div>
```

## When to use `unoptimized`

Use it for external URLs that resolve to NAT64/private IPs (common with Supabase Storage).
For small images like avatars the performance trade-off is negligible.

---
*Encountered in [ProfileSection.tsx](file:///Users/shraddha/projects/ats-checker/src/components/ui/ProfileSection.tsx) — March 2026*

# Braid Software Site

Astro static site for `braid.software`.

## Development

```sh
npm install
npm run dev
```

## Build

```sh
npm run build
```

## Paid Customer Flow

Product CTAs send customers to the hosted Lemon Squeezy checkout in
`src/lib/links.ts`.

After purchase, Lemon Squeezy should send customers to:

```text
https://braid.software/download?license_key=[license_key]
```

The `/download` page starts the public macOS DMG download and builds a
`braid://activate?license_key=...` link. The installed desktop app handles that
deep link and activates the license through the existing entitlement API.

# Toburt Product Support

Static customer support site for **support.toburt.com**.

The frontend is hosted by GitHub Pages. Product knowledge and AI answers come from the Digital Product Factory's `dp-support-api` Supabase Edge Function.

## One-time GitHub Pages setup

1. In this repository open **Settings → Pages**.
2. Under **Build and deployment**, publish from the `main` branch, root `/`.
3. Under **Custom domain**, enter `support.toburt.com` and Save.
4. At your DNS provider create:
   - Type: `CNAME`
   - Host/Name: `support`
   - Target/Value: `tophersendeavors.github.io`
5. After GitHub's DNS check completes, enable **Enforce HTTPS**.

GitHub Pages requests and manages the TLS certificate after the custom domain's DNS is configured correctly.

## Architecture

Customer browser
→ `support.toburt.com` (GitHub Pages)
→ `dp-support-api` (Supabase)
→ final product-version support knowledge
→ OpenAI only for product-use Q&A

The site contains no service-role key, OpenAI key, or private database credential.

## Factory rule

A product is not allowed to continue to release until its current version has a `dp_product_support` record with status `ready` and support QA score >= 90.

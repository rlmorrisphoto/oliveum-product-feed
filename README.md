# Oliveum Product Feed

Google/Microsoft Shopping-format product feed for [oliveum.com](https://oliveum.com).

**Feed URL (point Merchant Center here):**
https://raw.githubusercontent.com/rlmorrisphoto/oliveum-product-feed/main/oliveum_product_feed.xml

Consumed by:
- Google Merchant Center (account 5443803289)
- Microsoft Merchant Center (Microsoft Ads account 189319990 / cid 254976665)

## Regenerating

Generated from the live WooCommerce catalog — do not hand-edit `oliveum_product_feed.xml`.

```bash
cd ~/Documents/Claude/oliveum-ops
source venv/bin/activate
python3 pull_woocommerce_products.py   # pull current products from WooCommerce
python3 generate_product_feed.py       # rebuild the feed XML
```

Then copy the regenerated file here and push:

```bash
cp ~/Documents/Claude/oliveum-ops/oliveum_product_feed.xml .
git add oliveum_product_feed.xml && git commit -m "Refresh product feed" && git push
```

Both Merchant Centers re-fetch on their own schedule (set them to daily), so a push is all that's needed.

## Notes

- Collector's Box / blemished SKUs are deliberately excluded (self-fulfilled test-order items, not for ad-driven retail sales). The exclusion list lives in `generate_product_feed.py`.
- `identifier_exists` is set to `false` — Oliveum products have no registered GTIN/barcode, which both platforms allow for small brands.

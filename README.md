# บิลก๊วนแบด (Badminton Billing)

A single-page tool for splitting badminton court costs with friends, drawn in an xkcd-style sketch look (rough.js).

- One row per expense: name, price, and who fronted the money
- One column per friend (add with **+**), each cell has two checkboxes: **หาร** (shares this item) and **จ่าย** (has paid for it)
- Bottom rows show what each person still owes, plus a "paid everything" toggle
- Sketch bar chart of paid vs. unpaid, and a "who transfers to whom" list (netted between pairs)
- JSON export / import
- Thai / English toggle (TH | EN, top right), remembered per browser

## Running

`index.html` is written as a Claude Artifact page. Live sync between friends uses the Artifact `db` capability, so it only syncs when opened from its claude.ai artifact link. Opened anywhere else (local file, GitHub Pages), it still works but saves to that browser's `localStorage` only.

## JSON format

```json
{
  "format": "badminton-bill",
  "version": 2,
  "title": "ตีวันเสาร์",
  "people": [{ "id": "a1", "name": "พลับ" }, { "id": "b2", "name": "ฮ้อน" }],
  "items": [
    { "id": "i1", "name": "ค่าคอร์ด", "price": 40, "owner": "a1", "split": ["a1", "b2"], "paidBy": ["b2"] }
  ]
}
```

`owner`, `split` and `paidBy` hold person ids. Older exports with a top-level `"paid": [ids]` are still accepted.

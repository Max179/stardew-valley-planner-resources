# A source-checked Stardew Valley wiki: why I rebuilt the data layer

*Disclosure: I maintain Stardew Valley Planner, the fan site linked at the end of this post.*

Most Stardew Valley wikis look complete because they are large. The harder question is whether the numbers are current, whether two pages agree with each other, and whether anyone can tell where a value came from.

I maintain a small, independent Stardew Valley planning site. Over the last few weeks I stopped adding pages and rebuilt the data layer instead. The result is not a complete copy of the official wiki, but it is now much easier to audit.

## What the site covers

The site currently has 91 routes: item catalogues, NPC and gift pages, festival pages, and nine interactive tools. The tools are the reason the data has to be correct — a crop profit calculator is only useful if the seed price, growth time, and sell price all come from the same verified row.

Some current data points:

- 624 furniture entries imported from the official English and Chinese Furniture pages
- 150 crafting recipes after reconciling the official Crafting table
- 97 weapons, including the ten Desert Festival weapons and both slingshots
- 71 fish, 81 cooking recipes, 34 giftable NPCs, 12 festivals, and five mastery rewards

## The errors that made the rebuild necessary

The most useful part of an audit is usually the part that embarrasses you.

**1. A missing legendary fish.** The fish table had 70 entries. The official Wiki's Legendary Fish II set has five fish. Four were present; Radioactive Carp was not. It was added with its Sewers location, difficulty, size range, sell prices, and fish-pond data.

**2. “Furniture recipes” that were never recipes.** The crafting dataset had 149 entries, but 16 of them were furniture or miscellaneous items (Wood Chair, Oak Dresser, Mini-Fridge, Brazier, and similar). They are purchased or obtained, not crafted. At the same time, 17 real recipes were missing, including Bait, Grass Starter, Garden Pot, Wedding Ring, Iridium Band, and Tree Fertilizer. After removing the false entries and adding the missing ones, the set is 150 recipes — the normalized count from the official Crafting page.

**3. Furniture prices that were invented or stale.** I downloaded the complete official Furniture page and compared all 102 curated entries. Twenty-three prices were wrong, and several sources were wrong too. Examples: Child Bed was listed at 0 instead of 2,000g, Deluxe Fish Tank at 20 instead of 5,000g, Long Palm at 5 instead of 500g, and Calico Falls was attributed to the museum instead of Robin's shop. Thirty-five entries were corrected, then the catalogue was expanded to 624 items with official icons.

These are the kinds of errors that are easy to miss on a normal read and very obvious when a tool does arithmetic with them.

## How the data is checked now

Every dataset is registered at `/about/sources` with:

- the official Wiki page and, where useful, the Bilibili wiki cross-check
- the record count
- the date it was checked
- one of two coverage levels

“Sampled” means the count and key fields were compared with the source. “Checked” means the complete record set or name coverage was compared; individual stats may still be sampled. Both are deliberately honest labels. The site does not claim to be a field-by-field clone of the official Wiki.

The registry currently contains 24 datasets. Nine are marked checked; the rest are sampled. The official Wiki also occasionally returns 503, and the Bilibili wiki can rate-limit automated requests, so limitations are recorded rather than hidden.

## What this changes for players

The practical benefit is small but real: when you use the perfection tracker, the crop profit calculator, the bundle tracker, or the furniture catalogue, the numbers and the source page behind them are visible. If a value is wrong, there is a place to report it and a process for updating the data, the check date, and the affected page together.

If you want to see the result, start with:

- [Perfection tracker](https://www.stardewvalleywiki.net/tools/perfection)
- [Data sources and verification](https://www.stardewvalleywiki.net/about/sources)

The site is fan-made, unofficial, and not affiliated with ConcernedApe. The useful part is the audit trail, not the claim that it is the biggest wiki.

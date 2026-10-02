<!doctype html>
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<title>Tilth Farmer Pre-Sale Calculator</title>
<style>
  :root {
    --paper: #FFFFFF;
    --card: #FFFFFF;
    --ink: #2A241D;
    --muted: #6B675E;
    --rule: #C9CEBF;
    --leaf: #3E6A33;
    --leaf-soft: #DCE6D3;
    --focus: #3E6A33;
    --shadow: 0 .0625rem .125rem rgba(42, 36, 29, .06), 0 .375rem 1.125rem rgba(42, 36, 29, .10);
    --panel: rgba(62, 106, 51, .06);
    --pill: #E8F4BC;
    --pill-ink: #2F5A22;
    --pill-rule: #C6DD7E;
    box-sizing: border-box;
    padding-top: env(safe-area-inset-top, 0rem);
    padding-bottom: env(safe-area-inset-bottom, 0rem);
    color-scheme: light;
  }
  @media (prefers-color-scheme: dark) {
    :root:not([data-theme="light"]) {
      --paper: #1C1A16;
      --card: #25221D;
      --ink: #ECE8DF;
      --muted: #A8A397;
      --rule: #47423A;
      --leaf: #93BD7F;
      --leaf-soft: #2F3A28;
      --focus: #93BD7F;
    --shadow: 0 .0625rem .125rem rgba(0, 0, 0, .30), 0 .375rem 1.125rem rgba(0, 0, 0, .35);
    --panel: rgba(147, 189, 127, .08);
    --pill: #3A4721;
    --pill-ink: #D6EBA2;
    --pill-rule: #5A7030;
      color-scheme: dark;
    }
  }
  :root[data-theme="dark"] {
    --paper: #1C1A16;
    --card: #25221D;
    --ink: #ECE8DF;
    --muted: #A8A397;
    --rule: #47423A;
    --leaf: #93BD7F;
    --leaf-soft: #2F3A28;
    --focus: #93BD7F;
    --shadow: 0 .0625rem .125rem rgba(0, 0, 0, .30), 0 .375rem 1.125rem rgba(0, 0, 0, .35);
    --panel: rgba(147, 189, 127, .08);
    --pill: #3A4721;
    --pill-ink: #D6EBA2;
    --pill-rule: #5A7030;
    color-scheme: dark;
  }
  *, *::before, *::after { box-sizing: inherit; }
  html { scroll-padding-top: env(safe-area-inset-top, 0rem); }
  body {
    margin: 0;
    background: var(--paper);
    color: var(--ink);
    font-family: sans-serif;
    font-size: 0.8rem;
    line-height: 1.45;
    font-variant-numeric: tabular-nums;
    -webkit-font-smoothing: antialiased;
  }
  .wrap {
    max-width: 62rem;
    margin: 0 auto;
    padding: clamp(1rem, 3.2vw, 2.4rem) clamp(1rem, 4vw, 2.5rem) 2.4rem;
  }
  header { margin-bottom: clamp(1.2rem, 3.2vw, 2rem); }
  .brand {
    margin: 0 0 .28rem;
    font-weight: 600;
    color: var(--leaf);
    font-size: 0.76rem;
  }
  h1 {
    margin: 0;
    color: var(--pill-ink);
    font-weight: 800;
    font-size: clamp(1.52rem, 4.4vw, 2.48rem);
    line-height: 1.02;
    letter-spacing: -0.01em;
  }
  .season {
    margin: .4rem 0 0;
    color: var(--muted);
    font-size: 0.84rem;
  }

  [hidden] { display: none !important; }

  /* Truckload deals: one card, each deal a checkbox label */
  .deals { margin: 0 0 clamp(1.4rem, 3.2vw, 2.2rem); }
  .deals-head {
    margin: 0 0 .55rem;
    border-bottom: .09375rem solid var(--pill-rule);
  }
  .deals h2 {
    display: inline-block;
    vertical-align: bottom;
    margin: 0;
    padding: .27rem .576rem .225rem;
    border-radius: .25rem .25rem 0 0;
    background: var(--pill);
    color: var(--pill-ink);
    font-size: .576rem;
    font-weight: 700;
    text-transform: uppercase;
    letter-spacing: .005rem;
  }
  .section-h { margin: 0 0 .6rem; font-size: 1.21rem; font-weight: 700; }
  .sr-only { position: absolute; width: .0625rem; height: .0625rem; overflow: hidden; clip: rect(0 0 0 0); white-space: nowrap; }
  .deal-grid { display: grid; gap: .58rem .72rem; }
  @media (min-width: 40rem) {
    .deal-grid { grid-template-columns: 1fr 1fr; }
  }
  .deal {
    display: grid;
    grid-template-columns: auto 1fr;
    gap: .7rem;
    padding: .64rem .88rem .67rem;
    background: var(--panel);
    border-radius: .25rem;
    cursor: pointer;
  }
  .deal:hover { background: color-mix(in srgb, var(--leaf-soft) 70%, transparent); }
  .deal:has(input:checked) { background: var(--leaf-soft); }
  .deal input {
    width: 1.08rem;
    height: 1.08rem;
    margin: .02rem 0 0;
    accent-color: var(--leaf);
    cursor: pointer;
  }
  .deal input:focus-visible { outline: .1875rem solid var(--focus); outline-offset: .1875rem; }
  .deal .body { display: flex; flex-direction: column; gap: .26rem; min-width: 0; }
  .deal .title { font-size: .832rem; line-height: 1.25; }
  .deal .name { font-weight: 800; }
  .deal .sep { margin: 0 .4em; color: var(--muted); }
  .deal .desc { font-weight: 700; }
  .deal .perk { font-size: 0.736rem; color: color-mix(in srgb, var(--muted) 70%, var(--ink)); }
  .deal .offer {
    display: flex; justify-content: space-between; align-items: baseline; gap: .8rem;
    margin-top: auto;
    padding-top: .2rem;
  }
  .deal .offer strong { color: var(--leaf); font-weight: 800; font-size: .8rem; }
  .deal .rate { color: color-mix(in srgb, var(--muted) 70%, var(--ink)); white-space: nowrap; font-weight: 600; }

  .perk-line { margin: .36rem 0 0; color: var(--leaf); font-weight: 600; font-size: 0.76rem; }

  .grid {
    display: grid;
    gap: clamp(1.2rem, 3.2vw, 2.4rem) clamp(1.5rem, 4vw, 3rem);
    align-items: start;
  }
  @media (min-width: 47.5rem) {
    .grid { grid-template-columns: 1fr 1.05fr; }
  }

  /* Inputs */
  fieldset { border: 0; margin: 0 0 1rem; padding: 0; min-width: 0; }
  legend {
    font-weight: 700;
    font-size: 0.84rem;
    padding: 0;
    margin-bottom: .75rem;
  }
  .qty {
    display: grid;
    grid-template-columns: 1fr auto;
    align-items: center;
    gap: .75rem;
    padding: .68rem 0;
    border-top: .0625rem solid var(--rule);
  }
  .qty:last-child { border-bottom: .0625rem solid var(--rule); }
  .qty label { font-weight: 600; }
  .qty .sub { display: block; font-weight: 400; color: var(--muted); font-size: 0.72rem; }
  .field {
    display: flex;
    align-items: baseline;
    gap: .4rem;
  }
  .field input {
    width: 6.5rem;
    font: inherit;
    font-weight: 700;
    font-size: 1.2rem;
    text-align: right;
    color: var(--ink);
    background: var(--card);
    border: .125rem solid var(--rule);
    border-radius: .25rem;
    padding: .24rem .55rem;
    -moz-appearance: textfield;
  }
  .field input::-webkit-outer-spin-button,
  .field input::-webkit-inner-spin-button { -webkit-appearance: none; margin: 0; }
  .field input::placeholder { color: var(--muted); opacity: .6; }
  .field input:focus-visible { outline: .1875rem solid var(--focus); outline-offset: .125rem; border-color: var(--leaf); }
  .field .unit { color: var(--muted); font-size: 0.76rem; }

  .check {
    display: grid;
    grid-template-columns: auto 1fr auto;
    align-items: center;
    gap: .85rem;
    padding: .68rem .9rem;
    margin-bottom: .48rem;
    border: .125rem solid var(--rule);
    border-radius: .25rem;
    background: var(--card);
    cursor: pointer;
  }
  .check:has(input:checked) { border-color: var(--leaf); background: var(--leaf-soft); }
  .check input {
    width: 1.35rem;
    height: 1.35rem;
    margin: 0;
    accent-color: var(--leaf);
    cursor: pointer;
  }
  .check input:focus-visible { outline: .1875rem solid var(--focus); outline-offset: .1875rem; }
  .check .text { font-weight: 600; }
  .check .off { color: var(--leaf); font-weight: 700; white-space: nowrap; }

  .fine {
    color: var(--muted);
    font-size: 0.704rem;
    max-width: 34rem;
    margin: 1rem 0 0;
  }

  /* Results label */
  .label {
    background: var(--card);
    border: .125rem solid var(--rule);
    border-radius: .25rem;
    box-shadow: var(--shadow);
    padding: 1.6rem 1.15rem 1.76rem;
  }
  .label h2 {
    margin: 0;
    font-size: 0.8rem;
    font-weight: 700;
  }
  .total {
    margin: .16rem 0 0;
    font-weight: 800;
    font-size: clamp(1.84rem, 5.6vw, 2.56rem);
    line-height: 1.05;
    letter-spacing: -0.015em;
    overflow-wrap: anywhere;
  }
  .meta { margin: .24rem 0 0; color: var(--muted); font-size: 0.76rem; }
  .bar { height: .125rem; background: var(--rule); margin: .72rem -1.15rem .16rem; }
  .rows { margin: 0; padding: 0; list-style: none; }
  .row {
    display: flex;
    justify-content: space-between;
    align-items: baseline;
    gap: 1rem;
    padding: .36rem 0;
    border-bottom: .0625rem solid var(--rule);
  }
  .row:last-child { border-bottom: 0; }
  .row.head { font-weight: 700; border-bottom-color: var(--ink); }
  .row .v { font-weight: 600; text-align: right; white-space: nowrap; }
  .row.big .v { font-weight: 800; font-size: 1.08rem; }
  .row.sum { font-weight: 700; border-top: .125rem solid var(--ink); }
  .row.dim { color: var(--muted); }
  .row .note { color: var(--muted); font-weight: 400; font-size: 0.704rem; }
  .row.save .v { color: var(--leaf); font-weight: 800; font-size: 0.92rem; }

  .hint {
    margin: .72rem 0 0;
    font-size: 0.76rem;
    color: var(--ink);
    min-height: 1.4em;
  }
  .hint strong { color: var(--leaf); }

  @media (prefers-reduced-motion: no-preference) {
    .total { transition: color .15s ease; }
  }
</style>
</head>
<body>
<div class="wrap">
  <header>
    <h1>Tilth Farmer Pre-Sale Calculator</h1>
    <p class="season">2026–27 season</p>
  </header>

  <section class="deals" aria-labelledby="deals-h">
    <div class="deals-head"><h2 id="deals-h">Cool Deals • Paid and Shipped by Jan&nbsp;1</h2></div>
    <div class="deal-grid">
      <label class="deal">
        <input type="checkbox" data-deal="lbt">
        <span class="body">
          <span class="title"><span class="name">Little Big Truck</span><span class="sep" aria-hidden="true">•</span><span class="desc">16 yd³ in super sacks</span></span>
          <span class="perk">Free liftgate, appointment, or limited-access delivery</span>
          <span class="offer"><strong>25% off</strong><span class="rate" id="lbtRate"></span></span>
        </span>
      </label>
      <label class="deal">
        <input type="checkbox" data-deal="bbt">
        <span class="body">
          <span class="title"><span class="name">Big Big Truck</span><span class="sep" aria-hidden="true">•</span><span class="desc">60 yd³ in 48 extra-filled sacks</span></span>
          <span class="perk">Best material price, with freight spread across a full load</span>
          <span class="offer"><strong>40% off</strong><span class="rate" id="bbtRate"></span></span>
        </span>
      </label>
    </div>
  </section>

  <h2 class="section-h" id="order-h">Roll Your Own Deal</h2>
  <div class="grid">
    <section aria-labelledby="order-h">

      <fieldset>
        <legend class="sr-only">How much material?</legend>
        <div class="qty">
          <label for="sack">Sacked<span class="sub">$320 per cubic yard list</span></label>
          <div class="field">
            <input id="sack" type="number" inputmode="decimal" min="0" step="1" value="" placeholder="0" aria-describedby="sack-unit">
            <span class="unit" id="sack-unit">yd³</span>
          </div>
        </div>
        <div class="qty">
          <label for="bag">Bagged<span class="sub">$392 per cubic yard list</span></label>
          <div class="field">
            <input id="bag" type="number" inputmode="decimal" min="0" step="1" value="" placeholder="0" aria-describedby="bag-unit">
            <span class="unit" id="bag-unit">yd³</span>
          </div>
        </div>
      </fieldset>

      <fieldset>
        <legend class="sr-only">Early discounts</legend>
        <label class="check">
          <input id="paid" type="checkbox">
          <span class="text">Payment before Jan 1</span>
          <span class="off">4% off</span>
        </label>
        <label class="check">
          <input id="shipped" type="checkbox">
          <span class="text">Material received before Jan 1</span>
          <span class="off">4% off</span>
        </label>
      </fieldset>

      <p class="fine">Volume discount is based on total yards, sacked and bagged combined. Early discounts add to the volume discount. One cubic yard is 27 cubic feet.</p>
    </section>

    <section class="label" aria-labelledby="res-h" aria-live="polite">
      <h2 id="res-h">Total after discounts</h2>
      <p class="total" id="total">$0.00</p>
      <p class="meta" id="meta">Enter yards to see your price</p>
      <p class="perk-line" id="perkLine" hidden></p>

      <div class="bar"></div>
      <ul class="rows">
        <li class="row head"><span>Price per cubic foot</span><span class="v"></span></li>
        <li class="row big" id="sackRow"><span>Sacked</span><span class="v" id="sackCf">$0.00</span></li>
        <li class="row big" id="bagRow"><span>Bagged</span><span class="v" id="bagCf">$0.00</span></li>
      </ul>

      <div class="bar thin"></div>
      <ul class="rows">
        <li class="row head"><span>Discounts</span><span class="v"></span></li>
        <li class="row"><span>Volume <span class="note" id="volNote"></span></span><span class="v" id="volPct">0%</span></li>
        <li class="row" id="paidRow"><span>Payment before Jan 1</span><span class="v" id="paidPct">0%</span></li>
        <li class="row" id="shipRow"><span>Received before Jan 1</span><span class="v" id="shipPct">0%</span></li>
        <li class="row" id="dealRow" hidden><span id="dealName"></span><span class="v" id="dealPct"></span></li>
        <li class="row sum"><span>Total discount</span><span class="v" id="totPct">0%</span></li>
        <li class="row save"><span>You save</span><span class="v" id="save">$0.00</span></li>
      </ul>

      <p class="hint" id="hint"></p>
    </section>
  </div>
</div>

<script>
  // Pricing from Farm_Pre_Sale_26-27.xlsx
  const PRICE = { sack: 320, bag: 392 };          // $ per cubic yard, list
  const TIERS = [                                  // [minimum total yards, volume discount]
    [1, 0], [4, 0.04], [8, 0.08], [12, 0.12],
    [16, 0.16], [24, 0.20], [36, 0.28], [48, 0.32]
  ];
  const TIMING = 0.04;                             // each early discount
  const CF_PER_YD = 27;

  // Truckload deals. A deal is active whenever the order matches it.
  // Checkbox fields left undefined are not part of the deal.
  const DEALS = {
    lbt: {
      name: 'Little Big Truck', sack: 16, bag: 0, paid: true, shipped: true, flat: 0.25,
      perk: 'Includes free liftgate, appointment, or limited-access delivery.'
    },
    bbt: {
      name: 'Big Big Truck', sack: 60, bag: 0, paid: true, shipped: true,
      perk: '48 sacks at 1.25 yd³ each, on one semi.'
    }
  };

  const $ = id => document.getElementById(id);
  const usd = new Intl.NumberFormat('en-US', { style: 'currency', currency: 'USD', minimumFractionDigits: 2, maximumFractionDigits: 2 });
  const pct = n => (Math.round(n * 1000) / 10) + '%';
  const yd = n => (Math.round(n * 100) / 100).toLocaleString('en-US');

  function num(el) {
    const v = parseFloat(el.value);
    return Number.isFinite(v) && v > 0 ? v : 0;
  }

  function volumeDiscount(total) {
    let d = 0;
    for (const [min, disc] of TIERS) if (total >= min) d = disc;
    return d;
  }

  function nextTier(total) {
    const current = volumeDiscount(total);
    return TIERS.find(([min, disc]) => min > total && disc > current) || null;
  }

  function readState() {
    return { sack: num($('sack')), bag: num($('bag')), paid: $('paid').checked, shipped: $('shipped').checked };
  }
  function readRaw() {
    return { sack: $('sack').value, bag: $('bag').value, paid: $('paid').checked, shipped: $('shipped').checked };
  }
  function writeRaw(r) {
    $('sack').value = r.sack; $('bag').value = r.bag;
    $('paid').checked = r.paid; $('shipped').checked = r.shipped;
  }
  function matches(d, s) {
    return s.sack === d.sack && s.bag === d.bag &&
      (d.paid === undefined || s.paid === d.paid) &&
      (d.shipped === undefined || s.shipped === d.shipped);
  }
  function activeDeal(s) {
    return Object.keys(DEALS).find(k => matches(DEALS[k], s)) || null;
  }

  // Order as it was before a deal was applied, so clearing the deal restores it
  let snapshot = null;

  function update() {
    const state = readState();
    const { sack, bag, paid, shipped } = state;
    const total = sack + bag;

    const dealKey = activeDeal(state);
    const deal = dealKey ? DEALS[dealKey] : null;
    if (!deal) snapshot = null;

    const vol = volumeDiscount(total);
    let disc = vol + (paid ? TIMING : 0) + (shipped ? TIMING : 0);
    const bonus = deal && deal.flat ? Math.max(0, deal.flat - disc) : 0;
    disc += bonus;

    document.querySelectorAll('input[data-deal]').forEach(box => {
      box.checked = box.dataset.deal === dealKey;
    });
    $('perkLine').hidden = !deal;
    $('perkLine').textContent = deal ? deal.perk : '';
    $('dealRow').hidden = bonus <= 0;
    $('dealName').textContent = deal ? `${deal.name} deal` : '';
    $('dealPct').textContent = pct(bonus);
    const list = sack * PRICE.sack + bag * PRICE.bag;
    const net = list * (1 - disc);

    $('total').textContent = usd.format(net);
    $('meta').textContent = total > 0
      ? `${yd(total)} yd³ total, list price ${usd.format(list)}`
      : 'Enter yards to see your price';

    $('sackCf').textContent = usd.format(PRICE.sack * (1 - disc) / CF_PER_YD);
    $('bagCf').textContent = usd.format(PRICE.bag * (1 - disc) / CF_PER_YD);
    $('sackRow').classList.toggle('dim', sack === 0 && total > 0);
    $('bagRow').classList.toggle('dim', bag === 0 && total > 0);

    $('volNote').textContent = total > 0 ? `(${yd(total)} yd³)` : '';
    $('volPct').textContent = pct(vol);
    $('paidPct').textContent = pct(paid ? TIMING : 0);
    $('shipPct').textContent = pct(shipped ? TIMING : 0);
    $('paidRow').classList.toggle('dim', !paid);
    $('shipRow').classList.toggle('dim', !shipped);
    $('totPct').textContent = pct(disc);
    $('save').textContent = usd.format(list - net);

    const nt = nextTier(total);
    const hint = $('hint');
    if (nt) {
      const more = Math.ceil((nt[0] - total) * 100) / 100;
      hint.innerHTML = `Add <strong>${yd(more)} yd³</strong> to reach the ${pct(nt[1])} volume discount.`;
    } else {
      hint.textContent = 'This order is at the top volume discount.';
    }
  }

  ['sack', 'bag'].forEach(id => {
    $(id).addEventListener('input', update);
    $(id).addEventListener('focus', e => e.target.select());
  });
  ['paid', 'shipped'].forEach(id => $(id).addEventListener('change', update));

  // The order fields haven't changed yet when this fires, so activeDeal still reflects the prior state
  document.querySelectorAll('input[data-deal]').forEach(box => box.addEventListener('change', () => {
    const key = box.dataset.deal;
    const current = activeDeal(readState());
    if (current === key) {
      writeRaw(snapshot || { sack: '', bag: '', paid: false, shipped: false });
      snapshot = null;
    } else {
      if (!current) snapshot = readRaw();
      const d = DEALS[key];
      writeRaw({
        sack: d.sack ? String(d.sack) : '', bag: d.bag ? String(d.bag) : '',
        paid: d.paid ?? $('paid').checked,
        shipped: d.shipped ?? $('shipped').checked
      });
    }
    update();
  }));

  // Per-cubic-foot price shown on each deal card
  $('lbtRate').textContent = usd.format(PRICE.sack * (1 - DEALS.lbt.flat) / CF_PER_YD) + '/cu ft';
  $('bbtRate').textContent = usd.format(PRICE.sack * (1 - volumeDiscount(DEALS.bbt.sack) - 2 * TIMING) / CF_PER_YD) + '/cu ft';

  update();
</script>
</body>
</html>

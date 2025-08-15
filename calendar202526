<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Sumegh Holidays – 1‑Year Travel Calendar</title>
  <style>
    :root{
      --primary:#2957A0; /* Brand Blue */
      --accent:#DC3027;  /* Accent Red for Fixed Departures */
      --highlight:#FCB615; /* Highlight Yellow for Events */
      --ink:#1b2430;
      --muted:#6b7280;
      --bg:#f7f8fb;
      --card:#ffffff;
      --ring:rgba(41,87,160,0.15);
    }
    *{box-sizing:border-box}
    html,body{margin:0;padding:0;font-family:system-ui,-apple-system,Segoe UI,Roboto,Ubuntu,"Helvetica Neue",Arial,"Noto Sans",sans-serif;background:var(--bg);color:var(--ink)}
    header{
      position:sticky;top:0;z-index:10;background:linear-gradient(90deg,var(--primary),#1f3f77);
      color:white;padding:20px;border-bottom:4px solid var(--highlight);
      box-shadow:0 6px 20px rgba(0,0,0,.12)
    }
    .wrap{max-width:1200px;margin:0 auto;padding:20px}
    .brand{display:flex;align-items:center;gap:14px;flex-wrap:wrap}
    .logo{
      width:44px;height:44px;border-radius:12px;background:white;color:var(--primary);
      display:grid;place-items:center;font-weight:800;box-shadow:0 4px 14px rgba(0,0,0,.2)
    }
    h1{font-size:clamp(20px,3.2vw,28px);margin:0}
    .sub{opacity:.9;font-size:14px;margin-top:4px}

    .legend{display:flex;flex-wrap:wrap;gap:10px;margin-top:14px}
    .pill{display:inline-flex;align-items:center;gap:8px;background:rgba(255,255,255,.2);border:1px solid rgba(255,255,255,.35);padding:6px 10px;border-radius:999px;font-size:12px}
    .dot{width:10px;height:10px;border-radius:50%}
    .dot.blue{background:var(--primary)}
    .dot.red{background:var(--accent)}
    .dot.yellow{background:var(--highlight)}

    .grid{display:grid;grid-template-columns:repeat(1,1fr);gap:18px}
    @media (min-width:720px){.grid{grid-template-columns:repeat(2,1fr)}}
    @media (min-width:1024px){.grid{grid-template-columns:repeat(3,1fr)}}

    .card{background:var(--card);border-radius:18px;box-shadow:0 8px 30px rgba(31,63,119,.08);
          border:1px solid var(--ring);overflow:hidden;display:flex;flex-direction:column}
    .card header{position:relative;background:linear-gradient(135deg,rgba(41,87,160,.95),rgba(41,87,160,.7));
                 padding:16px 18px;border:0;border-bottom:3px solid var(--highlight)}
    .card header h2{margin:0;color:white;font-size:18px;letter-spacing:.4px}
    .section{padding:14px 18px;border-top:1px dashed #e8ecf5}
    .label{font-size:12px;text-transform:uppercase;letter-spacing:.12em;color:var(--muted);margin-bottom:6px}
    .list{display:flex;flex-wrap:wrap;gap:8px}
    .chip{font-size:12px;padding:6px 10px;border-radius:999px;background:#eef3fb;color:#1f3468;border:1px solid var(--ring)}
    .items{display:flex;flex-direction:column;gap:10px}
    .item{display:flex;gap:10px;align-items:flex-start}
    .badge{flex:0 0 auto;font-size:11px;font-weight:700;letter-spacing:.06em;color:#fff;background:var(--accent);padding:5px 8px;border-radius:7px}
    .badge.event{background:var(--highlight);color:#111}
    .text{font-size:14px;line-height:1.4}

    footer.note{max-width:900px;margin:28px auto 40px;color:var(--muted);font-size:13px;text-align:center}

    /* Print styles */
    @media print{
      header{position:static}
      .grid{grid-template-columns:repeat(2,1fr)}
      .card{break-inside:avoid-page}
      body{background:#fff}
    }

    /* Tiny helper */
    .toolbar{display:flex;flex-wrap:wrap;gap:10px;margin:14px 0}
    .btn{background:#fff;border:1px solid var(--ring);padding:8px 12px;border-radius:10px;cursor:pointer}
  </style>
</head>
<body>
  <header>
    <div class="wrap">
      <div class="brand">
        <div class="logo">SH</div>
        <div>
          <h1>Sumegh Holidays • 1‑Year Travel Calendar</h1>
          <div class="sub">Best travel months • Fixed departures • Major world events (editable)</div>
          <div class="legend">
            <span class="pill"><span class="dot blue"></span> Best destinations this month</span>
            <span class="pill"><span class="dot red"></span> Fixed departure</span>
            <span class="pill"><span class="dot yellow"></span> Festival / Event</span>
          </div>
        </div>
      </div>
    </div>
  </header>

  <main class="wrap">
    <div class="toolbar">
      <button class="btn" onclick="window.print()">🖨️ Print / Save as PDF</button>
    </div>
    <section class="grid" id="calendarGrid" aria-live="polite"></section>
  </main>

  <footer class="note">
    Tip: Edit the data inside <strong>calendarData</strong> in the HTML to update destinations, fixed departures and events. Colors use your brand palette: <code>#2957A0</code>, <code>#DC3027</code>, <code>#FCB615</code>.
  </footer>

  <script>
    // === EDITABLE DATA START ===
    // Update these arrays to change content quickly.
    const bestByMonth = {
      "January":   ["Maldives","Dubai","Thailand"],
      "February":  ["Vietnam","Cambodia","Sri Lanka"],
      "March":     ["Japan (Sakura)","Nepal Trekking"],
      "April":     ["Japan (Sakura)","Netherlands (Tulips)","Spain"],
      "May":       ["Bali","Turkey","Greece"],
      "June":      ["Switzerland","Italy","Canada"],
      "July":      ["Europe (cooler regions)","South Africa"],
      "August":    ["Kenya Safari","Indonesia"],
      "September": ["Dubai","Bhutan","China"],
      "October":   ["Japan (Autumn)","Maldives"],
      "November":  ["Thailand","Vietnam","Cambodia"],
      "December":  ["Australia","New Zealand","South Africa"]
    };

    // Fixed departures you provided (no year locked, repeats annually)
    const fixedDepartures = [
      { month:"July",   when:"Mid July", label:"Europe – 5 Countries (FR/IT/DE/CH/ES)" },
      { month:"September", date:"27 Sep", label:"Dubai" },
      { month:"October",   date:"03 Oct", label:"Bali + Singapore" },
      { month:"November",  when:"Mid Nov", label:"Thailand" },
      // Sakura season callout appears as an event for Mar/Apr below
    ];

    // Festivals / major events (kept generic so they remain valid each year)
    const events = [
      { month:"March",  label:"Japan – Sakura Season (dates vary)" },
      { month:"April",  label:"Japan – Sakura Season (dates vary)" },
      { month:"October",label:"Dashain (Nepal)" },
      { month:"November",label:"Tihar (Nepal)" }
    ];
    // === EDITABLE DATA END ===

    const months = [
      "January","February","March","April","May","June",
      "July","August","September","October","November","December"
    ];

    const grid = document.getElementById("calendarGrid");

    function render(){
      grid.innerHTML = "";
      months.forEach(m => {
        const card = document.createElement('article');
        card.className = 'card';

        const head = document.createElement('header');
        head.innerHTML = `<h2>${m}</h2>`;
        card.appendChild(head);

        // Best Destinations
        const best = document.createElement('div');
        best.className = 'section';
        best.innerHTML = `<div class="label">Best destinations</div>`;
        const list = document.createElement('div');
        list.className = 'list';
        (bestByMonth[m]||[]).forEach(x=>{
          const chip = document.createElement('span');
          chip.className = 'chip';
          chip.textContent = x;
          list.appendChild(chip);
        });
        best.appendChild(list);
        card.appendChild(best);

        // Fixed Departures
        const fx = (fixedDepartures||[]).filter(f=>f.month===m);
        const ev = (events||[]).filter(e=>e.month===m);

        if(fx.length){
          const sec = document.createElement('div');
          sec.className = 'section';
          sec.innerHTML = `<div class="label">Fixed departures</div>`;
          const items = document.createElement('div');
          items.className = 'items';
          fx.forEach(f=>{
            const row = document.createElement('div');
            row.className = 'item';
            const badge = document.createElement('span');
            badge.className = 'badge';
            badge.textContent = f.date? f.date : (f.when||'');
            const txt = document.createElement('div');
            txt.className = 'text';
            txt.textContent = f.label;
            row.appendChild(badge);
            row.appendChild(txt);
            items.appendChild(row);
          });
          sec.appendChild(items);
          card.appendChild(sec);
        }

        // Events / Festivals
        if(ev.length){
          const sec = document.createElement('div');
          sec.className = 'section';
          sec.innerHTML = `<div class="label">Festivals & events</div>`;
          const items = document.createElement('div');
          items.className = 'items';
          ev.forEach(e=>{
            const row = document.createElement('div');
            row.className = 'item';
            const badge = document.createElement('span');
            badge.className = 'badge event';
            badge.textContent = 'INFO';
            const txt = document.createElement('div');
            txt.className = 'text';
            txt.textContent = e.label;
            row.appendChild(badge);
            row.appendChild(txt);
            items.appendChild(row);
          });
          sec.appendChild(items);
          card.appendChild(sec);
        }

        grid.appendChild(card);
      });
    }

    render();
  </script>
</body>
</html>

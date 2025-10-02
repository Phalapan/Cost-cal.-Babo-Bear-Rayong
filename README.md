# Cost-cal.-Babo-Bear-Rayong
<!doctype html>
<html lang="th">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>เครื่องคิดต้นทุน ร้านชานมไข่มุก</title>
  <style>
    :root{--bg:#0f1724;--card:#0b1220;--accent:#f59e0b;--muted:#94a3b8;--glass:rgba(255,255,255,0.03)}
    *{box-sizing:border-box;font-family:Inter,ui-sans-serif,system-ui,Segoe UI,Roboto,'Helvetica Neue',Arial}
    body{margin:0;background:linear-gradient(180deg,#071024 0%,#071826 100%);color:#e6eef8;padding:28px}
    .container{max-width:980px;margin:0 auto}
    header{display:flex;align-items:center;gap:16px}
    h1{margin:0;font-size:20px}
    .card{background:var(--card);border-radius:12px;padding:18px;margin-top:18px;box-shadow:0 6px 18px rgba(2,6,23,0.6)}
    form .row{display:flex;gap:12px;align-items:center;margin-bottom:12px}
    label{min-width:130px;color:var(--muted);font-size:14px}
    input[type=number]{flex:1;padding:8px;border-radius:8px;border:1px solid rgba(255,255,255,0.06);background:var(--glass);color:inherit}
    .unit{width:130px;text-align:right;color:var(--muted);font-size:14px}
    .totals{display:flex;gap:12px;flex-wrap:wrap;margin-top:12px}
    .big{font-size:22px;font-weight:700}
    .muted{color:var(--muted)}
    .pill{background:linear-gradient(90deg,rgba(255,255,255,0.02),rgba(255,255,255,0.01));padding:12px;border-radius:10px}
    .dashboard{margin-top:14px;display:grid;grid-template-columns:repeat(auto-fit,minmax(160px,1fr));gap:12px}
    .bar{height:10px;background:rgba(255,255,255,0.06);border-radius:6px;overflow:hidden}
    .bar > i{display:block;height:100%;background:linear-gradient(90deg,var(--accent),#ffb86b)}
    footer{margin-top:18px;color:var(--muted);font-size:13px}
    .controls{display:flex;gap:8px;justify-content:flex-end;margin-top:12px}
    button{background:var(--accent);border:none;padding:10px 14px;border-radius:10px;color:#072033;font-weight:700;cursor:pointer}
    @media(max-width:720px){.row{flex-direction:column;align-items:flex-start}.unit{width:100%;text-align:left}}
  </style>
</head>
<body>
  <div class="container">
    <header>
      <div>
        <h1>เครื่องคิดต้นทุน ร้านชานมไข่มุก</h1>
        <div class="muted">กรอกจำนวน / ราคาต้นทุน แล้วกดคำนวณ</div>
      </div>
      <div style="margin-left:auto;text-align:right">
        <div id="today" class="muted"></div>
      </div>
    </header>

    <div class="card">
      <form id="costForm" onsubmit="return false;">
        <!-- ชา -->
        <div class="row">
          <label>ชา (ขวด)</label>
          <input type="number" id="qtyTea" min="0" step="1" value="0" />
          <div class="unit">ราคา/ขวด: 12 ฿</div>
          <div id="teaTotal" class="unit">0 ฿</div>
        </div>

        <!-- ชีส -->
        <div class="row">
          <label>ชีส (ราคา)</label>
          <input type="number" id="priceCheese" min="0" step="0.01" value="0" />
          <div class="unit">฿</div>
          <div id="cheeseTotal" class="unit">0 ฿</div>
        </div>

        <!-- น้ำแข็ง (ใส่ราคาเลย) -->
        <div class="row">
          <label>น้ำแข็ง (ราคา)</label>
          <input type="number" id="priceIce" min="0" step="0.01" value="0" />
          <div class="unit">฿</div>
          <div id="iceTotal" class="unit">0 ฿</div>
        </div>

        <!-- ไข่มุก -->
        <div class="row">
          <label>ไข่มุก (กก.)</label>
          <input type="number" id="qtyPearl" min="0" step="0.01" value="0" />
          <div class="unit">ราคา/กก.: 60 ฿</div>
          <div id="pearlTotal" class="unit">0 ฿</div>
        </div>

        <!-- ค่าที่ (ราคา) -->
        <div class="row">
          <label>ค่าที่ (ราคา)</label>
          <input type="number" id="priceRent" min="0" step="0.01" value="0" />
          <div class="unit">฿</div>
          <div id="rentTotal" class="unit">0 ฿</div>
        </div>

        <!-- นมสด -->
        <div class="row">
          <label>นมสด (ขวด)</label>
          <input type="number" id="qtyMilk" min="0" step="1" value="0" />
          <div class="unit">ราคา/ขวด: 100 ฿</div>
          <div id="milkTotal" class="unit">0 ฿</div>
        </div>

        <!-- แก้ว -->
        <div class="row">
          <label>แก้ว (ใบ)</label>
          <input type="number" id="qtyCup" min="0" step="1" value="0" />
          <div class="unit">ราคา/ใบ: 3 ฿</div>
          <div id="cupTotal" class="unit">0 ฿</div>
        </div>

        <!-- บุกบราว์ -->
        <div class="row">
          <label>บุกบราว์ (ราคา)</label>
          <input type="number" id="priceBrown" min="0" step="0.01" value="0" />
          <div class="unit">฿</div>
          <div id="brownTotal" class="unit">0 ฿</div>
        </div>

        <!-- ไมโล -->
        <div class="row">
          <label>ไมโล (ราคา)</label>
          <input type="number" id="priceMilo" min="0" step="0.01" value="0" />
          <div class="unit">฿</div>
          <div id="miloTotal" class="unit">0 ฿</div>
        </div>

        <!-- โกโก้ -->
        <div class="row">
          <label>โกโก้ (ราคา)</label>
          <input type="number" id="priceCocoa" min="0" step="0.01" value="0" />
          <div class="unit">฿</div>
          <div id="cocoaTotal" class="unit">0 ฿</div>
        </div>

        <div class="controls">
          <button id="calcBtn">คำนวณ</button>
          <button id="resetBtn" type="button">รีเซ็ต</button>
          <button id="downloadBtn" type="button">ดาวน์โหลด CSV</button>
        </div>

        <div class="totals">
          <div class="pill" style="flex:1">
            <div class="muted">รวมต้นทุนทั้งหมด</div>
            <div id="grandTotal" class="big">0 ฿</div>
          </div>

          <div class="pill" style="width:220px">
            <div class="muted">วันที่</div>
            <div id="dateNow" class="big"></div>
          </div>
        </div>

      </form>

      <div class="card" style="margin-top:16px">
        <h3 style="margin-top:0">Dashboard: สรุปตามรายการ</h3>
        <div id="dashArea" class="dashboard"></div>
      </div>

    </div>

    <footer class="muted">ออกแบบโดยเครื่องมือช่วย — สามารถบันทึก/แก้ไขช่องราคาได้เอง</footer>
  </div>

<script>
  const PRICE = { tea:12, pearl:60, milk:100, cup:3 };
  const nf = new Intl.NumberFormat('th-TH', { style:'currency', currency:'THB', maximumFractionDigits:2});
  function format(v){ return nf.format(v); }

  function getInputs(){
    return {
      tea: Number(document.getElementById('qtyTea').value) || 0,
      cheese: Number(document.getElementById('priceCheese').value) || 0,
      ice: Number(document.getElementById('priceIce').value) || 0,
      pearl: Number(document.getElementById('qtyPearl').value) || 0,
      rent: Number(document.getElementById('priceRent').value) || 0,
      milk: Number(document.getElementById('qtyMilk').value) || 0,
      cup: Number(document.getElementById('qtyCup').value) || 0,
      brown: Number(document.getElementById('priceBrown').value) || 0,
      milo: Number(document.getElementById('priceMilo').value) || 0,
      cocoa: Number(document.getElementById('priceCocoa').value) || 0
    }
  }

  function calc(){
    const i = getInputs();
    const tTea = i.tea * PRICE.tea;
    const tCheese = i.cheese;
    const tIce = i.ice;
    const tPearl = i.pearl * PRICE.pearl;
    const tRent = i.rent;
    const tMilk = i.milk * PRICE.milk;
    const tCup = i.cup * PRICE.cup;
    const tBrown = i.brown;
    const tMilo = i.milo;
    const tCocoa = i.cocoa;

    const grand = tTea + tCheese + tIce + tPearl + tRent + tMilk + tCup + tBrown + tMilo + tCocoa;

    document.getElementById('teaTotal').textContent = format(tTea);
    document.getElementById('cheeseTotal').textContent = format(tCheese);
    document.getElementById('iceTotal').textContent = format(tIce);
    document.getElementById('pearlTotal').textContent = format(tPearl);
    document.getElementById('rentTotal').textContent = format(tRent);
    document.getElementById('milkTotal').textContent = format(tMilk);
    document.getElementById('cupTotal').textContent = format(tCup);
    document.getElementById('brownTotal').textContent = format(tBrown);
    document.getElementById('miloTotal').textContent = format(tMilo);
    document.getElementById('cocoaTotal').textContent = format(tCocoa);
    document.getElementById('grandTotal').textContent = format(grand);

    renderDashboard({tea:tTea,cheese:tCheese,ice:tIce,pearl:tPearl,rent:tRent,milk:tMilk,cup:tCup,brown:tBrown,milo:tMilo,cocoa:tCocoa}, grand);
    return {items:{tea:tTea,cheese:tCheese,ice:tIce,pearl:tPearl,rent:tRent,milk:tMilk,cup:tCup,brown:tBrown,milo:tMilo,cocoa:tCocoa},grand}
  }

  function renderDashboard(items, grand){
    const container = document.getElementById('dashArea');
    container.innerHTML = '';
    for(const k of Object.keys(items)){
      const val = items[k];
      const perc = grand>0? (val/grand*100):0;
      const title = ({tea:'ชา',cheese:'ชีส',ice:'น้ำแข็ง',pearl:'ไข่มุก',rent:'ค่าที่',milk:'นมสด',cup:'แก้ว',brown:'บุกบราว์',milo:'ไมโล',cocoa:'โกโก้'})[k];

      const card = document.createElement('div'); card.className='pill';
      card.innerHTML = `<div style="display:flex;justify-content:space-between;align-items:center"><div class="muted">${title}</div><div style="font-weight:700">${format(val)}</div></div>
        <div style="margin-top:8px;font-size:13px;color:var(--muted);display:flex;gap:8px;align-items:center"><div class="bar" style="flex:1"><i style="width:${perc}%"></i></div><div>${perc.toFixed(1)}%</div></div>`;
      container.appendChild(card);
    }
  }

  function setToday(){
    const d = new Date();
    const dd = d.toLocaleDateString('th-TH');
    document.getElementById('dateNow').textContent = dd;
    document.getElementById('today').textContent = d.toLocaleString('th-TH', { weekday:'short', year:'numeric', month:'short', day:'numeric' });
  }

  function downloadCSV(data){
    const rows = [['รายการ','จำนวน/ราคา','รวม (฿)']];
    const inp = getInputs();
    rows.push(['ชา', inp.tea, data.items.tea.toFixed(2)]);
    rows.push(['ชีส','-', data.items.cheese.toFixed(2)]);
    rows.push(['น้ำแข็ง','-', data.items.ice.toFixed(2)]);
    rows.push(['ไข่มุก', inp.pearl, data.items.pearl.toFixed(2)]);
    rows.push(['ค่าที่','-', data.items.rent.toFixed(2)]);
    rows.push(['นมสด', inp.milk, data.items.milk.toFixed(2)]);
    rows.push(['แก้ว', inp.cup, data.items.cup.toFixed(2)]);
    rows.push(['บุกบราว์','-', data.items.brown.toFixed(2)]);
    rows.push(['ไมโล','-', data.items.milo.toFixed(2)]);
    rows.push(['โกโก้','-', data.items.cocoa.toFixed(2)]);
    rows.push(['รวม', '', data.grand.toFixed(2)]);
    rows.push(['วันที่','', new Date().toLocaleString('th-TH')]);

    const csv = rows.map(r => r.map(v=>`"${String(v).replace(/"/g,'""')}"`).join(',')).join('\n');
    const blob = new Blob([csv], {type:'text/csv;charset=utf-8;'});
    const url = URL.createObjectURL(blob);
    const a = document.createElement('a');
    a.href = url; a.download = `cost_summary_${(new Date()).toISOString().slice(0,10)}.csv`;
    document.body.appendChild(a); a.click(); a.remove(); URL.revokeObjectURL(url);
  }

  document.getElementById('calcBtn').addEventListener('click', ()=>{ downloadState = calc(); });
  document.getElementById('resetBtn').addEventListener('click', ()=>{
    ['qtyTea','priceCheese','priceIce','qtyPearl','priceRent','qtyMilk','qtyCup','priceBrown','priceMilo','priceCocoa'].forEach(id=>document.getElementById(id).value = 0);
    calc();
  });
  let downloadState = calc();
  document.getElementById('downloadBtn').addEventListener('click', ()=>{ downloadCSV(downloadState); });

  ['qtyTea','priceCheese','priceIce','qtyPearl','priceRent','qtyMilk','qtyCup','priceBrown','priceMilo','priceCocoa'].forEach(id=>{
    document.getElementById(id).addEventListener('input', ()=>{ downloadState = calc(); });
  });

  setToday();
  calc();
</script>
</body>
</html>

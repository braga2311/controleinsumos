[index (1).html](https://github.com/user-attachments/files/26488900/index.1.html)
<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Controle de Insumos</title>
<link href="https://fonts.googleapis.com/css2?family=DM+Sans:wght@400;500;600;700&family=DM+Mono:wght@400;500&display=swap" rel="stylesheet">
<style>
:root{
  --bg:#060c18;--bg2:#0a1225;--surface:#0f1d35;--surface2:#152540;--surface3:#1c304f;
  --border:rgba(96,148,255,0.13);--border2:rgba(96,148,255,0.26);
  --text:#e4ecfa;--text2:#7e9dc8;--text3:#3f5f8a;
  --accent:#3b82f6;--accent2:#60a5fa;--accent-bg:rgba(59,130,246,0.11);--accent-glow:rgba(59,130,246,0.28);
  --green:#22c55e;--green-bg:rgba(34,197,94,0.11);
  --yellow:#f59e0b;--yellow-bg:rgba(245,158,11,0.11);
  --red:#ef4444;--red-bg:rgba(239,68,68,0.11);
  --radius:13px;--radius-sm:8px;
}
*{box-sizing:border-box;margin:0;padding:0;-webkit-tap-highlight-color:transparent}
body{font-family:'DM Sans',sans-serif;background:var(--bg);color:var(--text);min-height:100dvh;display:flex;flex-direction:column;font-size:15px}
header{background:var(--bg2);border-bottom:1px solid var(--border);padding:11px 16px;position:sticky;top:0;z-index:100}
.hdr{max-width:760px;margin:0 auto;display:flex;align-items:center;justify-content:space-between;gap:10px}
.logo-area{display:flex;align-items:center;gap:10px}
.logo-box{width:36px;height:36px;background:linear-gradient(135deg,#1d4ed8,#3b82f6);border-radius:9px;display:flex;align-items:center;justify-content:center;flex-shrink:0;box-shadow:0 0 16px rgba(59,130,246,0.45)}
.logo-box svg{width:19px;height:19px;fill:white}
.app-title{font-size:15px;font-weight:700;color:var(--text)}
.app-sub{font-size:11px;color:var(--text3);font-family:'DM Mono',monospace}
.turno-pill{background:var(--accent-bg);border:1px solid var(--border2);color:var(--accent2);font-size:11px;font-weight:600;padding:4px 10px;border-radius:20px;font-family:'DM Mono',monospace;white-space:nowrap;flex-shrink:0}
.sync-bar{background:var(--surface);border-bottom:1px solid var(--border);padding:5px 16px;display:flex;align-items:center;justify-content:center;gap:8px;font-size:12px;color:var(--text3)}
.sdot{width:7px;height:7px;border-radius:50%;flex-shrink:0;transition:all .3s}
.sdot.ok{background:var(--green);box-shadow:0 0 6px var(--green)}
.sdot.err{background:var(--red)}
.sdot.load{background:var(--yellow);animation:blink 1s infinite}
@keyframes blink{0%,100%{opacity:1}50%{opacity:.35}}
main{flex:1;padding:14px 14px 90px;max-width:760px;width:100%;margin:0 auto}
.tab-bar{display:flex;gap:4px;background:var(--surface);border:1px solid var(--border);border-radius:var(--radius);padding:4px;margin-bottom:16px}
.tab-btn{flex:1;padding:8px 4px;border:none;background:none;border-radius:9px;font-family:'DM Sans',sans-serif;font-size:12px;font-weight:600;color:var(--text3);cursor:pointer;transition:all .15s;display:flex;flex-direction:column;align-items:center;gap:3px}
.tab-btn svg{width:18px;height:18px;stroke:currentColor;fill:none;stroke-width:2}
.tab-btn.active{background:var(--accent);color:#fff;box-shadow:0 2px 12px var(--accent-glow)}
.tab-btn:not(.active):hover{background:var(--surface2);color:var(--text)}
.strip{display:grid;grid-template-columns:repeat(3,1fr);gap:8px;margin-bottom:14px}
.stat{background:var(--surface);border:1px solid var(--border);border-radius:var(--radius-sm);padding:12px;text-align:center}
.stat .v{font-size:24px;font-weight:700;font-family:'DM Mono',monospace;line-height:1}
.stat .l{font-size:11px;color:var(--text3);margin-top:3px}
.grid{display:grid;grid-template-columns:repeat(2,1fr);gap:9px}
@media(min-width:480px){.grid{grid-template-columns:repeat(3,1fr)}}
@media(min-width:680px){.grid{grid-template-columns:repeat(4,1fr)}}
.ic{background:var(--surface);border:1.5px solid var(--border);border-radius:var(--radius);padding:13px 11px;cursor:pointer;transition:all .15s;position:relative;overflow:hidden}
.ic:hover{border-color:var(--accent);box-shadow:0 0 0 3px var(--accent-bg)}
.ic-dot{position:absolute;top:9px;right:9px;width:8px;height:8px;border-radius:50%;background:var(--green);box-shadow:0 0 6px var(--green)}
.ic.warn .ic-dot{background:var(--yellow);box-shadow:0 0 6px var(--yellow)}
.ic.crit .ic-dot{background:var(--red);box-shadow:0 0 6px var(--red)}
.ic-emoji{font-size:25px;display:block;margin-bottom:6px}
.ic-nome{font-size:12px;font-weight:600;color:var(--text);white-space:nowrap;overflow:hidden;text-overflow:ellipsis}
.ic-ref{font-size:10px;color:var(--text3);font-family:'DM Mono',monospace;margin-top:1px}
.ic-qty{font-size:22px;font-weight:700;font-family:'DM Mono',monospace;color:var(--accent2);margin-top:5px;line-height:1}
.ic.warn .ic-qty{color:var(--yellow)}
.ic.crit .ic-qty{color:var(--red)}
.ic-unit{font-size:11px;color:var(--text3)}
.card{background:var(--surface);border:1px solid var(--border);border-radius:var(--radius);padding:16px;margin-bottom:12px}
.card-title{font-size:11px;font-weight:700;color:var(--text3);text-transform:uppercase;letter-spacing:.6px;margin-bottom:13px}
.tipo-tog{display:grid;grid-template-columns:1fr 1fr;gap:6px;margin-bottom:14px}
.tipo-opt{padding:10px;border:1.5px solid var(--border);border-radius:var(--radius-sm);text-align:center;cursor:pointer;font-weight:600;font-size:14px;transition:all .15s;color:var(--text2)}
.tipo-opt.estoque.sel{background:var(--green-bg);border-color:rgba(34,197,94,.45);color:var(--green)}
.tipo-opt.expedicao.sel{background:var(--red-bg);border-color:rgba(239,68,68,.45);color:var(--red)}
.tipo-opt:not(.sel):hover{background:var(--surface2)}
.data-row{display:flex;align-items:center;gap:10px;background:var(--surface2);border:1px solid var(--border);border-radius:var(--radius-sm);padding:8px 12px;margin-bottom:12px}
.data-row label{font-size:12px;color:var(--text2);font-weight:600;flex-shrink:0}
.data-row input[type=date]{flex:1;background:transparent;border:none;color:var(--text);font-family:'DM Mono',monospace;font-size:14px;outline:none;min-width:0}
.data-row input[type=checkbox]{width:16px;height:16px;cursor:pointer;accent-color:var(--accent)}
.fg{margin-bottom:11px}
.fg label{display:block;font-size:11px;font-weight:700;color:var(--text3);margin-bottom:5px;text-transform:uppercase;letter-spacing:.5px}
.fg input,.fg select{width:100%;padding:10px 12px;border:1.5px solid var(--border);border-radius:var(--radius-sm);font-family:'DM Sans',sans-serif;font-size:15px;background:var(--surface2);color:var(--text);outline:none;transition:border-color .15s}
.fg input:focus,.fg select:focus{border-color:var(--accent);box-shadow:0 0 0 3px var(--accent-bg)}
.fg select option{background:#0a1225}
.fg input:disabled{background:var(--surface);color:var(--text3)}
.frow{display:grid;grid-template-columns:1fr 1fr;gap:9px}
.btn{display:inline-flex;align-items:center;justify-content:center;gap:6px;padding:10px 18px;border-radius:var(--radius-sm);border:none;font-family:'DM Sans',sans-serif;font-size:14px;font-weight:600;cursor:pointer;transition:all .15s}
.btn-p{background:var(--accent);color:#fff;box-shadow:0 2px 10px var(--accent-glow)}
.btn-p:hover{background:#2563eb}
.btn-p:active{transform:scale(.98)}
.btn-s{background:var(--surface2);color:var(--text2);border:1px solid var(--border)}
.btn-s:hover{background:var(--surface3);color:var(--text)}
.btn-d{background:var(--red-bg);color:var(--red);border:1px solid rgba(239,68,68,.3)}
.btn-sm{padding:5px 11px;font-size:12px}
.btn-full{width:100%}
.btn:disabled{opacity:.5;cursor:not-allowed;transform:none}
.hist-item{display:flex;align-items:center;gap:12px;padding:11px 0;border-bottom:1px solid var(--border)}
.hist-item:last-child{border-bottom:none}
.hist-badge{width:36px;height:36px;border-radius:8px;display:flex;align-items:center;justify-content:center;font-size:15px;flex-shrink:0}
.hist-badge.Estoque{background:var(--green-bg)}
.hist-badge.Expedicao{background:var(--red-bg)}
.hist-info{flex:1;min-width:0}
.hist-nome{font-size:13px;font-weight:600;white-space:nowrap;overflow:hidden;text-overflow:ellipsis}
.hist-meta{font-size:11px;color:var(--text3);margin-top:1px;display:flex;align-items:center;gap:5px;flex-wrap:wrap}
.hist-qty{font-family:'DM Mono',monospace;font-weight:700;font-size:14px;flex-shrink:0}
.hist-qty.Estoque{color:var(--green)}
.hist-qty.Expedicao{color:var(--red)}
.status-badge{font-size:10px;font-weight:700;padding:2px 6px;border-radius:6px}
.status-badge.pendente{background:var(--yellow-bg);color:var(--yellow)}
.status-badge.requisitado{background:var(--accent-bg);color:var(--accent2)}
.rel-row{display:flex;align-items:center;padding:9px 0;border-bottom:1px solid var(--border)}
.rel-row:last-child{border-bottom:none}
.rel-nome{font-size:13px;font-weight:500;flex:1;overflow:hidden;text-overflow:ellipsis;white-space:nowrap}
.rel-bar-wrap{width:80px;height:5px;background:var(--surface3);border-radius:3px;margin:0 10px;overflow:hidden;flex-shrink:0}
.rel-bar{height:100%;border-radius:3px;transition:width .4s}
.rel-val{font-family:'DM Mono',monospace;font-size:12px;font-weight:600;color:var(--text2);min-width:44px;text-align:right;flex-shrink:0}
.filtros{display:flex;gap:7px;margin-bottom:12px;overflow-x:auto;padding-bottom:2px}
.filtro-btn{white-space:nowrap;padding:5px 13px;border:1.5px solid var(--border);border-radius:20px;background:var(--surface);font-size:12px;font-weight:600;cursor:pointer;transition:all .15s;color:var(--text3)}
.filtro-btn.active{background:var(--accent);color:#fff;border-color:var(--accent)}
.sbox{position:relative;margin-bottom:12px}
.sbox input{padding-left:36px}
.sbox svg{position:absolute;left:10px;top:50%;transform:translateY(-50%);width:17px;height:17px;color:var(--text3);pointer-events:none;stroke:currentColor;fill:none;stroke-width:2}
.modal-overlay{position:fixed;inset:0;background:rgba(0,0,0,.68);z-index:200;display:flex;align-items:flex-end;justify-content:center;opacity:0;pointer-events:none;transition:opacity .2s}
.modal-overlay.open{opacity:1;pointer-events:all}
.modal{background:var(--bg2);border:1px solid var(--border2);border-radius:20px 20px 0 0;width:100%;max-width:760px;padding:20px 18px 32px;transform:translateY(30px);transition:transform .25s;max-height:90dvh;overflow-y:auto}
@media(min-width:600px){.modal-overlay{align-items:center}.modal{border-radius:16px;max-height:82dvh}}
.modal-overlay.open .modal{transform:translateY(0)}
.modal-handle{width:36px;height:4px;background:var(--border2);border-radius:2px;margin:0 auto 16px}
.modal-title{font-size:17px;font-weight:700;margin-bottom:16px}
.sec-hdr{display:flex;align-items:center;justify-content:space-between;margin-bottom:13px}
.sec-hdr h2{font-size:15px;font-weight:700}
.alert{border-radius:var(--radius-sm);padding:9px 13px;font-size:13px;font-weight:500;margin-bottom:11px;display:flex;align-items:center;gap:8px}
.alert-w{background:var(--yellow-bg);color:var(--yellow);border:1px solid rgba(245,158,11,.3)}
.alert-e{background:var(--red-bg);color:var(--red);border:1px solid rgba(239,68,68,.3)}
.pending-bar{background:var(--yellow-bg);border:1px solid rgba(245,158,11,.3);border-radius:var(--radius-sm);padding:9px 13px;font-size:13px;color:var(--yellow);display:flex;align-items:center;justify-content:space-between;margin-bottom:11px;gap:10px;flex-wrap:wrap}
.toast{position:fixed;top:68px;left:50%;transform:translateX(-50%) translateY(-10px);background:var(--surface3);border:1px solid var(--border2);color:var(--text);padding:10px 18px;border-radius:20px;font-size:13px;font-weight:600;z-index:999;opacity:0;transition:all .25s;pointer-events:none;max-width:90vw;text-align:center;box-shadow:0 4px 20px rgba(0,0,0,.5)}
.toast.show{opacity:1;transform:translateX(-50%) translateY(0)}
.spinner{display:inline-block;width:16px;height:16px;border:2.5px solid var(--border2);border-top-color:var(--accent);border-radius:50%;animation:spin .7s linear infinite}
@keyframes spin{to{transform:rotate(360deg)}}
.empty{text-align:center;padding:36px 16px;color:var(--text3)}
.empty-icon{font-size:38px;margin-bottom:10px}
.empty p{font-size:13px;line-height:1.6}
.emoji-opts{display:flex;gap:6px;flex-wrap:wrap;margin-bottom:8px}
.emoji-opt{font-size:22px;cursor:pointer;padding:4px;border-radius:6px;transition:background .1s}
.emoji-opt:hover{background:var(--surface3)}
#loading-overlay{position:fixed;inset:0;background:var(--bg);z-index:500;display:flex;flex-direction:column;align-items:center;justify-content:center;gap:16px;transition:opacity .4s}
#loading-overlay.hide{opacity:0;pointer-events:none}
</style>
</head>
<body>

<div id="loading-overlay">
  <div style="width:56px;height:56px;background:linear-gradient(135deg,#1d4ed8,#3b82f6);border-radius:14px;display:flex;align-items:center;justify-content:center;box-shadow:0 0 32px rgba(59,130,246,.55)">
    <svg width="28" height="28" viewBox="0 0 24 24" fill="white"><path d="M20 7H4C2.9 7 2 7.9 2 9v11c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V9c0-1.1-.9-2-2-2zm0 12H4V9h16v10zM6 5h12V3H6v2z"/></svg>
  </div>
  <div class="spinner" style="width:22px;height:22px;border-width:3px"></div>
  <p style="color:var(--text2);font-size:14px">Carregando insumos...</p>
</div>

<header>
  <div class="hdr">
    <div class="logo-area">
      <div class="logo-box">
        <svg viewBox="0 0 24 24"><path d="M20 7H4C2.9 7 2 7.9 2 9v11c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V9c0-1.1-.9-2-2-2zm0 12H4V9h16v10zM6 5h12V3H6v2z"/></svg>
      </div>
      <div>
        <div class="app-title">Controle de Insumos</div>
        <div class="app-sub" id="turno-lbl">—</div>
      </div>
    </div>
    <div class="turno-pill" id="data-pill">—</div>
  </div>
</header>

<div class="sync-bar">
  <div class="sdot load" id="sdot"></div>
  <span id="smsg">Conectando à planilha...</span>
  <button class="btn btn-s btn-sm" onclick="carregarTudo()" style="margin-left:6px">↻ Sync</button>
</div>

<main>
  <div class="tab-bar">
    <button class="tab-btn active" onclick="showTab('estoque')" id="tb-estoque">
      <svg viewBox="0 0 24 24"><rect x="3" y="3" width="7" height="7" rx="1"/><rect x="14" y="3" width="7" height="7" rx="1"/><rect x="3" y="14" width="7" height="7" rx="1"/><rect x="14" y="14" width="7" height="7" rx="1"/></svg>
      Estoque
    </button>
    <button class="tab-btn" onclick="showTab('lancar')" id="tb-lancar">
      <svg viewBox="0 0 24 24"><circle cx="12" cy="12" r="10"/><line x1="12" y1="8" x2="12" y2="16"/><line x1="8" y1="12" x2="16" y2="12"/></svg>
      Lançar
    </button>
    <button class="tab-btn" onclick="showTab('historico')" id="tb-historico">
      <svg viewBox="0 0 24 24"><path d="M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z"/></svg>
      Histórico
    </button>
    <button class="tab-btn" onclick="showTab('relatorios')" id="tb-relatorios">
      <svg viewBox="0 0 24 24"><line x1="18" y1="20" x2="18" y2="10"/><line x1="12" y1="20" x2="12" y2="4"/><line x1="6" y1="20" x2="6" y2="14"/></svg>
      Relatórios
    </button>
  </div>

  <!-- ESTOQUE -->
  <div id="tab-estoque">
    <div class="strip">
      <div class="stat"><div class="v" id="s-total">—</div><div class="l">Insumos</div></div>
      <div class="stat"><div class="v" style="color:var(--green)" id="s-ent">—</div><div class="l">Total Entradas</div></div>
      <div class="stat"><div class="v" style="color:var(--red)" id="s-sai">—</div><div class="l">Total Saídas</div></div>
    </div>
    <div id="alertas"></div>
    <div class="sec-hdr">
      <h2>Insumos</h2>
      <button class="btn btn-s btn-sm" onclick="carregarTudo()">↻ Atualizar</button>
    </div>
    <div class="grid" id="estoque-grid">
      <div style="grid-column:1/-1;text-align:center;padding:32px"><div class="spinner" style="width:22px;height:22px;border-width:3px"></div></div>
    </div>
  </div>

  <!-- LANÇAR -->
  <div id="tab-lancar" style="display:none">
    <div id="pending-warn"></div>
    <div class="card">
      <div class="card-title">Novo Lançamento</div>
      <div class="tipo-tog">
        <div class="tipo-opt estoque sel" id="opt-estoque"   onclick="setTipo('Estoque')">📥 Entrada</div>
        <div class="tipo-opt expedicao"   id="opt-expedicao" onclick="setTipo('Expedicao')">📤 Expedição</div>
      </div>
      <div class="fg">
        <label>Insumo</label>
        <select id="f-insumo" onchange="atualizarRef()">
          <option value="">Selecione...</option>
        </select>
      </div>
      <div class="frow">
        <div class="fg">
          <label>Referência</label>
          <input type="text" id="f-ref" disabled placeholder="—">
        </div>
        <div class="fg">
          <label>Quantidade</label>
          <input type="number" id="f-qty" min="1" placeholder="0" inputmode="numeric">
        </div>
      </div>
      <div class="data-row">
        <input type="checkbox" id="chk-data" onchange="toggleData()">
        <label for="chk-data">Data manual:</label>
        <input type="date" id="f-data" disabled>
      </div>
      <button class="btn btn-p btn-full" id="btn-lancar" onclick="registrarLancamento()">Registrar Lançamento</button>
    </div>
  </div>

  <!-- HISTÓRICO -->
  <div id="tab-historico" style="display:none">
    <div class="sec-hdr">
      <h2>Histórico</h2>
      <button class="btn btn-s btn-sm" onclick="carregarHistorico()">↻ Atualizar</button>
    </div>
    <div class="filtros">
      <button class="filtro-btn active" onclick="setFiltro('todos')">Todos</button>
      <button class="filtro-btn" onclick="setFiltro('Estoque')">Entradas</button>
      <button class="filtro-btn" onclick="setFiltro('Expedicao')">Expedições</button>
    </div>
    <div class="sbox">
      <svg viewBox="0 0 24 24"><circle cx="11" cy="11" r="8"/><line x1="21" y1="21" x2="16.65" y2="16.65"/></svg>
      <input type="text" id="hist-busca" placeholder="Buscar por insumo ou referência..." oninput="renderHistorico()">
    </div>
    <div class="card" style="padding:4px 16px"><div id="hist-list"></div></div>
  </div>

  <!-- RELATÓRIOS -->
  <div id="tab-relatorios" style="display:none">
    <div class="strip">
      <div class="stat"><div class="v" style="color:var(--green)" id="r-ent">—</div><div class="l">Qtd. Entradas</div></div>
      <div class="stat"><div class="v" style="color:var(--red)"   id="r-sai">—</div><div class="l">Qtd. Saídas</div></div>
      <div class="stat"><div class="v" id="r-tot">—</div><div class="l">Movimentos</div></div>
    </div>
    <div class="card">
      <div class="card-title">Top expedições (saídas)</div>
      <div id="rel-exp"></div>
    </div>
    <div class="card">
      <div class="card-title">Top entradas (estoque)</div>
      <div id="rel-est"></div>
    </div>
    <div style="text-align:center;margin-top:8px">
      <button class="btn btn-s btn-sm" onclick="exportarCSV()">📥 Exportar CSV</button>
    </div>
  </div>
</main>

<!-- MODAL DETALHE -->
<div class="modal-overlay" id="modal-det" onclick="fecharModal('modal-det')">
  <div class="modal" onclick="event.stopPropagation()">
    <div class="modal-handle"></div>
    <div id="det-body"></div>
  </div>
</div>

<div class="toast" id="toast"></div>

<script>
// ─────────────────────────────────────────────────────────
// CONFIGURAÇÃO — campos exatos da sua planilha
// buscarInsumos  → [ { nome, ref } ]
// buscarHistorico→ [ { data, item, ref, qtd, tipo, status } ]
//   tipo: "Estoque" = Entrada  |  "Expedicao" = Saída
//   qtd:  positivo em Estoque  |  negativo em Expedicao
// doPost recebe: { tipo, nome_item, referencia, quantidade, dataManual? }
// ─────────────────────────────────────────────────────────
const API = 'https://script.google.com/macros/s/AKfycbwRLuYb27DOjC7_wLz703_QA7xt1Rgz0o36mcPMOkzIQzTXZsBJdIQT0biqbWsyLOfm/exec';
const EMOJIS = ['📦','🧊','🎁','🏷️','🛍️','🧴','🧻','💧','🔧','📌','🗂️','🧺','🪣','🫙'];

// ── STATE ─────────────────────────────────────────────────
// insumos: vêm da aba Lista_Insumos via buscarInsumos
// historico: vêm das abas Entradas+Saidas via buscarHistorico
let insumos   = [];  // { nome, ref, emoji }
let historico = [];  // { data, item, ref, qtd, tipo, status }
let pendentes = [];  // lançamentos offline
let filtroHist = 'todos';
let tipoAtual  = 'Estoque';

// ── PERSIST ───────────────────────────────────────────────
function salvarEmojis() {
  // Só salva o mapeamento emoji (o resto vem sempre da planilha)
  const map = {};
  insumos.forEach(i => { map[i.nome] = i.emoji; });
  try { localStorage.setItem('emoji_map', JSON.stringify(map)); } catch(e){}
}
function carregarEmojis() {
  try { return JSON.parse(localStorage.getItem('emoji_map')) || {}; } catch(e){ return {}; }
}
function salvarPend() {
  try { localStorage.setItem('pend_v2', JSON.stringify(pendentes)); } catch(e){}
}
function carregarPend() {
  try { pendentes = JSON.parse(localStorage.getItem('pend_v2')) || []; } catch(e){ pendentes=[]; }
}

// ── UTILS ─────────────────────────────────────────────────
function uid() { return Date.now().toString(36)+Math.random().toString(36).slice(2); }

function getDataContabil() {
  const now = new Date();
  if (now.getHours() < 8) now.setDate(now.getDate()-1);
  return now.toLocaleDateString('pt-BR');
}
function getTurno() {
  const h = new Date().getHours();
  if (h>=6&&h<14) return 'Turno A · 06h–14h';
  if (h>=14&&h<22) return 'Turno B · 14h–22h';
  return 'Turno C · 22h–06h';
}
function fmtData(v) {
  if (!v) return '—';
  try {
    const d = new Date(v);
    if (!isNaN(d)) return d.toLocaleDateString('pt-BR');
  } catch(e){}
  return String(v).substring(0,10);
}
function normalizar(s) {
  return String(s||'').trim().toLowerCase()
    .normalize('NFD').replace(/[\u0300-\u036f]/g,'');
}

// ── SYNC STATUS ───────────────────────────────────────────
function setSS(state, msg) {
  document.getElementById('sdot').className = 'sdot '+state;
  document.getElementById('smsg').textContent = msg;
}

// ── API ───────────────────────────────────────────────────
async function apiGet(action) {
  const r = await fetch(`${API}?action=${action}`);
  if (!r.ok) throw new Error('HTTP '+r.status);
  return JSON.parse(await r.text());
}

async function apiPost(payload) {
  const r = await fetch(API, {
    method: 'POST',
    headers: { 'Content-Type': 'text/plain' },
    body: JSON.stringify(payload)
  });
  if (!r.ok) throw new Error('HTTP '+r.status);
  const res = JSON.parse(await r.text());
  if (res.result !== 'success') throw new Error(res.message || 'Erro na planilha');
  return res;
}

// ── CARREGAR INSUMOS ──────────────────────────────────────
// Resposta: [ { nome: "Isopor 3L", ref: "EMB0022" }, ... ]
async function carregarInsumos() {
  const data = await apiGet('buscarInsumos');
  if (!Array.isArray(data)) return;
  const emojiMap = carregarEmojis();
  insumos = data.map(d => ({
    nome:  d.nome || '',
    ref:   d.ref  || '',
    emoji: emojiMap[d.nome] || '📦',
  }));
  salvarEmojis();
}

// ── CARREGAR HISTÓRICO ────────────────────────────────────
// Resposta: [ { data, item, ref, qtd, tipo, status }, ... ]
// tipo "Estoque"   → qtd positivo  → Entrada
// tipo "Expedicao" → qtd negativo  → Saída (qtd já vem *-1 do script)
async function carregarHistorico() {
  const data = await apiGet('buscarHistorico');
  if (!Array.isArray(data)) return;
  // Ordena do mais recente para o mais antigo
  historico = data.sort((a,b) => new Date(b.data) - new Date(a.data));
}

// ── CARREGAR TUDO ─────────────────────────────────────────
async function carregarTudo() {
  setSS('load','Sincronizando...');
  try {
    await carregarInsumos();
    await carregarHistorico();
    await enviarPendentes();
    setSS('ok','Sincronizado · '+new Date().toLocaleTimeString('pt-BR',{hour:'2-digit',minute:'2-digit'}));
  } catch(e) {
    setSS('err','Sem conexão com a planilha');
    console.warn('Sync error:', e);
  }
  renderEstoque();
  renderFormLancar();
  if (document.getElementById('tab-historico').style.display !== 'none') renderHistorico();
  if (document.getElementById('tab-relatorios').style.display !== 'none') renderRelatorios();
  document.getElementById('loading-overlay').classList.add('hide');
}

async function enviarPendentes() {
  if (!pendentes.length) return;
  const fila = [...pendentes]; pendentes = []; salvarPend();
  for (const p of fila) {
    try { await apiPost(p); }
    catch(e) { pendentes.push(p); }
  }
  salvarPend();
  renderPendingWarn();
}

// ── SALDO POR INSUMO ──────────────────────────────────────
// Calcula somando Estoque (qtd positivo) e subtraindo Expedicao (qtd negativo = já veio *-1)
function saldoInsumo(ins) {
  const nomeN = normalizar(ins.nome);
  const refN  = normalizar(ins.ref);
  return historico.reduce((acc, h) => {
    const itemN = normalizar(h.item);
    const hrefN = normalizar(h.ref);
    // Compara por nome OU por referência
    if (itemN !== nomeN && !(refN && hrefN && hrefN === refN)) return acc;
    const qtd = Number(h.qtd) || 0;
    // tipo "Estoque" → entrada (qtd positivo)
    // tipo "Expedicao" → saída (qtd já vem negativo do script: qtd * -1)
    if (h.tipo === 'Estoque')    return acc + Math.abs(qtd);
    if (h.tipo === 'Expedicao')  return acc - Math.abs(qtd);
    return acc;
  }, 0);
}

// ── RENDER ESTOQUE ────────────────────────────────────────
function renderEstoque() {
  // Totais gerais
  const totalEnt = historico.filter(h=>h.tipo==='Estoque')
    .reduce((s,h)=>s+Math.abs(Number(h.qtd)||0),0);
  const totalSai = historico.filter(h=>h.tipo==='Expedicao')
    .reduce((s,h)=>s+Math.abs(Number(h.qtd)||0),0);
  document.getElementById('s-total').textContent = insumos.length;
  document.getElementById('s-ent').textContent   = totalEnt;
  document.getElementById('s-sai').textContent   = totalSai;

  const al = document.getElementById('alertas');
  al.innerHTML = pendentes.length
    ? `<div class="alert alert-w">⏳ ${pendentes.length} lançamento(s) aguardando envio</div>` : '';

  const grid = document.getElementById('estoque-grid');
  if (!insumos.length) {
    grid.innerHTML = `<div class="empty" style="grid-column:1/-1">
      <div class="empty-icon">📭</div>
      <p>Nenhum insumo encontrado.<br>Verifique a aba <b>Lista_Insumos</b> na planilha.</p>
    </div>`;
    return;
  }

  grid.innerHTML = insumos.map(ins => {
    const saldo = saldoInsumo(ins);
    const cls   = saldo <= 0 ? 'crit' : saldo <= 10 ? 'warn' : '';
    return `<div class="ic ${cls}" onclick="abrirDetalhe(${JSON.stringify(ins.nome)})">
      <div class="ic-dot"></div>
      <span class="ic-emoji">${ins.emoji}</span>
      <div class="ic-nome">${ins.nome}</div>
      <div class="ic-ref">${ins.ref}</div>
      <div class="ic-qty">${saldo}</div>
      <div class="ic-unit">un</div>
    </div>`;
  }).join('');
}

// ── RENDER FORM LANÇAR ────────────────────────────────────
function renderFormLancar() {
  const sel = document.getElementById('f-insumo'), cur = sel.value;
  sel.innerHTML = '<option value="">Selecione...</option>' +
    insumos.map(i =>
      `<option value="${encodeURIComponent(i.nome)}">${i.emoji} ${i.nome} (${i.ref})</option>`
    ).join('');
  if (cur) sel.value = cur;
  atualizarRef();
  renderPendingWarn();
}

function atualizarRef() {
  const key = document.getElementById('f-insumo').value;
  const ins = insumos.find(i => encodeURIComponent(i.nome) === key);
  document.getElementById('f-ref').value = ins ? ins.ref : '';
}

function setTipo(t) {
  tipoAtual = t;
  document.getElementById('opt-estoque').classList.toggle('sel',   t==='Estoque');
  document.getElementById('opt-expedicao').classList.toggle('sel', t==='Expedicao');
}

function toggleData() {
  const chk = document.getElementById('chk-data').checked;
  const inp = document.getElementById('f-data');
  inp.disabled = !chk;
  if (chk && !inp.value) inp.value = new Date().toISOString().split('T')[0];
}

function renderPendingWarn() {
  const el = document.getElementById('pending-warn');
  if (!el) return;
  el.innerHTML = pendentes.length
    ? `<div class="pending-bar">⏳ ${pendentes.length} lançamento(s) offline
        <button class="btn btn-s btn-sm" onclick="carregarTudo()">Enviar agora</button>
       </div>` : '';
}

// ── REGISTRAR LANÇAMENTO ──────────────────────────────────
// Envia para doPost: { tipo, nome_item, referencia, quantidade, dataManual? }
async function registrarLancamento() {
  const key = document.getElementById('f-insumo').value;
  const qty = parseFloat(document.getElementById('f-qty').value);
  const ins = insumos.find(i => encodeURIComponent(i.nome) === key);

  if (!ins)         return toast('Selecione um insumo.');
  if (!qty || qty<=0) return toast('Informe uma quantidade válida.');

  const chkData = document.getElementById('chk-data').checked;
  const dataVal = document.getElementById('f-data').value;

  const payload = {
    tipo:       tipoAtual,   // "Estoque" → aba Entradas | "Expedicao" → aba Saidas
    nome_item:  ins.nome,    // campo exato esperado pelo doPost
    referencia: ins.ref,
    quantidade: qty,
  };
  if (chkData && dataVal) payload.dataManual = dataVal;

  const btn = document.getElementById('btn-lancar');
  btn.disabled = true;
  btn.innerHTML = '<div class="spinner"></div> Enviando...';

  try {
    await apiPost(payload);
    toast(`✅ ${tipoAtual==='Estoque'?'Entrada':'Expedição'} de ${qty} un gravada na planilha!`);
    // Recarrega histórico para refletir o novo lançamento
    await carregarHistorico();
    renderEstoque();
  } catch(e) {
    pendentes.push({ ...payload, _id: uid(), _ts: Date.now() });
    salvarPend();
    toast('⚠️ Sem conexão — salvo offline. Será enviado ao reconectar.');
    renderPendingWarn();
  }

  btn.disabled = false;
  btn.textContent = 'Registrar Lançamento';
  document.getElementById('f-qty').value = '';
}

// ── RENDER HISTÓRICO ──────────────────────────────────────
function renderHistorico() {
  const busca = normalizar(document.getElementById('hist-busca')?.value || '');
  let lista = [...historico];
  if (filtroHist !== 'todos') lista = lista.filter(h => h.tipo === filtroHist);
  if (busca) lista = lista.filter(h =>
    normalizar(h.item).includes(busca) || normalizar(h.ref).includes(busca)
  );

  const el = document.getElementById('hist-list');
  if (!lista.length) {
    el.innerHTML = '<div class="empty"><div class="empty-icon">📋</div><p>Nenhum registro encontrado.</p></div>';
    return;
  }

  el.innerHTML = lista.map(h => {
    const isEnt   = h.tipo === 'Estoque';
    const qtdAbs  = Math.abs(Number(h.qtd)||0);
    const stNorm  = normalizar(h.status||'');
    const stClass = stNorm.includes('pend') ? 'pendente' : 'requisitado';
    const stLabel = h.status || '';
    return `<div class="hist-item">
      <div class="hist-badge ${h.tipo}">${isEnt ? '📥' : '📤'}</div>
      <div class="hist-info">
        <div class="hist-nome">${h.item||'—'} <span style="color:var(--text3);font-size:11px;font-family:'DM Mono',monospace">${h.ref||''}</span></div>
        <div class="hist-meta">
          ${fmtData(h.data)}
          ${stLabel ? `<span class="status-badge ${stClass}">${stLabel}</span>` : ''}
        </div>
      </div>
      <div class="hist-qty ${h.tipo}">${isEnt ? '+' : '-'}${qtdAbs}</div>
    </div>`;
  }).join('');
}

function setFiltro(f) {
  filtroHist = f;
  document.querySelectorAll('.filtro-btn').forEach((b,i) =>
    b.classList.toggle('active', ['todos','Estoque','Expedicao'][i] === f));
  renderHistorico();
}

// ── RENDER RELATÓRIOS ─────────────────────────────────────
function renderRelatorios() {
  const ents = historico.filter(h=>h.tipo==='Estoque');
  const exps = historico.filter(h=>h.tipo==='Expedicao');
  document.getElementById('r-ent').textContent = ents.reduce((s,h)=>s+Math.abs(Number(h.qtd)||0),0);
  document.getElementById('r-sai').textContent = exps.reduce((s,h)=>s+Math.abs(Number(h.qtd)||0),0);
  document.getElementById('r-tot').textContent = historico.length;

  function grupo(arr, elId, cor) {
    const ag = {};
    arr.forEach(h => {
      const k = h.item||'—';
      ag[k] = (ag[k]||0) + Math.abs(Number(h.qtd)||0);
    });
    const sorted = Object.entries(ag).sort((a,b)=>b[1]-a[1]).slice(0,8);
    const max = sorted[0]?.[1]||1;
    document.getElementById(elId).innerHTML = !sorted.length
      ? '<div style="color:var(--text3);font-size:13px;padding:6px 0">Sem dados.</div>'
      : sorted.map(([nome,total]) => `
          <div class="rel-row">
            <div class="rel-nome">📦 ${nome}</div>
            <div class="rel-bar-wrap"><div class="rel-bar" style="width:${Math.round(total/max*100)}%;background:${cor}"></div></div>
            <div class="rel-val">${total}</div>
          </div>`).join('');
  }
  grupo(exps, 'rel-exp', 'var(--red)');
  grupo(ents, 'rel-est', 'var(--green)');
}

// ── DETALHE DO INSUMO ─────────────────────────────────────
function abrirDetalhe(nome) {
  const ins   = insumos.find(i => i.nome === nome);
  if (!ins) return;
  const saldo = saldoInsumo(ins);
  const nomeN = normalizar(ins.nome);
  const refN  = normalizar(ins.ref);
  const movs  = historico.filter(h =>
    normalizar(h.item) === nomeN || (refN && normalizar(h.ref) === refN)
  ).slice(0, 8);

  document.getElementById('det-body').innerHTML = `
    <div style="display:flex;align-items:center;gap:13px;margin-bottom:16px">
      <span style="font-size:42px">${ins.emoji}</span>
      <div>
        <div style="font-size:18px;font-weight:700">${ins.nome}</div>
        <div style="font-size:12px;color:var(--text3);font-family:'DM Mono',monospace">${ins.ref}</div>
      </div>
    </div>
    <div style="display:grid;grid-template-columns:1fr 1fr;gap:9px;margin-bottom:16px">
      <div class="stat"><div class="v" style="color:var(--accent2)">${saldo}</div><div class="l">Saldo atual</div></div>
      <div class="stat"><div class="v">${movs.length}</div><div class="l">Últimos mov.</div></div>
    </div>
    ${movs.length ? `<div class="card-title">Movimentos recentes</div>` +
      movs.map(h => {
        const isEnt = h.tipo === 'Estoque';
        return `<div class="hist-item">
          <div class="hist-badge ${h.tipo}">${isEnt?'📥':'📤'}</div>
          <div class="hist-info">
            <div class="hist-nome">${isEnt?'Entrada':'Expedição'}</div>
            <div class="hist-meta">${fmtData(h.data)} ${h.status?'· '+h.status:''}</div>
          </div>
          <div class="hist-qty ${h.tipo}">${isEnt?'+':'-'}${Math.abs(Number(h.qtd)||0)}</div>
        </div>`;
      }).join('') : ''}
    <div style="display:grid;grid-template-columns:1fr 1fr;gap:8px;margin-top:14px">
      <button class="btn btn-s" onclick="fecharModal('modal-det');showTab('lancar');setTimeout(()=>{
        document.getElementById('f-insumo').value=encodeURIComponent(${JSON.stringify(nome)});
        atualizarRef();setTipo('Estoque');},120)">📥 Entrada</button>
      <button class="btn btn-s" onclick="fecharModal('modal-det');showTab('lancar');setTimeout(()=>{
        document.getElementById('f-insumo').value=encodeURIComponent(${JSON.stringify(nome)});
        atualizarRef();setTipo('Expedicao');},120)">📤 Expedição</button>
    </div>
    <div style="margin-top:12px">
      <label style="font-size:11px;font-weight:700;color:var(--text3);text-transform:uppercase;letter-spacing:.5px;display:block;margin-bottom:6px">Ícone</label>
      <div class="emoji-opts">${EMOJIS.map(e=>`<span class="emoji-opt" onclick="trocarEmoji(${JSON.stringify(nome)},'${e}')">${e}</span>`).join('')}</div>
    </div>`;
  document.getElementById('modal-det').classList.add('open');
}

function trocarEmoji(nome, emoji) {
  const ins = insumos.find(i=>i.nome===nome);
  if (ins) { ins.emoji = emoji; salvarEmojis(); renderEstoque(); renderFormLancar(); }
  fecharModal('modal-det');
  toast('Ícone atualizado!');
}

function fecharModal(id) { document.getElementById(id).classList.remove('open'); }

// ── EXPORTAR CSV ──────────────────────────────────────────
function exportarCSV() {
  const rows = historico.map(h =>
    `${fmtData(h.data)},"${h.item||''}","${h.ref||''}",${h.tipo},${Math.abs(Number(h.qtd)||0)},"${h.status||''}"`
  );
  const csv = ['Data,Item,Referência,Tipo,Quantidade,Status', ...rows].join('\n');
  const a = Object.assign(document.createElement('a'), {
    href: URL.createObjectURL(new Blob(['\uFEFF'+csv],{type:'text/csv;charset=utf-8;'})),
    download: `historico_${getDataContabil().replace(/\//g,'-')}.csv`
  });
  a.click(); URL.revokeObjectURL(a.href);
  toast('CSV exportado!');
}

// ── TABS ──────────────────────────────────────────────────
function showTab(tab) {
  ['estoque','lancar','historico','relatorios'].forEach(t => {
    document.getElementById('tab-'+t).style.display = t===tab?'':'none';
    document.getElementById('tb-'+t).classList.toggle('active', t===tab);
  });
  if (tab==='estoque')    renderEstoque();
  if (tab==='lancar')     renderFormLancar();
  if (tab==='historico')  renderHistorico();
  if (tab==='relatorios') renderRelatorios();
}

// ── TOAST ─────────────────────────────────────────────────
function toast(msg) {
  const el = document.getElementById('toast');
  el.textContent = msg; el.classList.add('show');
  clearTimeout(el._t); el._t = setTimeout(()=>el.classList.remove('show'),3200);
}

// ── INIT ──────────────────────────────────────────────────
carregarPend();
document.getElementById('turno-lbl').textContent = getTurno();
document.getElementById('data-pill').textContent = getDataContabil();
carregarTudo();
setInterval(carregarTudo, 180000); // auto-sync a cada 3 min
</script>
</body>
</html>

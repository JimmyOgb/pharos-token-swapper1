<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Pharos Token Swapper</title>
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@tabler/icons-webfont@latest/dist/tabler-icons.min.css">
<style>
*{box-sizing:border-box;margin:0;padding:0}
:root {
  --font-sans: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
  --font-mono: SFMono-Regular, Consolas, "Liberation Mono", Menlo, monospace;
  --color-background-primary: #ffffff;
  --color-background-secondary: #f8f9fa;
  --color-background-tertiary: #f1f3f5;
  --color-border-tertiary: #dee2e6;
  --color-border-secondary: #ced4da;
  --color-text-primary: #212529;
  --color-text-secondary: #495057;
  --color-text-tertiary: #868e96;
  --border-radius-md: 8px;
  --border-radius-lg: 12px;
}
body{font-family:var(--font-sans);background:var(--color-background-tertiary);min-height:100vh;padding:0}
.app{max-width:480px;margin:0 auto;padding:1.5rem 1rem 3rem}
.topbar{display:flex;align-items:center;justify-content:space-between;margin-bottom:1.5rem}
.logo{display:flex;align-items:center;gap:8px}
.logo-icon{width:28px;height:28px;background:#1D9E75;border-radius:8px;display:flex;align-items:center;justify-content:center}
.logo-icon i{font-size:16px;color:#fff}
.logo-text{font-size:15px;font-weight:500;color:var(--color-text-primary)}
.logo-sub{font-size:11px;color:var(--color-text-secondary);margin-top:1px}
.network-badge{display:flex;align-items:center;gap:6px;background:var(--color-background-primary);border:0.5px solid var(--color-border-tertiary);border-radius:var(--border-radius-md);padding:5px 10px;font-size:12px;color:var(--color-text-secondary)}
.net-dot{width:7px;height:7px;border-radius:50%;background:#1D9E75}

.wallet-card{background:var(--color-background-primary);border:0.5px solid var(--color-border-tertiary);border-radius:var(--border-radius-lg);padding:1rem 1.25rem;margin-bottom:1rem}
.wallet-header{display:flex;align-items:center;justify-content:space-between;margin-bottom:.75rem}
.wallet-label{font-size:12px;color:var(--color-text-secondary);letter-spacing:.02em}
.wallet-actions{display:flex;gap:6px}
.icon-btn{background:none;border:0.5px solid var(--color-border-tertiary);border-radius:6px;width:26px;height:26px;display:flex;align-items:center;justify-content:center;cursor:pointer;color:var(--color-text-secondary)}
.icon-btn:hover{background:var(--color-background-secondary)}
.icon-btn i{font-size:14px}
.wallet-addr{font-size:13px;font-family:var(--font-mono);color:var(--color-text-primary);margin-bottom:.75rem}
.balances{display:grid;grid-template-columns:1fr 1fr;gap:8px}
.bal-item{background:var(--color-background-secondary);border-radius:var(--border-radius-md);padding:.6rem .75rem}
.bal-symbol{font-size:11px;color:var(--color-text-secondary);margin-bottom:2px}
.bal-amount{font-size:15px;font-weight:500;color:var(--color-text-primary)}

.connect-card{background:var(--color-background-primary);border:0.5px solid var(--color-border-tertiary);border-radius:var(--border-radius-lg);padding:1.5rem 1.25rem;margin-bottom:1rem;text-align:center}
.connect-icon{width:48px;height:48px;background:var(--color-background-secondary);border-radius:50%;display:flex;align-items:center;justify-content:center;margin:0 auto 1rem}
.connect-icon i{font-size:24px;color:var(--color-text-secondary)}
.connect-title{font-size:14px;font-weight:500;color:var(--color-text-primary);margin-bottom:.4rem}
.connect-desc{font-size:12px;color:var(--color-text-secondary);margin-bottom:1rem;line-height:1.5}
.btn-primary{width:100%;background:#1D9E75;color:#fff;border:none;border-radius:var(--border-radius-md);padding:10px 16px;font-size:14px;font-weight:500;cursor:pointer;display:flex;align-items:center;justify-content:center;gap:8px}
.btn-primary:hover{background:#0F6E56}
.btn-primary i{font-size:16px}

.swap-card{background:var(--color-background-primary);border:0.5px solid var(--color-border-tertiary);border-radius:var(--border-radius-lg);padding:1.25rem;margin-bottom:1rem}
.token-field{background:var(--color-background-secondary);border:0.5px solid var(--color-border-tertiary);border-radius:var(--border-radius-md);padding:.75rem 1rem;margin-bottom:.5rem}
.field-row{display:flex;align-items:center;justify-content:space-between;margin-bottom:.5rem}
.field-label{font-size:11px;color:var(--color-text-secondary)}
.field-balance{font-size:11px;color:var(--color-text-secondary);cursor:pointer}
.field-balance:hover{color:var(--color-text-primary)}
.token-row{display:flex;align-items:center;gap:.75rem}
.token-select{display:flex;align-items:center;gap:6px;background:var(--color-background-primary);border:0.5px solid var(--color-border-tertiary);border-radius:var(--border-radius-md);padding:5px 10px;cursor:pointer;font-size:13px;font-weight:500;color:var(--color-text-primary);white-space:nowrap}
.token-select:hover{border-color:var(--color-border-secondary)}
.token-icon{width:20px;height:20px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:9px;font-weight:700;color:#fff}
.token-select i{font-size:12px;color:var(--color-text-secondary)}
.amount-input{flex:1;background:none;border:none;outline:none;font-size:20px;font-weight:500;color:var(--color-text-primary);text-align:right;font-family:var(--font-sans);width:0}
.amount-input::placeholder{color:var(--color-text-tertiary)}
.usd-value{font-size:11px;color:var(--color-text-secondary);text-align:right;margin-top:2px}

.swap-arrow{display:flex;justify-content:center;margin:.25rem 0;position:relative;z-index:1}
.arrow-btn{background:var(--color-background-primary);border:0.5px solid var(--color-border-tertiary);border-radius:8px;width:32px;height:32px;display:flex;align-items:center;justify-content:center;cursor:pointer;color:var(--color-text-secondary);transition:transform .2s}
.arrow-btn:hover{color:#1D9E75;border-color:#1D9E75;transform:rotate(180deg)}
.arrow-btn i{font-size:16px}

.slippage-row{display:flex;align-items:center;justify-content:space-between;margin:.75rem 0 .25rem}
.slippage-label{font-size:12px;color:var(--color-text-secondary)}
.slippage-options{display:flex;gap:4px}
.slip-btn{background:none;border:0.5px solid var(--color-border-tertiary);border-radius:5px;padding:3px 8px;font-size:11px;color:var(--color-text-secondary);cursor:pointer}
.slip-btn.active{background:#E1F5EE;border-color:#1D9E75;color:#0F6E56}
.slip-btn:hover:not(.active){background:var(--color-background-secondary)}

.quote-box{background:var(--color-background-secondary);border-radius:var(--border-radius-md);padding:.75rem 1rem;margin:.75rem 0;font-size:12px}
.quote-row{display:flex;justify-content:space-between;align-items:center;padding:2px 0}
.quote-key{color:var(--color-text-secondary)}
.quote-val{color:var(--color-text-primary);font-weight:500}
.quote-val.good{color:#0F6E56}
.quote-val.warn{color:#BA7517}

.btn-swap{width:100%;padding:12px;border-radius:var(--border-radius-md);border:none;font-size:15px;font-weight:500;cursor:pointer;display:flex;align-items:center;justify-content:center;gap:8px;transition:all .15s}
.btn-swap.ready{background:#1D9E75;color:#fff}
.btn-swap.ready:hover{background:#0F6E56}
.btn-swap.disabled{background:var(--color-background-secondary);color:var(--color-text-tertiary);cursor:not-allowed;border:0.5px solid var(--color-border-tertiary)}
.btn-swap i{font-size:18px}

.steps-card{background:var(--color-background-primary);border:0.5px solid var(--color-border-tertiary);border-radius:var(--border-radius-lg);padding:1.25rem;margin-bottom:1rem}
.steps-title{font-size:13px;font-weight:500;color:var(--color-text-primary);margin-bottom:1rem}
.step-item{display:flex;align-items:flex-start;gap:.75rem;padding:.5rem 0}
.step-item:not(:last-child){border-bottom:0.5px solid var(--color-border-tertiary)}
.step-dot{width:24px;height:24px;border-radius:50%;border:0.5px solid var(--color-border-tertiary);display:flex;align-items:center;justify-content:center;flex-shrink:0;background:var(--color-background-secondary)}
.step-dot i{font-size:13px}
.step-dot.done{background:#E1F5EE;border-color:#1D9E75}
.step-dot.done i{color:#0F6E56}
.step-dot.active{background:#E1F5EE;border-color:#1D9E75;animation:pulse 1.5s infinite}
.step-dot.active i{color:#0F6E56}
.step-dot.pending i{color:var(--color-text-tertiary)}
@keyframes pulse{0%,100%{opacity:1}50%{opacity:.5}}
.step-info{flex:1;padding-top:2px}
.step-name{font-size:13px;color:var(--color-text-primary);font-weight:500}
.step-desc{font-size:11px;color:var(--color-text-secondary);margin-top:2px}
.step-hash{font-size:10px;font-family:var(--font-mono);color:#0F6E56;margin-top:3px;cursor:pointer;text-decoration:underline}

.modal-bg{position:fixed;inset:0;background:rgba(0,0,0,.4);display:flex;align-items:center;justify-content:center;z-index:100;padding:1rem}
.modal{background:var(--color-background-primary);border-radius:var(--border-radius-lg);border:0.5px solid var(--color-border-tertiary);padding:1.5rem;width:100%;max-width:380px}
.modal-title{font-size:15px;font-weight:500;margin-bottom:1rem;display:flex;justify-content:space-between;align-items:center}
.modal-close{background:none;border:none;cursor:pointer;color:var(--color-text-secondary);font-size:20px;line-height:1}
.wallet-option{display:flex;align-items:center;gap:12px;padding:.75rem;border:0.5px solid var(--color-border-tertiary);border-radius:var(--border-radius-md);cursor:pointer;margin-bottom:.5rem;transition:border-color .15s}
.wallet-option:hover{border-color:#1D9E75;background:var(--color-background-secondary)}
.wallet-opt-icon{width:36px;height:36px;border-radius:8px;display:flex;align-items:center;justify-content:center;font-size:18px}
.wallet-opt-name{font-size:14px;font-weight:500;color:var(--color-text-primary)}
.wallet-opt-desc{font-size:11px;color:var(--color-text-secondary)}

.token-modal .token-list-item{display:flex;align-items:center;gap:10px;padding:.6rem .75rem;border-radius:var(--border-radius-md);cursor:pointer}
.token-modal .token-list-item:hover{background:var(--color-background-secondary)}
.tok-name{font-size:13px;font-weight:500;color:var(--color-text-primary)}
.tok-bal{font-size:11px;color:var(--color-text-secondary)}
.tok-addr{font-size:10px;font-family:var(--font-mono);color:var(--color-text-tertiary)}
.search-input{width:100%;padding:8px 12px;border:0.5px solid var(--color-border-tertiary);border-radius:var(--border-radius-md);font-size:13px;background:var(--color-background-secondary);color:var(--color-text-primary);outline:none;margin-bottom:.75rem}
.search-input:focus{border-color:#1D9E75}

.tab-row{display:flex;gap:4px;background:var(--color-background-secondary);border-radius:var(--border-radius-md);padding:3px;margin-bottom:1rem}
.tab{flex:1;text-align:center;padding:6px;border-radius:6px;font-size:12px;cursor:pointer;color:var(--color-text-secondary);border:none;background:none}
.tab.active{background:var(--color-background-primary);color:var(--color-text-primary);font-weight:500;border:0.5px solid var(--color-border-tertiary)}
</style>
</head>
<body>
<div class="app" id="app">

<div class="topbar">
  <div class="logo">
    <div class="logo-icon"><i class="ti ti-arrows-exchange" aria-hidden="true"></i></div>
    <div>
      <div class="logo-text">Token Swapper</div>
      <div class="logo-sub">Pharos Skill Engine</div>
    </div>
  </div>
  <div class="network-badge">
    <div class="net-dot"></div>
    Atlantic Testnet
  </div>
</div>

<div id="main"></div>

</div>

<div id="modal-root"></div>

<script>
const TOKENS = [
  {symbol:'PHRS',name:'Pharos',addr:'native',decimals:18,color:'#1D9E75',icon:'ti-coin',balance:2.418},
  {symbol:'USDC',name:'USD Coin',addr:'0xE0BE0...ec8',decimals:6,color:'#2775CA',icon:'ti-currency-dollar',balance:150.00},
  {symbol:'USDT',name:'Tether USD',addr:'0xdAC17...ec1',decimals:6,color:'#26A17B',icon:'ti-currency-dollar',balance:80.50},
  {symbol:'WPHRS',name:'Wrapped PHRS',addr:'0xC02aa...6Cc2',decimals:18,color:'#627EEA',icon:'ti-coin',balance:0.5},
];

const PRICES = {PHRS:2.14,USDC:1.0,USDT:1.0,WPHRS:2.14};

let state = {
  connected: false,
  wallet: '',
  tokenIn: TOKENS[1],
  tokenOut: TOKENS[0],
  amountIn: '',
  slippage: 1.0,
  view: 'swap',
  swapping: false,
  swapStep: 0,
  txHash: '',
  showWalletModal: false,
  showTokenModal: null,
  tokenSearchQuery: '',
};

function shortAddr(a){return a?a.slice(0,6)+'...'+a.slice(-4):''}

function getQuote(){
  if(!state.amountIn||isNaN(parseFloat(state.amountIn)))return null;
  const amt = parseFloat(state.amountIn);
  const pIn = PRICES[state.tokenIn.symbol]||1;
  const pOut = PRICES[state.tokenOut.symbol]||1;
  const raw = amt * pIn / pOut;
  const min = raw*(1-state.slippage/100);
  const impact = ((Math.random()*0.3)+0.05).toFixed(2);
  return {out:raw.toFixed(4),min:min.toFixed(4),impact,gas:'~0.0012 PHRS'};
}

function tokenIcon(tok,size=20){
  return `<div class="token-icon" style="width:${size}px;height:${size}px;background:${tok.color};font-size:${Math.floor(size*0.45)}px">${tok.symbol[0]}</div>`;
}

function renderWalletCard(){
  if(!state.connected) return `
    <div class="connect-card">
      <div class="connect-icon"><i class="ti ti-wallet" aria-hidden="true"></i></div>
      <div class="connect-title">Connect your wallet</div>
      <div class="connect-desc">Link a wallet to check balances, approve tokens, and execute swaps on Pharos.</div>
      <button class="btn-primary" onclick="openWalletModal()">
        <i class="ti ti-plug" aria-hidden="true"></i> Connect wallet
      </button>
    </div>`;

  return `
    <div class="wallet-card">
      <div class="wallet-header">
        <span class="wallet-label">Connected wallet</span>
        <div class="wallet-actions">
          <button class="icon-btn" title="Copy address" onclick="copyAddr()"><i class="ti ti-copy" aria-hidden="true"></i></button>
          <button class="icon-btn" title="Disconnect" onclick="disconnect()"><i class="ti ti-plug-x" aria-hidden="true"></i></button>
        </div>
      </div>
      <div class="wallet-addr">${state.wallet}</div>
      <div class="balances">
        ${TOKENS.map(t=>`
        <div class="bal-item">
          <div class="bal-symbol">${t.symbol}</div>
          <div class="bal-amount">${t.balance.toFixed(3)}</div>
        </div>`).join('')}
      </div>
    </div>`;
}

function renderSwap(){
  const q = state.connected ? getQuote() : null;
  const canSwap = state.connected && state.amountIn && parseFloat(state.amountIn)>0;
  return `
    <div class="swap-card">
      <div class="tab-row">
        <button class="tab ${state.view==='swap'?'active':''}" onclick="setView('swap')">Swap</button>
        <button class="tab ${state.view==='monitor'?'active':''}" onclick="setView('monitor')">Activity</button>
      </div>

      <div class="token-field">
        <div class="field-row">
          <span class="field-label">You pay</span>
          ${state.connected?`<span class="field-balance" onclick="setMax()">Balance: ${state.tokenIn.balance.toFixed(3)} ${state.tokenIn.symbol}</span>`:''}
        </div>
        <div class="token-row">
          <button class="token-select" onclick="openTokenModal('in')">
            ${tokenIcon(state.tokenIn,20)}
            ${state.tokenIn.symbol}
            <i class="ti ti-chevron-down" aria-hidden="true"></i>
          </button>
          <input class="amount-input" type="number" placeholder="0.00" value="${state.amountIn}"
            oninput="setAmount(this.value)" ${!state.connected?'disabled':''}>
        </div>
        ${state.amountIn?`<div class="usd-value">≈ $${(parseFloat(state.amountIn||0)*PRICES[state.tokenIn.symbol]).toFixed(2)}</div>`:''}
      </div>

      <div class="swap-arrow">
        <button class="arrow-btn" onclick="flipTokens()" title="Flip tokens">
          <i class="ti ti-arrows-up-down" aria-hidden="true"></i>
        </button>
      </div>

      <div class="token-field">
        <div class="field-row">
          <span class="field-label">You receive</span>
          ${state.connected?`<span class="field-balance">Balance: ${state.tokenOut.balance.toFixed(3)} ${state.tokenOut.symbol}</span>`:''}
        </div>
        <div class="token-row">
          <button class="token-select" onclick="openTokenModal('out')">
            ${tokenIcon(state.tokenOut,20)}
            ${state.tokenOut.symbol}
            <i class="ti ti-chevron-down" aria-hidden="true"></i>
          </button>
          <input class="amount-input" type="number" placeholder="0.00"
            value="${q?q.out:''}" readonly style="color:var(--color-text-secondary)">
        </div>
        ${q?`<div class="usd-value">≈ $${(parseFloat(q.out)*PRICES[state.tokenOut.symbol]).toFixed(2)}</div>`:''}
      </div>

      <div class="slippage-row">
        <span class="slippage-label">Slippage tolerance</span>
        <div class="slippage-options">
          ${[0.1,0.5,1.0,2.0].map(s=>`
          <button class="slip-btn ${state.slippage===s?'active':''}" onclick="setSlippage(${s})">${s}%</button>`).join('')}
        </div>
      </div>

      ${q?`
      <div class="quote-box">
        <div class="quote-row"><span class="quote-key">Rate</span><span class="quote-val">1 ${state.tokenIn.symbol} = ${(parseFloat(q.out)/parseFloat(state.amountIn)).toFixed(4)} ${state.tokenOut.symbol}</span></div>
        <div class="quote-row"><span class="quote-key">Minimum received</span><span class="quote-val">${q.min} ${state.tokenOut.symbol}</span></div>
        <div class="quote-row"><span class="quote-key">Price impact</span><span class="quote-val ${parseFloat(q.impact)<1?'good':'warn'}">${q.impact}%</span></div>
        <div class="quote-row"><span class="quote-key">Network fee</span><span class="quote-val">${q.gas}</span></div>
      </div>`:''}

      ${state.swapping?`
      <button class="btn-swap disabled" disabled>
        <i class="ti ti-loader spin-anim" aria-hidden="true"></i> Swapping…
      </button>`:
      canSwap?`
      <button class="btn-swap ready" onclick="runSwap()">
        <i class="ti ti-arrows-exchange" aria-hidden="true"></i>
        Swap ${state.tokenIn.symbol} → ${state.tokenOut.symbol}
      </button>`:
      `<button class="btn-swap disabled" disabled>
        ${!state.connected?'Connect wallet to swap':'Enter an amount'}
      </button>`}
    </div>`;
}

function renderSteps(){
  if(!state.swapStep) return '';
  const steps = [
    {name:'Pre-flight checks',desc:'Verifying balance, private key, and network',icon:'ti-shield-check'},
    {name:'Check allowance',desc:`Reading ${state.tokenIn.symbol} allowance for DEX router`,icon:'ti-eye'},
    {name:'Approve token',desc:`Approving ${state.tokenIn.symbol} spend via cast send`,icon:'ti-check'},
    {name:'Execute swap',desc:`Swapping ${state.amountIn} ${state.tokenIn.symbol} → ${state.tokenOut.symbol}`,icon:'ti-arrows-exchange'},
    {name:'Confirmed',desc:'Transaction included in block',icon:'ti-circle-check'},
  ];
  return `
    <div class="steps-card">
      <div class="steps-title">Swap progress</div>
      ${steps.map((s,i)=>{
        const done = i<state.swapStep-1;
        const active = i===state.swapStep-1;
        const cls = done?'done':active?'active':'pending';
        return `
        <div class="step-item">
          <div class="step-dot ${cls}"><i class="ti ${done?'ti-check':active?'ti-loader':s.icon}" aria-hidden="true"></i></div>
          <div class="step-info">
            <div class="step-name">${s.name}</div>
            <div class="step-desc">${s.desc}</div>
            ${done&&i===3&&state.txHash?`<div class="step-hash" onclick="openExplorer()">${state.txHash} ↗</div>`:''}
          </div>
        </div>`}).join('')}
    </div>`;
}

function renderActivity(){
  const history = [
    {from:'USDC',to:'PHRS',amtIn:'50',amtOut:'23.36',time:'2m ago',hash:'0x1a2b...3c4d',status:'success'},
    {from:'PHRS',to:'USDT',amtIn:'5',amtOut:'10.68',time:'18m ago',hash:'0x5e6f...7a8b',status:'success'},
  ];
  if(!state.connected) return `<div style="text-align:center;padding:2rem;color:var(--color-text-secondary);font-size:13px">Connect wallet to see swap history</div>`;
  if(!history.length) return `<div style="text-align:center;padding:2rem;color:var(--color-text-secondary);font-size:13px">No swaps yet</div>`;
  return history.map(h=>`
    <div style="display:flex;align-items:center;justify-content:space-between;padding:.75rem 0;border-bottom:0.5px solid var(--color-border-tertiary)">
      <div style="display:flex;align-items:center;gap:8px">
        <div style="display:flex">
          ${tokenIcon(TOKENS.find(t=>t.symbol===h.from)||TOKENS[0],22)}
          <div style="margin-left:-6px">${tokenIcon(TOKENS.find(t=>t.symbol===h.to)||TOKENS[0],22)}</div>
        </div>
        <div>
          <div style="font-size:13px;font-weight:500;color:var(--color-text-primary)">${h.amtIn} ${h.from} → ${h.amtOut} ${h.to}</div>
          <div style="font-size:10px;font-family:var(--font-mono);color:var(--color-text-tertiary)">${h.hash}</div>
        </div>
      </div>
      <div style="text-align:right">
        <div style="font-size:11px;color:#0F6E56;font-weight:500">✓ confirmed</div>
        <div style="font-size:11px;color:var(--color-text-secondary)">${h.time}</div>
      </div>
    </div>`).join('');
}

function renderModal(){
  if(state.showWalletModal){
    return `
    <div class="modal-bg" onclick="closeModal()">
      <div class="modal" onclick="event.stopPropagation()">
        <div class="modal-title">
          Connect wallet
          <button class="modal-close" onclick="closeModal()">×</button>
        </div>
        <div class="wallet-option" onclick="connectWallet('MetaMask')">
          <div class="wallet-opt-icon" style="background:#FFF3E0">🦊</div>
          <div><div class="wallet-opt-name">MetaMask</div><div class="wallet-opt-desc">Browser extension wallet</div></div>
        </div>
        <div class="wallet-option" onclick="connectWallet('WalletConnect')">
          <div class="wallet-opt-icon" style="background:#E3F2FD">🔗</div>
          <div><div class="wallet-opt-name">WalletConnect</div><div class="wallet-opt-desc">Scan with mobile wallet</div></div>
        </div>
        <div class="wallet-option" onclick="connectWallet('Phantom')">
          <div class="wallet-opt-icon" style="background:#EDE7F6">👻</div>
          <div><div class="wallet-opt-name">Phantom</div><div class="wallet-opt-desc">Multi-chain wallet</div></div>
        </div>
        <div style="margin-top:.75rem;font-size:11px;color:var(--color-text-secondary);text-align:center">
          Connecting adds Pharos Atlantic Testnet (chain ID 688689)
        </div>
      </div>
    </div>`;
  }
  if(state.showTokenModal){
    const otherTok = state.showTokenModal==='in'?state.tokenOut:state.tokenIn;
    
    // Filter tokens based on search string and exclude active asset on opposite side
    const filteredTokens = TOKENS.filter(t => {
      if (t.symbol === otherTok.symbol) return false;
      if (!state.tokenSearchQuery) return true;
      const query = state.tokenSearchQuery.toLowerCase();
      return t.symbol.toLowerCase().includes(query) || t.name.toLowerCase().includes(query) || t.addr.toLowerCase().includes(query);
    });

    return `
    <div class="modal-bg token-modal" onclick="closeModal()">
      <div class="modal" onclick="event.stopPropagation()">
        <div class="modal-title">
          Select token
          <button class="modal-close" onclick="closeModal()">×</button>
        </div>
        <input class="search-input" id="token-search-box" placeholder="Search by name or address…" value="${state.tokenSearchQuery}" oninput="handleTokenSearch(this.value)">
        <div class="token-list-container" style="max-height: 280px; overflow-y: auto;">
          ${filteredTokens.length === 0 ? `<div style="text-align:center; padding: 1.5rem; color: var(--color-text-tertiary); font-size: 13px;">No tokens found</div>` : ''}
          ${filteredTokens.map(t=>`
          <div class="token-list-item" onclick="selectToken('${t.symbol}')">
            ${tokenIcon(t,28)}
            <div style="flex:1">
              <div class="tok-name">${t.symbol} — ${t.name}</div>
              <div class="tok-addr">${t.addr}</div>
            </div>
            ${state.connected?`<div class="tok-bal">${t.balance.toFixed(3)}</div>`:''}
          </div>`).join('')}
        </div>
      </div>
    </div>`;
  }
  return '';
}

function render(){
  const main = document.getElementById('main');
  main.innerHTML = renderWalletCard() +
    (state.swapStep>0 ? renderSteps() : '') +
    (state.view==='swap' ? renderSwap() : `
      <div class="swap-card">
        <div class="tab-row">
          <button class="tab" onclick="setView('swap')">Swap</button>
          <button class="tab active" onclick="setView('monitor')">Activity</button>
        </div>
        ${renderActivity()}
      </div>`);

  document.getElementById('modal-root').innerHTML = renderModal();
  
  // Retain focus on search input field if modal re-renders while user typing
  const searchBox = document.getElementById('token-search-box');
  if(searchBox) {
    searchBox.focus();
    searchBox.setSelectionRange(searchBox.value.length, searchBox.value.length);
  }
}

function openWalletModal(){state.showWalletModal=true;render()}
function closeModal(){state.showWalletModal=false;state.showTokenModal=null;state.tokenSearchQuery='';render()}
function openTokenModal(side){state.showTokenModal=side;state.tokenSearchQuery='';render()}

function handleTokenSearch(val) {
  state.tokenSearchQuery = val;
  render();
}

function connectWallet(name){
  state.connected=true;
  state.wallet='0x71C7...3b2e';
  state.showWalletModal=false;
  render();
}

function disconnect(){state.connected=false;state.wallet='';state.swapStep=0;render()}
function copyAddr(){navigator.clipboard&&navigator.clipboard.writeText(state.wallet)}

function setView(v){state.view=v;render()}
function setAmount(v){state.amountIn=v;render()}
function setSlippage(s){state.slippage=s;render()}
function setMax(){state.amountIn=state.tokenIn.balance.toFixed(3);render()}

function flipTokens(){
  const tmp=state.tokenIn;state.tokenIn=state.tokenOut;state.tokenOut=tmp;
  state.amountIn='';render();
}

function selectToken(sym){
  const tok=TOKENS.find(t=>t.symbol===sym);
  if(state.showTokenModal==='in') state.tokenIn=tok;
  else state.tokenOut=tok;
  state.showTokenModal=null;
  state.tokenSearchQuery='';
  state.amountIn='';
  render();
}

function openExplorer(){
  const url='https://atlantic.pharosscan.xyz/tx/'+state.txHash;
  if(typeof openLink==='function') openLink(url);
  else window.open(url,'_blank');
}

// Asynchronous clean workflow simulation loop
const sleep = ms => new Promise(resolve => setTimeout(resolve, ms));

async function runSwap(){
  if(!state.connected||!state.amountIn) return;
  
  state.swapping=true;
  state.swapStep=1; // Pre-flight checks
  render();
  
  try {
    await sleep(1200);
    state.swapStep=2; // Check allowance
    render();
    
    await sleep(900);
    state.swapStep=3; // Approve token
    render();
    
    await sleep(1400);
    state.swapStep=4; // Execute swap sequence
    state.txHash='0x'+Math.random().toString(16).slice(2,10)+'...'+Math.random().toString(16).slice(2,6);
    render();
    
    await sleep(1800);
    state.swapStep=5; // Complete transaction receipt confirmed block state
    
    const q=getQuote();
    if(q){
      state.tokenOut.balance = state.tokenOut.balance + parseFloat(q.out);
      state.tokenIn.balance = state.tokenIn.balance - parseFloat(state.amountIn);
    }
    state.amountIn='';
  } catch (err) {
    console.error("Simulation error caught: ", err);
  } finally {
    state.swapping=false;
    render();
  }
}

render();
</script>
</body>
</html>

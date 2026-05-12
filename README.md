<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Theria Wiki</title>
<link href="https://fonts.googleapis.com/css2?family=Cinzel:wght@400;600;700&family=Crimson+Pro:ital,wght@0,300;0,400;0,600;1,300;1,400&display=swap" rel="stylesheet">
<style>
*,*::before,*::after{box-sizing:border-box;margin:0;padding:0}
:root{--bg:#0e0c0a;--bg-card:#1c1710;--bg-sidebar:#120f0b;--border:#2e2518;--border-light:#3d3020;--gold:#c9a84c;--gold-dim:#8a6e32;--gold-pale:#f0d98a;--text:#e8dcc8;--text-muted:#9e8e72;--text-dim:#6b5c42;--red:#8b2020;--sidebar-w:270px;--header-h:56px}
html{scroll-behavior:smooth}
body{font-family:'Crimson Pro',Georgia,serif;background:var(--bg);color:var(--text);min-height:100vh;font-size:17px;line-height:1.75;overflow-x:hidden}
header{position:fixed;top:0;left:0;right:0;height:var(--header-h);background:var(--bg-sidebar);border-bottom:1px solid var(--border);display:flex;align-items:center;z-index:200;padding:0 20px;gap:16px}
.logo{font-family:'Cinzel',serif;font-size:20px;font-weight:700;color:var(--gold);letter-spacing:.08em;cursor:pointer;white-space:nowrap}
.logo span{color:var(--text-muted);font-weight:400;font-size:13px;margin-left:8px;letter-spacing:.15em;font-family:'Crimson Pro',serif;font-style:italic}
.hfill{flex:1}
.search-bar{display:flex;align-items:center;background:var(--bg-card);border:1px solid var(--border-light);border-radius:4px;padding:6px 12px;gap:8px;width:200px}
.search-bar input{background:none;border:none;outline:none;color:var(--text);font-family:'Crimson Pro',serif;font-size:14px;width:100%}
.search-bar input::placeholder{color:var(--text-dim)}
.menu-btn{display:none;background:none;border:none;color:var(--text-muted);cursor:pointer;padding:4px}
.layout{display:flex;padding-top:var(--header-h);min-height:100vh}
aside{position:fixed;top:var(--header-h);left:0;bottom:0;width:var(--sidebar-w);background:var(--bg-sidebar);border-right:1px solid var(--border);overflow-y:auto;z-index:90;padding-bottom:60px}
aside::-webkit-scrollbar{width:4px}
aside::-webkit-scrollbar-thumb{background:var(--border-light);border-radius:2px}
.sb-section{border-bottom:1px solid var(--border);transition:background .15s}
.sb-section.drag-over{background:rgba(201,168,76,.1);outline:2px dashed var(--gold-dim)}
.sb-section.dragging{opacity:.35}
.sb-header{display:flex;align-items:center;gap:8px;padding:12px 14px 10px;cursor:pointer;user-select:none}
.sb-header:hover{background:rgba(201,168,76,.06)}
.sb-drag-handle{color:var(--text-dim);flex-shrink:0;cursor:grab;opacity:0;transition:opacity .15s;font-size:14px;line-height:1;padding:2px}
.sb-header:hover .sb-drag-handle{opacity:1}
.sb-icon{width:15px;height:15px;color:var(--gold-dim);flex-shrink:0}
.sb-label{font-family:'Cinzel',serif;font-size:10px;font-weight:600;letter-spacing:.12em;color:var(--gold-dim);text-transform:uppercase;flex:1}
.sb-chevron{width:11px;height:11px;color:var(--text-dim);transition:transform .2s;flex-shrink:0}
.sb-section.open .sb-chevron{transform:rotate(180deg)}
.sb-links{display:none;padding:2px 0 4px}
.sb-section.open .sb-links{display:block}
.sb-links a{display:flex;align-items:center;padding:6px 14px 6px 42px;color:var(--text-muted);font-size:14px;cursor:pointer;transition:color .15s,background .15s;position:relative}
.sb-links a:hover{color:var(--gold-pale);background:rgba(201,168,76,.05)}
.sb-links a.active{color:var(--gold)}
.sb-links a.active::before{content:'';position:absolute;left:26px;top:50%;transform:translateY(-50%);width:3px;height:3px;border-radius:50%;background:var(--gold)}
.sb-new{display:flex;align-items:center;gap:5px;padding:7px 14px 9px 38px;color:var(--gold-dim);font-size:12px;cursor:pointer;font-style:italic;transition:color .15s}
.sb-new:hover{color:var(--gold)}
main{margin-left:var(--sidebar-w);flex:1;padding:40px 52px 100px;max-width:1000px}
.breadcrumb{display:flex;align-items:center;gap:6px;font-size:13px;color:var(--text-dim);margin-bottom:22px;font-style:italic}
.breadcrumb a{color:var(--gold-dim);text-decoration:none;cursor:pointer}
.breadcrumb a:hover{color:var(--gold)}
.page-header{display:flex;align-items:flex-start;justify-content:space-between;gap:16px;margin-bottom:6px}
.page-title{font-family:'Cinzel',serif;font-size:34px;font-weight:700;color:var(--gold-pale);line-height:1.2;letter-spacing:.02em}
.page-subtitle{font-size:16px;color:var(--text-muted);font-style:italic;margin-bottom:22px}
.divider{border:none;border-top:1px solid var(--border);margin:26px 0}
.gold-divider{border:none;border-top:1px solid var(--gold-dim);margin:26px 0;opacity:.35}
.btn{display:inline-flex;align-items:center;gap:5px;padding:6px 13px;border-radius:3px;font-family:'Cinzel',serif;font-size:10.5px;letter-spacing:.08em;cursor:pointer;transition:all .15s;border:1px solid;white-space:nowrap}
.btn-edit{background:transparent;border-color:var(--gold-dim);color:var(--gold-dim)}
.btn-edit:hover{background:rgba(201,168,76,.1);border-color:var(--gold);color:var(--gold)}
.btn-save{background:rgba(201,168,76,.15);border-color:var(--gold);color:var(--gold-pale)}
.btn-save:hover{background:rgba(201,168,76,.25)}
.btn-cancel{background:transparent;border-color:var(--border-light);color:var(--text-muted)}
.btn-cancel:hover{border-color:var(--text-muted);color:var(--text)}
.edit-bar{display:flex;align-items:center;gap:8px;flex-wrap:wrap;flex-shrink:0}
.saved-flash{font-size:12px;color:var(--gold);font-style:italic;opacity:0;transition:opacity .4s}
.saved-flash.show{opacity:1}
.editable-title{outline:none;border-bottom:2px solid var(--gold-dim);padding-bottom:3px;background:transparent;font-family:'Cinzel',serif;font-size:34px;font-weight:700;color:var(--gold-pale);line-height:1.2;letter-spacing:.02em;width:100%}
.editable-subtitle{outline:none;border-bottom:1px dashed var(--border-light);padding:2px 0;background:transparent;font-size:16px;color:var(--text-muted);font-style:italic;width:100%;font-family:'Crimson Pro',serif;margin-top:8px;display:block}
.editable-title:focus,.editable-subtitle:focus{border-color:var(--gold)}
.fmt-bar{display:flex;align-items:center;gap:3px;padding:7px 10px;background:var(--bg-card);border:1px solid var(--border-light);border-radius:3px;margin-bottom:10px;flex-wrap:wrap}
.fmt-btn{background:none;border:1px solid transparent;color:var(--text-muted);cursor:pointer;padding:4px 8px;border-radius:2px;font-size:13px;transition:all .15s;font-family:inherit}
.fmt-btn:hover{background:var(--border);color:var(--text)}
.fmt-sep{width:1px;height:16px;background:var(--border-light);margin:0 3px}
.editable-content{outline:none;min-height:140px;padding:14px;background:var(--bg-card);border:1px solid var(--border-light);border-radius:3px;color:var(--text);font-family:'Crimson Pro',serif;font-size:17px;line-height:1.75}
.editable-content:focus{border-color:var(--gold-dim)}
.editable-content h2{font-family:'Cinzel',serif;font-size:18px;color:var(--gold);margin:20px 0 10px;padding-bottom:6px;border-bottom:1px solid var(--border);letter-spacing:.04em}
.editable-content h3{font-family:'Cinzel',serif;font-size:14px;color:var(--text);margin:14px 0 6px;letter-spacing:.04em}
.editable-content p{margin-bottom:10px}
.editable-content ul{margin:0 0 10px 18px}
.editable-content blockquote{border-left:2px solid var(--gold-dim);padding:6px 14px;margin:12px 0;font-style:italic;color:var(--text-muted)}
.edit-hint{font-size:12px;color:var(--text-dim);margin-top:6px;font-style:italic}
.content h2{font-family:'Cinzel',serif;font-size:18px;font-weight:600;color:var(--gold);margin:30px 0 12px;padding-bottom:7px;border-bottom:1px solid var(--border);letter-spacing:.04em}
.content h3{font-family:'Cinzel',serif;font-size:14px;font-weight:600;color:var(--text);margin:18px 0 8px;letter-spacing:.04em}
.content p{margin-bottom:12px;color:var(--text)}
.content ul{margin:0 0 12px 18px;color:var(--text)}
.content li{margin-bottom:4px}
.content blockquote{border-left:2px solid var(--gold-dim);padding:9px 18px;margin:16px 0;font-style:italic;color:var(--text-muted);background:var(--bg-card)}
.content cite{display:block;margin-top:5px;font-size:13px;color:var(--text-dim);font-style:normal}
.notice{background:rgba(201,168,76,.07);border:1px solid var(--gold-dim);border-radius:2px;padding:11px 15px;font-size:14px;color:var(--text-muted);margin-bottom:20px;display:flex;gap:10px;align-items:flex-start}
.cat-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(130px,1fr));gap:12px;margin:18px 0}
.cat-card{background:var(--bg-card);border:1px solid var(--border-light);border-radius:2px;padding:15px 12px;cursor:pointer;transition:border-color .2s,background .2s;text-align:center}
.cat-card:hover{border-color:var(--gold-dim);background:rgba(201,168,76,.06)}
.cat-icon{font-size:24px;margin-bottom:8px;line-height:1}
.cat-name{font-family:'Cinzel',serif;font-size:10px;letter-spacing:.08em;color:var(--gold);text-transform:uppercase}
.stub-badge{display:inline-block;background:rgba(139,32,32,.3);border:1px solid var(--red);color:#d47070;font-size:10px;padding:2px 7px;border-radius:2px;font-family:'Cinzel',serif;letter-spacing:.06em;vertical-align:middle;margin-left:6px}

/* WIDGET SYSTEM */
.page-canvas{position:relative;min-height:100px}
.page-canvas.edit-mode .widget:hover{outline:2px dashed rgba(201,168,76,.4);outline-offset:3px}
.widget{position:relative;margin-bottom:16px;transition:opacity .15s}
.widget.dragging{opacity:.4}
.widget.drop-above{border-top:3px solid var(--gold)!important;padding-top:14px}
.widget.drop-below{border-bottom:3px solid var(--gold)!important;padding-bottom:14px}
.widget-chrome{position:absolute;top:6px;right:6px;display:none;gap:4px;z-index:10;align-items:center}
.page-canvas.edit-mode .widget:hover .widget-chrome{display:flex}
.wc-btn{background:var(--bg-sidebar);border:1px solid var(--border-light);color:var(--text-muted);border-radius:2px;padding:3px 7px;font-size:11px;cursor:pointer;transition:all .15s;font-family:'Cinzel',serif;letter-spacing:.03em;user-select:none}
.wc-btn:hover{border-color:var(--gold-dim);color:var(--gold)}
.wc-drag{cursor:grab}
.wc-drag:active{cursor:grabbing}

/* WIDGET TOOLBAR */
.widget-toolbar{position:fixed;bottom:0;left:var(--sidebar-w);right:0;display:none;justify-content:center;z-index:150;padding:10px 20px;background:linear-gradient(transparent,rgba(14,12,10,.95) 40%);pointer-events:none}
.widget-toolbar.visible{display:flex}
.wt-inner{background:var(--bg-sidebar);border:1px solid var(--border-light);border-radius:30px;padding:7px 12px;display:flex;align-items:center;gap:5px;pointer-events:all;flex-wrap:wrap;justify-content:center}
.wt-label{font-family:'Cinzel',serif;font-size:9px;letter-spacing:.1em;color:var(--text-dim);text-transform:uppercase;padding-right:8px;border-right:1px solid var(--border-light);margin-right:2px;white-space:nowrap}
.wt-btn{background:transparent;border:1px solid var(--border-light);color:var(--text-muted);border-radius:20px;padding:4px 10px;font-size:12px;cursor:pointer;transition:all .2s;white-space:nowrap;font-family:'Crimson Pro',serif}
.wt-btn:hover{border-color:var(--gold-dim);color:var(--gold);background:rgba(201,168,76,.08)}

/* INDIVIDUAL WIDGET STYLES */
.w-text{padding:2px 0}
.w-quote{border-left:3px solid var(--gold-dim);padding:12px 20px;background:var(--bg-card);border-radius:0 3px 3px 0}
.w-quote .qt{font-size:18px;font-style:italic;color:var(--text-muted);line-height:1.6;margin-bottom:7px}
.w-quote .qa{font-size:13px;color:var(--text-dim)}
.w-quote .qa::before{content:'— '}
.w-callout{border:1px solid var(--gold-dim);background:rgba(201,168,76,.06);border-radius:3px;padding:13px 16px;display:flex;gap:11px;align-items:flex-start}
.w-callout .ci{font-size:18px;flex-shrink:0;margin-top:2px}
.w-callout .ct{font-family:'Cinzel',serif;font-size:11px;letter-spacing:.08em;color:var(--gold);text-transform:uppercase;margin-bottom:4px}
.w-callout .cb{font-size:14px;color:var(--text-muted);line-height:1.6}
.w-char{background:var(--bg-card);border:1px solid var(--border-light);border-radius:3px;overflow:hidden;display:flex}
.w-char-portrait{width:100px;flex-shrink:0;background:#1a1208;display:flex;align-items:center;justify-content:center;min-height:130px}
.w-char-initial{font-family:'Cinzel',serif;font-size:44px;color:var(--gold-dim);opacity:.6;font-weight:700}
.w-char-body{padding:14px 16px;flex:1}
.w-char-name{font-family:'Cinzel',serif;font-size:16px;color:var(--gold-pale);margin-bottom:2px;letter-spacing:.04em}
.w-char-role{font-size:13px;color:var(--gold-dim);font-style:italic;margin-bottom:9px}
.w-char-desc{font-size:14px;color:var(--text-muted);line-height:1.6;margin-bottom:9px}
.w-char-tags{display:flex;gap:5px;flex-wrap:wrap}
.char-tag{background:rgba(201,168,76,.1);border:1px solid var(--border-light);color:var(--text-dim);font-size:10px;padding:2px 7px;border-radius:2px;font-family:'Cinzel',serif;letter-spacing:.04em}
.w-location{background:var(--bg-card);border:1px solid var(--border-light);border-radius:3px;overflow:hidden}
.w-loc-header{background:var(--border);padding:11px 14px;display:flex;align-items:center;gap:9px}
.w-loc-icon{font-size:20px}
.w-loc-name{font-family:'Cinzel',serif;font-size:14px;color:var(--gold-pale);letter-spacing:.04em}
.w-loc-type{font-size:11px;color:var(--text-dim);font-style:italic}
.w-loc-body{padding:13px 14px}
.w-loc-desc{font-size:14px;color:var(--text-muted);line-height:1.6;margin-bottom:11px}
.loc-stats{display:grid;grid-template-columns:repeat(3,1fr);gap:8px}
.loc-stat{text-align:center;background:var(--bg-sidebar);border-radius:2px;padding:7px 5px}
.loc-stat-val{font-family:'Cinzel',serif;font-size:13px;color:var(--gold);display:block}
.loc-stat-lbl{font-size:11px;color:var(--text-dim)}
.w-faction{background:var(--bg-card);border:1px solid var(--border-light);border-radius:3px;padding:16px;display:flex;gap:14px;align-items:flex-start}
.faction-emblem{width:58px;height:58px;border-radius:50%;background:var(--border);display:flex;align-items:center;justify-content:center;font-size:26px;flex-shrink:0;border:2px solid var(--border-light)}
.faction-info{flex:1}
.faction-name{font-family:'Cinzel',serif;font-size:15px;color:var(--gold-pale);letter-spacing:.04em;margin-bottom:2px}
.faction-type{font-size:12px;color:var(--gold-dim);font-style:italic;margin-bottom:7px}
.faction-desc{font-size:14px;color:var(--text-muted);line-height:1.6}
.w-seasons{background:var(--bg-card);border:1px solid var(--border-light);border-radius:3px;padding:16px}
.w-seasons-title{font-family:'Cinzel',serif;font-size:11px;letter-spacing:.1em;color:var(--gold);text-transform:uppercase;margin-bottom:13px}
.seasons-grid{display:grid;grid-template-columns:repeat(4,1fr);gap:10px}
.season-col{text-align:center}
.season-name{font-family:'Cinzel',serif;font-size:9px;letter-spacing:.08em;color:var(--text-dim);text-transform:uppercase;margin-bottom:5px}
.season-icon{font-size:20px;margin-bottom:5px;display:block}
.season-temp{font-family:'Cinzel',serif;font-size:14px;color:var(--gold-pale)}
.season-desc{font-size:11px;color:var(--text-dim);margin-top:3px;line-height:1.4}
.season-bar{height:56px;display:flex;align-items:flex-end;justify-content:center;margin-bottom:4px}
.season-bar-fill{width:20px;border-radius:3px 3px 0 0;transition:height .3s}
.w-timeline{padding:2px 0}
.tl-title{font-family:'Cinzel',serif;font-size:11px;letter-spacing:.1em;color:var(--gold);text-transform:uppercase;margin-bottom:14px}
.tl-track{position:relative;padding-left:26px}
.tl-track::before{content:'';position:absolute;left:7px;top:6px;bottom:6px;width:1px;background:var(--border-light)}
.tl-event{position:relative;margin-bottom:16px}
.tl-dot{position:absolute;left:-22px;top:5px;width:9px;height:9px;border-radius:50%;background:var(--gold-dim);border:2px solid var(--bg)}
.tl-dot.major{background:var(--gold);width:11px;height:11px;left:-23px;box-shadow:0 0 0 3px rgba(201,168,76,.2)}
.tl-year{font-family:'Cinzel',serif;font-size:10px;color:var(--gold-dim);letter-spacing:.06em;margin-bottom:1px}
.tl-event-title{font-family:'Cinzel',serif;font-size:13px;color:var(--text);margin-bottom:2px;letter-spacing:.03em}
.tl-event-desc{font-size:13px;color:var(--text-muted);line-height:1.5}
.w-stats{background:var(--bg-card);border:1px solid var(--border-light);border-radius:3px;padding:16px}
.stats-title{font-family:'Cinzel',serif;font-size:11px;letter-spacing:.1em;color:var(--gold);text-transform:uppercase;margin-bottom:13px}
.stat-row{display:flex;align-items:center;gap:10px;margin-bottom:9px}
.stat-label{font-size:13px;color:var(--text-muted);width:120px;flex-shrink:0}
.stat-track{flex:1;height:7px;background:var(--border);border-radius:4px;overflow:hidden}
.stat-fill{height:100%;border-radius:4px;background:var(--gold-dim)}
.stat-val{font-family:'Cinzel',serif;font-size:11px;color:var(--gold-dim);width:34px;text-align:right;flex-shrink:0}
.w-table{overflow-x:auto}
.wiki-table{width:100%;border-collapse:collapse;font-size:14px}
.wiki-table th{font-family:'Cinzel',serif;font-size:10px;letter-spacing:.1em;text-transform:uppercase;color:var(--gold-dim);padding:7px 11px;border-bottom:1px solid var(--border-light);text-align:left;background:var(--bg-card)}
.wiki-table td{padding:7px 11px;border-bottom:1px solid var(--border);color:var(--text-muted);line-height:1.4}
.wiki-table tr:last-child td{border-bottom:none}
.wiki-table tr:hover td{background:rgba(201,168,76,.03)}
.w-divider{display:flex;align-items:center;gap:14px;padding:6px 0;color:var(--gold-dim);opacity:.5}
.w-divider::before,.w-divider::after{content:'';flex:1;height:1px;background:var(--gold-dim)}
.w-divider-sym{font-size:13px;flex-shrink:0}
.w-map{background:var(--bg-card);border:1px solid var(--border-light);border-radius:3px;padding:16px}
.map-area{height:130px;background:linear-gradient(135deg,#0e1a10 0%,#0a1208 40%,#161008 70%,#1a1205 100%);border-radius:2px;position:relative;overflow:hidden;margin-bottom:9px;border:1px solid var(--border)}
.map-pin{position:absolute;font-size:14px;transform:translate(-50%,-100%);pointer-events:none}
.map-pin-label{position:absolute;font-family:'Cinzel',serif;font-size:8px;color:var(--gold);letter-spacing:.06em;transform:translate(-50%,2px);white-space:nowrap;text-shadow:0 1px 3px rgba(0,0,0,.9);pointer-events:none}
.map-caption{font-size:13px;color:var(--text-dim);font-style:italic;text-align:center}

/* MODAL */
.modal-bg{position:fixed;inset:0;background:rgba(0,0,0,.8);z-index:300;display:flex;align-items:center;justify-content:center;padding:20px}
.modal{background:var(--bg-card);border:1px solid var(--border-light);border-radius:4px;padding:26px;width:500px;max-width:100%;max-height:86vh;overflow-y:auto}
.modal::-webkit-scrollbar{width:4px}
.modal::-webkit-scrollbar-thumb{background:var(--border-light)}
.modal-title{font-family:'Cinzel',serif;font-size:14px;color:var(--gold);margin-bottom:18px;letter-spacing:.06em}
.fl{display:block;font-size:10px;color:var(--text-dim);margin-bottom:4px;margin-top:14px;font-family:'Cinzel',serif;letter-spacing:.08em;text-transform:uppercase}
.fl:first-of-type{margin-top:0}
.modal input,.modal select,.modal textarea{width:100%;background:var(--bg-sidebar);border:1px solid var(--border-light);color:var(--text);font-family:'Crimson Pro',serif;font-size:15px;padding:7px 10px;border-radius:2px;outline:none;transition:border-color .15s}
.modal input:focus,.modal select:focus,.modal textarea:focus{border-color:var(--gold-dim)}
.modal textarea{min-height:65px;resize:vertical;line-height:1.5}
.modal select option{background:var(--bg-card)}
.modal-actions{display:flex;gap:10px;margin-top:20px;justify-content:flex-end}
.modal-row{display:grid;grid-template-columns:1fr 1fr;gap:10px}
.tl-ev-wrap{display:flex;flex-direction:column;gap:0;margin-bottom:8px}
.tl-ev-top{display:flex;gap:6px;align-items:center;background:var(--bg-sidebar);border:1px solid var(--border);border-radius:2px 2px 0 0;padding:6px 8px}
.tl-ev-top input{background:none;border:none;border-bottom:1px solid var(--border-light);border-radius:0;padding:2px 0;font-size:13px;color:var(--text)}
.tl-ev-top input:focus{border-color:var(--gold-dim);outline:none}
.tl-ev-bot{background:var(--bg-sidebar);border:1px solid var(--border);border-top:none;border-radius:0 0 2px 2px;padding:6px 8px}
.tl-ev-bot textarea{background:none;border:none;padding:0;min-height:36px;font-size:13px;color:var(--text-muted);width:100%;outline:none;resize:none;font-family:'Crimson Pro',serif}
.ev-yr{width:80px;flex-shrink:0}
.ev-ti{flex:1}
.ev-rm{background:none;border:none;color:var(--text-dim);cursor:pointer;font-size:14px;padding:0 3px;transition:color .15s;flex-shrink:0}
.ev-rm:hover{color:#d47070}
.ev-major{display:flex;align-items:center;gap:5px;font-size:11px;color:var(--text-dim);margin-top:4px}
.ev-major input{width:auto;background:none;border:none;padding:0;accent-color:var(--gold)}
.add-row-btn{background:none;border:1px dashed var(--border-light);color:var(--text-dim);border-radius:2px;padding:5px 10px;width:100%;cursor:pointer;font-size:13px;font-family:'Crimson Pro',serif;transition:all .15s;margin-top:4px}
.add-row-btn:hover{border-color:var(--gold-dim);color:var(--gold-dim)}
.stat-edit-row{display:flex;gap:7px;align-items:center;margin-bottom:7px}
.stat-edit-row input[type=text]{flex:1}
.stat-edit-row input[type=range]{width:90px;flex:none;accent-color:var(--gold)}
.stat-edit-row .sv{font-family:'Cinzel',serif;font-size:11px;color:var(--gold);width:36px;text-align:right;flex-shrink:0}
.stat-rm{background:none;border:none;color:var(--text-dim);cursor:pointer;font-size:14px;padding:0 3px;transition:color .15s}
.stat-rm:hover{color:#d47070}
.table-edit{overflow-x:auto;margin-top:6px}
.table-edit table{border-collapse:collapse}
.table-edit td,.table-edit th{padding:0}
.table-edit input{background:var(--bg-sidebar);border:1px solid var(--border);color:var(--text);font-family:'Crimson Pro',serif;font-size:13px;padding:5px 7px;width:100%;min-width:80px;outline:none}
.table-edit th input{font-family:'Cinzel',serif;font-size:10px;color:var(--gold-dim)}
.table-edit input:focus{border-color:var(--gold-dim)}
.table-edit .del-btn{background:none;border:1px solid var(--border);color:var(--text-dim);cursor:pointer;font-size:11px;padding:4px 6px;transition:all .15s}
.table-edit .del-btn:hover{border-color:var(--red);color:#d47070}
.season-edit-grid{display:grid;grid-template-columns:1fr 1fr;gap:10px;margin-top:6px}
.season-edit-box{background:var(--bg-sidebar);border:1px solid var(--border);border-radius:2px;padding:9px}
.season-edit-box .se-title{font-family:'Cinzel',serif;font-size:9px;color:var(--gold-dim);text-transform:uppercase;letter-spacing:.08em;margin-bottom:7px}
.season-edit-box input{margin-bottom:5px}
.map-pin-row{display:flex;gap:6px;align-items:center;margin-bottom:6px;flex-wrap:wrap}
.map-pin-row input{background:var(--bg-sidebar);border:1px solid var(--border-light);color:var(--text);font-family:'Crimson Pro',serif;font-size:14px;padding:5px 8px;border-radius:2px;outline:none}
.map-pin-row input:focus{border-color:var(--gold-dim)}
.pin-emoji{width:48px}
.pin-label{flex:1;min-width:70px}
.pin-xy{width:54px}

@media(max-width:768px){
  :root{--sidebar-w:0px}
  aside{transform:translateX(-100%);width:270px;transition:transform .25s}
  aside.open{transform:translateX(0)}
  main{margin-left:0;padding:22px 16px 80px}
  .menu-btn{display:block}
  .page-title,.editable-title{font-size:24px}
  .seasons-grid{grid-template-columns:repeat(2,1fr)}
  .widget-toolbar{left:0}
  .overlay{display:none;position:fixed;inset:0;background:rgba(0,0,0,.6);z-index:89}
  .overlay.show{display:block}
}
</style>
</head>
<body>
<header>
  <button class="menu-btn" onclick="toggleSidebar()" aria-label="menu">
    <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><line x1="3" y1="6" x2="21" y2="6"/><line x1="3" y1="12" x2="21" y2="12"/><line x1="3" y1="18" x2="21" y2="18"/></svg>
  </button>
  <span class="logo" onclick="showPage('home')">THERIA<span>The Living World</span></span>
  <div class="hfill"></div>
  <div class="search-bar">
    <svg width="13" height="13" viewBox="0 0 24 24" fill="none" stroke="var(--text-dim)" stroke-width="2"><circle cx="11" cy="11" r="8"/><line x1="21" y1="21" x2="16.65" y2="16.65"/></svg>
    <input type="text" placeholder="Search…" id="search-input" onkeyup="handleSearch(event)">
  </div>
</header>
<div class="overlay" id="overlay" onclick="toggleSidebar()"></div>
<div class="layout">
  <aside id="sidebar"><div id="sb-container"></div></aside>
  <main id="main-content"></main>
</div>
<div class="widget-toolbar" id="widget-toolbar">
  <div class="wt-inner">
    <span class="wt-label">+ Widget</span>
    <button class="wt-btn" onclick="addWidget('text')">📝 Text</button>
    <button class="wt-btn" onclick="addWidget('quote')">💬 Quote</button>
    <button class="wt-btn" onclick="addWidget('callout')">📌 Callout</button>
    <button class="wt-btn" onclick="addWidget('character')">👤 Character</button>
    <button class="wt-btn" onclick="addWidget('location')">🏰 Location</button>
    <button class="wt-btn" onclick="addWidget('faction')">⚔️ Faction</button>
    <button class="wt-btn" onclick="addWidget('seasons')">🌤 Seasons</button>
    <button class="wt-btn" onclick="addWidget('timeline')">📅 Timeline</button>
    <button class="wt-btn" onclick="addWidget('stats')">📊 Stats</button>
    <button class="wt-btn" onclick="addWidget('table')">📋 Table</button>
    <button class="wt-btn" onclick="addWidget('divider')">— Divider</button>
    <button class="wt-btn" onclick="addWidget('map')">🗺 Map</button>
  </div>
</div>
<div id="modal-root"></div>

<script>
// ═══════════════════════════════════════════
//  STATE
// ═══════════════════════════════════════════
var currentPage = 'home';
var isEditing = false;
var customPages = {};
var customSidebarLinks = {};
var sidebarOrder = [];
var dragWidgetId = null;
var sbDragId = null;

// ═══════════════════════════════════════════
//  SIDEBAR DEFINITIONS
// ═══════════════════════════════════════════
var SECTIONS = [
  {id:'overview', label:'Overview & Systems',
   icon:'<path d="M12 2L2 7l10 5 10-5-10-5z"/><path d="M2 17l10 5 10-5"/><path d="M2 12l10 5 10-5"/>',
   links:[{l:'Welcome to Theria',k:'home'},{l:'The Arcane System',k:'magic'},{l:'World Geography',k:'geography'},{l:'Calendar & Time',k:'calendar'},{l:'Bestiary',k:'bestiary'},{l:'Economy & Trade',k:'economy',stub:true}]},
  {id:'factions', label:'Factions',
   icon:'<path d="M17 21v-2a4 4 0 0 0-4-4H5a4 4 0 0 0-4 4v2"/><circle cx="9" cy="7" r="4"/><path d="M23 21v-2a4 4 0 0 0-3-3.87"/><path d="M16 3.13a4 4 0 0 1 0 7.75"/>',
   links:[{l:'All Factions',k:'factions'},{l:'The Auric Conclave',k:'stub'},{l:'The Iron Brotherhood',k:'stub'},{l:'The Thornwood Circle',k:'stub'},{l:'The Pale Court',k:'stub'},{l:'The Mireborn Pact',k:'stub',stub:true}]},
  {id:'locations', label:'Locations',
   icon:'<path d="M21 10c0 7-9 13-9 13s-9-6-9-13a9 9 0 0 1 18 0z"/><circle cx="12" cy="10" r="3"/>',
   links:[{l:'All Locations',k:'locations'},{l:'Veranthas (Capital)',k:'stub'},{l:'The Ashfield Plains',k:'stub'},{l:'Durath Mountains',k:'stub'},{l:'The Sunken Sea',k:'stub'},{l:'Mirewood Forest',k:'stub',stub:true}]},
  {id:'races', label:'Races',
   icon:'<path d="M17 21v-2a4 4 0 0 0-4-4H8a4 4 0 0 0-4 4v2"/><circle cx="12" cy="7" r="4"/>',
   links:[{l:'All Races',k:'species'},{l:'Humans',k:'stub'},{l:'The Vaeren (Elves)',k:'stub'},{l:'Stonekin (Dwarves)',k:'stub'},{l:'The Dusk-Born',k:'stub'},{l:'The Hollowed',k:'stub',stub:true}]},
  {id:'characters', label:'Characters',
   icon:'<circle cx="12" cy="8" r="4"/><path d="M4 20c0-4 3.6-7 8-7s8 3 8 7"/>',
   links:[{l:'All Characters',k:'characters'},{l:'Notable Figures',k:'stub'},{l:'Rulers & Monarchs',k:'stub'},{l:'Legendary Heroes',k:'stub'},{l:'Villains & Antagonists',k:'stub',stub:true}]},
  {id:'history', label:'History & Timelines',
   icon:'<circle cx="12" cy="12" r="10"/><polyline points="12 6 12 12 16 14"/>',
   links:[{l:'Full Timeline',k:'history'},{l:'The First Age',k:'stub'},{l:'The Age of Flame',k:'stub'},{l:'The Sundering War',k:'stub'},{l:'Prophecies & Omens',k:'stub',stub:true}]},
  {id:'research', label:'Research',
   icon:'<path d="M2 3h6a4 4 0 0 1 4 4v14a3 3 0 0 0-3-3H2z"/><path d="M22 3h-6a4 4 0 0 0-4 4v14a3 3 0 0 1 3-3h7z"/>',
   links:[{l:'Research Hub',k:'research'},{l:'Artifacts & Relics',k:'stub'},{l:'Lore Fragments',k:'stub'},{l:'Open Questions',k:'stub',stub:true}]},
];

// ═══════════════════════════════════════════
//  DEFAULT WIDGETS  (no backticks inside obj)
// ═══════════════════════════════════════════
function getDefaultWidgets(key) {
  var dw = {
    home:[
      {id:'dw1',type:'text',data:{html:'<p><strong style="color:var(--gold-pale)">Theria</strong> is a world of ancient magic, fractured empires, and a history stretching back beyond mortal memory. Once unified under the Auric Conclave, the world was shattered by the Sundering War three centuries ago.</p>'}},
      {id:'dw2',type:'callout',data:{icon:'📖',title:'Getting Started',body:'Click \u2712 Edit on any page to write lore. Use the + Widget toolbar at the bottom to add interactive blocks. Drag the \u283f handle on widgets to reorder. Drag sidebar section headers to reorder the navigation.'}}
    ],
    magic:[
      {id:'dw1',type:'text',data:{html:'<h2>Overview</h2><p>All magic in Theria draws on <strong style="color:var(--gold-pale)">The Weave</strong> \u2014 a lattice of arcane energy permeating all matter. The Weave was laid down by the Firstborn and is anchored by a network of monolithic stones across every continent.</p>'}},
      {id:'dw2',type:'stats',data:{title:'Arcane Disciplines',stats:[{label:'Weave-Threading',val:90},{label:'Elemental Shaping',val:72},{label:'Mind-Touch',val:55},{label:'Bone-Craft',val:38},{label:'Void-Work',val:20}]}},
      {id:'dw3',type:'text',data:{html:'<h2>Core Principles</h2><ul><li><strong>The Weave cannot be created or destroyed</strong> \u2014 only redirected.</li><li><strong>Casting has a cost</strong> \u2014 drawing on the Weave drains the practitioner\'s life-energy.</li><li><strong>Anchor-stones regulate flow</strong> \u2014 without them, Weave energy pools erratically.</li></ul>'}}
    ],
    bestiary:[
      {id:'dw1',type:'text',data:{html:'<h2>Classification</h2><p>Theriac naturalists classify creatures into four categories: <strong>Natural</strong>, <strong>Weave-touched</strong>, <strong>Arcane</strong>, and <strong>Hollowed</strong>.</p>'}},
      {id:'dw2',type:'character',data:{name:'Ashfield Wyvern',role:'Weave-touched Beast',desc:'A large, six-limbed reptile native to the Durath Mountains. Breathes superheated air. Territorial but rarely aggressive unless provoked.',tags:['Weave-touched','Reptile','Durath'],initial:'\ud83d\udc09'}},
      {id:'dw3',type:'character',data:{name:'The Mirewood Shade',role:'Arcane Entity (Disputed)',desc:'A shifting silhouette that mimics whoever observes it. The Thornwood Circle insists it is a forest spirit, not a creature.',tags:['Arcane','Mirewood','Disputed'],initial:'\ud83d\udc41'}}
    ],
    factions:[
      {id:'dw1',type:'faction',data:{emblem:'\u2696\ufe0f',name:'The Auric Conclave',type:'Arcane Council',desc:'Once the ruling body of the Unified Empire. Now a council of archmages clinging to legitimacy in Veranthas, guarding the Weave\'s primary anchor-stones.'}},
      {id:'dw2',type:'faction',data:{emblem:'\ud83d\udd25',name:'The Iron Brotherhood',type:'Militant Order',desc:'Soldier-priests who worship the Eternal Flame. They control the Durath Mountain passes and command the most disciplined army in Theria.'}},
      {id:'dw3',type:'faction',data:{emblem:'\ud83c\udf3f',name:'The Thornwood Circle',type:'Druidic Coalition',desc:'Vaeren elders, human hedge-witches, and Thornkin spirits who govern Mirewood Forest and oppose expansion into the old growth.'}},
      {id:'dw4',type:'faction',data:{emblem:'\ud83c\udf19',name:'The Pale Court',type:'Government-in-Exile',desc:'Believed to be the Dusk-Born\'s hidden authority, operating beneath the Sunken Sea. Their motives are poorly understood.'}}
    ],
    locations:[
      {id:'dw1',type:'location',data:{icon:'\ud83c\udfd9',name:'Veranthas',type:'Imperial Capital',desc:'The former Imperial Capital, home to 300,000 souls and the Grand Archive. Built atop ruins of three older cities.',stat1:'300k',lbl1:'Population',stat2:'3',lbl2:'Layers of Ruin',stat3:'312',lbl3:'Years Old'}},
      {id:'dw2',type:'seasons',data:{location:'The Ashfield Plains',spring:{temp:'14\u00b0C',desc:'Dry winds, sparse bloom'},summer:{temp:'31\u00b0C',desc:'Scorching, ash-haze skies'},autumn:{temp:'18\u00b0C',desc:'Cool, mineral-scented'},winter:{temp:'-4\u00b0C',desc:'Grey frost, rare snow'}}},
      {id:'dw3',type:'location',data:{icon:'\u26f0',name:'Durath Mountains',type:'Mountain Range',desc:'A massive east-west range dividing northern and southern Theria. Home to the Stonekin and wyverns.',stat1:'4,200m',lbl1:'Peak Height',stat2:'7',lbl2:'Known Passes',stat3:'200k',lbl3:'Stonekin Pop.'}}
    ],
    species:[
      {id:'dw1',type:'character',data:{name:'The Vaeren',role:'Ancient Race \u2022 Lifespan: ~600 years',desc:'The oldest sapient people in Theria with innate Weave sensitivity. They dwell in deep forests or isolated enclaves.',tags:['Forest-Dwellers','Weave-Sensitive','Long-Lived'],initial:'V'}},
      {id:'dw2',type:'character',data:{name:'Stonekin',role:'Subterranean Race \u2022 Lifespan: ~225 years',desc:'Stocky, stone-grey master craftspeople and engineers. Their mountain-cities predate the Unified Empire.',tags:['Underground','Craftspeople','Mountain'],initial:'S'}},
      {id:'dw3',type:'stats',data:{title:'Racial Lifespans (relative)',stats:[{label:'Humans',val:8},{label:'Stonekin',val:23},{label:'Dusk-Born',val:30},{label:'Vaeren',val:60},{label:'Firstborn',val:100}]}}
    ],
    characters:[
      {id:'dw1',type:'character',data:{name:'Archon Selindra Vaur',role:'Head of the Auric Conclave',desc:'An elderly Vaeren woman of prodigious arcane talent. She has ruled the Conclave for 120 years and shows no sign of relinquishing power.',tags:['Vaeren','Arcane','Conclave'],initial:'S'}},
      {id:'dw2',type:'character',data:{name:'Warlord Brek Stonehammer',role:'Commander, Iron Brotherhood (East)',desc:'A human soldier of common birth who rose through pure martial ability. Widely regarded as the most dangerous individual in Theria in open battle.',tags:['Human','Military','Brotherhood'],initial:'B'}},
      {id:'dw3',type:'quote',data:{text:'To know the Pale Emperor is to know that Theria was once something greater, and something far more terrible.',attr:'Mira of the Seven Lanterns, Chronicle of the Broken Throne'}}
    ],
    history:[
      {id:'dw1',type:'timeline',data:{title:'The Ages of Theria',events:[
        {year:'Before reckoning',title:'The First Age',desc:'Inhabited by the Firstborn \u2014 beings of pure arcane energy who shaped the continents and seeded the Weave.',major:true},
        {year:'~4000\u20132500 years ago',title:'Age of Flame',desc:'Catastrophic volcanic period. Multiple continents reshaped. Stonekin and Vaeren retreated to their strongholds.',major:false},
        {year:'~2500\u2013312 years ago',title:'The Second Age & the Empire',desc:'Rise of human civilisation. The Unified Empire at its height rules all of Theria for 800 years.',major:true},
        {year:'312 years ago',title:'The Sundering War',desc:'A thirty-year civil war following the death of the Pale Emperor. Three cities destroyed. Multiple anchor-stones damaged.',major:true},
        {year:'Present \u2014 Year 312',title:'The Third Age',desc:'Theria rebuilds. The Hollowing spreads from the north. Something stirs beneath the Sunken Sea.',major:false}
      ]}}
    ],
    research:[
      {id:'dw1',type:'callout',data:{icon:'\u26a0\ufe0f',title:'Active Crisis: The Hollowing',body:'An expanding region of magical corruption spreading from the northern wastes. Affected individuals lose memory, then personality, then physical form. Classification: Weave-poisoning.'}},
      {id:'dw2',type:'text',data:{html:'<h2>Active Research Topics</h2><h3>The Sunken Archive</h3><p>A legendary repository of First Age knowledge believed submerged beneath the Sunken Sea. Three expeditions launched; none returned with verifiable evidence.</p><h3>The Sixteenth Crown</h3><p>Last known possession of the Pale Emperor. Disappeared at the end of the Sundering War. Several factions believe it carries binding authority over the Weave\'s anchor-stones.</p>'}}
    ],
    stub:[{id:'dw1',type:'callout',data:{icon:'\u270f\ufe0f',title:'Empty Page',body:'Click \u2712 Edit above to start writing, or use the + Widget toolbar to add content blocks.'}}],
    geography:[{id:'dw1',type:'map',data:{caption:'Known regions of Theria',pins:[{x:30,y:40,emoji:'\ud83c\udfd9',label:'Veranthas'},{x:65,y:25,emoji:'\u26f0',label:'Durath Mtns'},{x:20,y:65,emoji:'\ud83c\udf32',label:'Mirewood'},{x:72,y:68,emoji:'\ud83c\udf0a',label:'Sunken Sea'},{x:50,y:78,emoji:'\ud83c\udfd5',label:'Ashfields'}]}}],
    calendar:[{id:'dw1',type:'seasons',data:{location:'Theria (temperate average)',spring:{temp:'12\u00b0C',desc:'Mild rains, new growth'},summer:{temp:'26\u00b0C',desc:'Warm and bright'},autumn:{temp:'14\u00b0C',desc:'Golden, windy'},winter:{temp:'-2\u00b0C',desc:'Cold snaps, grey skies'}}}],
    economy:[{id:'dw1',type:'stats',data:{title:'Trade Goods by Volume',stats:[{label:'Ore & Metals',val:85},{label:'Grain & Produce',val:70},{label:'Woven Textiles',val:55},{label:'Arcane Components',val:40},{label:'Luxury Goods',val:25}]}}]
  };
  return dw[key] ? JSON.parse(JSON.stringify(dw[key])) : JSON.parse(JSON.stringify(dw.stub));
}

var DEFAULT_META = {
  home:{title:'Welcome to Theria',subtitle:'The encyclopaedia of the Living World'},
  magic:{title:'The Arcane System',subtitle:'How magic works in Theria \u2014 The Weave'},
  bestiary:{title:'Bestiary',subtitle:'A catalogue of the creatures and beasts of Theria'},
  factions:{title:'Factions of Theria',subtitle:'The powers, orders, and coalitions that shape the world\'s politics'},
  locations:{title:'Locations',subtitle:'Cities, regions, and wilderness of the known world'},
  species:{title:'Races of Theria',subtitle:'The peoples of the Living World'},
  characters:{title:'Characters',subtitle:'Notable individuals who have shaped or are shaping the world'},
  history:{title:'History & Timelines',subtitle:'From the First Making to the present day'},
  research:{title:'Research Hub',subtitle:'Ongoing scholarly work, open questions, and contested theories'},
  geography:{title:'World Geography',subtitle:'The shape of the known world'},
  calendar:{title:'Calendar & Time',subtitle:'How Theria measures the years'},
  economy:{title:'Economy & Trade',subtitle:'Commerce, currency, and mercantile guilds'},
  stub:{title:'Article Stub',subtitle:'This page has not yet been written'}
};

// ═══════════════════════════════════════════
//  STORAGE
// ═══════════════════════════════════════════
function loadData() {
  var p1 = (window.storage ? window.storage.get('tw-pages') : Promise.reject()).then(function(r){ if(r) customPages = JSON.parse(r.value); }).catch(function(){});
  var p2 = (window.storage ? window.storage.get('tw-sidebar') : Promise.reject()).then(function(r){ if(r) customSidebarLinks = JSON.parse(r.value); }).catch(function(){});
  var p3 = (window.storage ? window.storage.get('tw-sborder') : Promise.reject()).then(function(r){ if(r) sidebarOrder = JSON.parse(r.value); }).catch(function(){});
  return Promise.all([p1,p2,p3]);
}
function savePages(){ if(window.storage) window.storage.set('tw-pages', JSON.stringify(customPages)).catch(function(){}); }
function saveSidebarLinks(){ if(window.storage) window.storage.set('tw-sidebar', JSON.stringify(customSidebarLinks)).catch(function(){}); }
function saveSbOrder(){ if(window.storage) window.storage.set('tw-sborder', JSON.stringify(sidebarOrder)).catch(function(){}); }

// ═══════════════════════════════════════════
//  SIDEBAR
// ═══════════════════════════════════════════
function buildSidebar() {
  var container = document.getElementById('sb-container');
  var order = sidebarOrder.length ? sidebarOrder : SECTIONS.map(function(s){return s.id;});
  SECTIONS.forEach(function(s){ if(order.indexOf(s.id)<0) order.push(s.id); });
  container.innerHTML = '';
  order.forEach(function(id){
    var sec = null;
    for(var i=0;i<SECTIONS.length;i++){if(SECTIONS[i].id===id){sec=SECTIONS[i];break;}}
    if(!sec) return;
    var customLinks = customSidebarLinks[sec.id]||[];
    var div = document.createElement('div');
    div.className = 'sb-section open';
    div.id = 'sbsec-'+sec.id;
    var linksHtml = sec.links.map(function(lk){
      return '<a onclick="showPage(\''+lk.k+'\')" style="'+(lk.stub?'font-style:italic;color:var(--text-dim);font-size:13px':'')+'">' + escHtml(lk.l) + '</a>';
    }).join('');
    customLinks.forEach(function(lk){
      linksHtml += '<a onclick="showPage(\''+lk.key+'\')">'+escHtml(lk.label)+'</a>';
    });
    div.innerHTML =
      '<div class="sb-header" onclick="toggleSbSection(\'sbsec-'+sec.id+'\')">' +
        '<span class="sb-drag-handle" draggable="true" onmousedown="sbDragId=\''+sec.id+'\'" onclick="event.stopPropagation()" title="Drag to reorder">\u283f</span>' +
        '<svg class="sb-icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">'+sec.icon+'</svg>' +
        '<span class="sb-label">'+sec.label+'</span>' +
        '<svg class="sb-chevron" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><polyline points="6 9 12 15 18 9"/></svg>' +
      '</div>' +
      '<div class="sb-links" id="sblinks-'+sec.id+'">'+linksHtml+'</div>' +
      '<div class="sb-new" onclick="openNewPageModal(\''+sec.id+'\')">+ new page</div>';
    div.addEventListener('dragstart', function(e){ if(!sbDragId) return; e.dataTransfer.effectAllowed='move'; div.classList.add('dragging'); });
    div.addEventListener('dragend', function(){ div.classList.remove('dragging'); sbDragId=null; document.querySelectorAll('.sb-section').forEach(function(s){s.classList.remove('drag-over');}); });
    div.addEventListener('dragover', function(e){ e.preventDefault(); div.classList.add('drag-over'); });
    div.addEventListener('dragleave', function(){ div.classList.remove('drag-over'); });
    div.addEventListener('drop', function(e){
      e.preventDefault(); div.classList.remove('drag-over');
      if(!sbDragId || sbDragId===sec.id) return;
      var allEls = document.querySelectorAll('#sb-container .sb-section');
      var allIds = Array.from(allEls).map(function(el){return el.id.replace('sbsec-','');});
      var fromIdx = allIds.indexOf(sbDragId);
      var toIdx = allIds.indexOf(sec.id);
      allIds.splice(fromIdx,1); allIds.splice(toIdx,0,sbDragId);
      sidebarOrder = allIds; saveSbOrder(); buildSidebar();
    });
    container.appendChild(div);
  });
}

function toggleSbSection(id) { var el=document.getElementById(id); if(el) el.classList.toggle('open'); }

// ═══════════════════════════════════════════
//  PAGE RENDERING
// ═══════════════════════════════════════════
function getMeta(key){ return customPages[key] || DEFAULT_META[key] || DEFAULT_META.stub; }
function getWidgets(key){ return (customPages[key] && customPages[key].widgets) ? customPages[key].widgets : getDefaultWidgets(key); }

function showPage(key) {
  currentPage = key; isEditing = false;
  document.getElementById('sidebar').classList.remove('open');
  document.getElementById('overlay').classList.remove('show');
  document.getElementById('widget-toolbar').classList.remove('visible');
  document.querySelectorAll('.sb-links a').forEach(function(a){a.classList.remove('active');});
  window.scrollTo(0,0);
  renderViewPage(key);
}

function renderViewPage(key) {
  var meta = getMeta(key);
  var widgets = getWidgets(key);
  var main = document.getElementById('main-content');
  var isStub = !customPages[key] && (key==='stub' || !DEFAULT_META[key]);
  var canvasHtml = widgets.map(function(w){return renderWidget(w,false);}).join('');

  if(key==='home') {
    main.innerHTML =
      '<div class="breadcrumb"><a onclick="showPage(\'home\')">Theria Wiki</a> <span>&#8250;</span> <span>Main Page</span></div>' +
      '<div class="page-header">' +
        '<div style="flex:1"><h1 class="page-title">'+escHtml(meta.title)+'</h1><p class="page-subtitle">'+escHtml(meta.subtitle)+'</p></div>' +
        '<div class="edit-bar"><button class="btn btn-edit" onclick="enterEdit(\'home\')">&#10002; Edit</button></div>' +
      '</div>' +
      '<div class="notice"><svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><circle cx="12" cy="12" r="10"/><line x1="12" y1="8" x2="12" y2="12"/><line x1="12" y1="16" x2="12.01" y2="16"/></svg>' +
        '<span>Click <strong>&#10002; Edit</strong> to write lore &amp; add widgets. Use the bottom toolbar in edit mode to insert new widget types. Drag the <strong>\u283f</strong> handle on any widget to reorder. Drag sidebar section headers to reorder navigation.</span></div>' +
      '<div class="page-canvas" id="canvas-home">'+canvasHtml+'</div>' +
      '<hr class="gold-divider">' +
      '<div class="cat-grid">' +
        [{icon:'\ud83d\uddfa',name:'Overview',k:'home'},{icon:'\u2694\ufe0f',name:'Factions',k:'factions'},{icon:'\ud83c\udff0',name:'Locations',k:'locations'},{icon:'\ud83e\uddec',name:'Races',k:'species'},{icon:'\ud83d\udc64',name:'Characters',k:'characters'},{icon:'\ud83d\udcdc',name:'History',k:'history'},{icon:'\ud83d\udd2c',name:'Research',k:'research'}]
          .map(function(c){return '<div class="cat-card" onclick="showPage(\''+c.k+'\')" ><div class="cat-icon">'+c.icon+'</div><div class="cat-name">'+c.name+'</div></div>';}).join('') +
      '</div>';
    return;
  }

  main.innerHTML =
    '<div class="breadcrumb"><a onclick="showPage(\'home\')">Theria Wiki</a> <span>&#8250;</span> <span>'+escHtml(meta.title)+'</span></div>' +
    '<div class="page-header">' +
      '<div style="flex:1"><h1 class="page-title">'+escHtml(meta.title)+'</h1><p class="page-subtitle">'+escHtml(meta.subtitle)+'</p></div>' +
      '<div class="edit-bar">'+(isStub?'<span class="stub-badge">stub</span>':'')+'<button class="btn btn-edit" onclick="enterEdit(\''+key+'\')">&#10002; Edit</button></div>' +
    '</div>' +
    '<hr class="divider">' +
    '<div class="page-canvas" id="canvas-'+key+'">'+canvasHtml+'</div>';
}

function enterEdit(key) {
  isEditing = true;
  var meta = getMeta(key);
  var widgets = getWidgets(key);
  var main = document.getElementById('main-content');
  var canvasHtml = widgets.map(function(w){return renderWidget(w,true);}).join('');
  if(!canvasHtml) canvasHtml = '<p style="color:var(--text-dim);font-style:italic;padding:16px 0">No widgets yet. Use the toolbar below to add your first widget.</p>';

  main.innerHTML =
    '<div class="breadcrumb"><a onclick="showPage(\''+key+'\')">&#8592; Back</a> <span>&#8250;</span> <span style="color:var(--gold-dim)">Editing</span></div>' +
    '<div class="page-header" style="margin-bottom:12px">' +
      '<div style="flex:1">' +
        '<div contenteditable="true" id="ed-title" class="editable-title" spellcheck="true">'+escHtml(meta.title)+'</div>' +
        '<div contenteditable="true" id="ed-sub" class="editable-subtitle" spellcheck="true">'+escHtml(meta.subtitle)+'</div>' +
      '</div>' +
      '<div class="edit-bar">' +
        '<button class="btn btn-save" onclick="savePageMeta(\''+key+'\')">&#10003; Save</button>' +
        '<button class="btn btn-cancel" onclick="showPage(\''+key+'\')">&#10005; Done</button>' +
        '<span class="saved-flash" id="sf">Saved!</span>' +
      '</div>' +
    '</div>' +
    '<hr class="divider" style="margin:12px 0">' +
    '<div class="page-canvas edit-mode" id="canvas-'+key+'">'+canvasHtml+'</div>';

  document.getElementById('widget-toolbar').classList.add('visible');
  setTimeout(function(){ var b=document.getElementById('ed-title'); if(b) b.focus(); },60);
}

function savePageMeta(key) {
  var t = document.getElementById('ed-title');
  var s = document.getElementById('ed-sub');
  if(!customPages[key]) customPages[key] = {widgets: getWidgets(key)};
  if(t) customPages[key].title = t.innerText.trim();
  if(s) customPages[key].subtitle = s.innerText.trim();
  savePages(); flashSave();
}

function flashSave() {
  ['sf','sf2'].forEach(function(id){ var el=document.getElementById(id); if(el){el.classList.add('show');setTimeout(function(){el.classList.remove('show');},1800);}});
}

// ═══════════════════════════════════════════
//  WIDGET RENDERING
// ═══════════════════════════════════════════
function renderWidget(w, em) {
  var chrome = em ?
    '<div class="widget-chrome">' +
      '<span class="wc-btn wc-drag" draggable="true" onmousedown="dragWidgetId=\''+w.id+'\'" title="Drag to reorder">\u283f</span>' +
      '<button class="wc-btn" onclick="openWidgetEditor(\''+w.id+'\')">Edit</button>' +
      '<button class="wc-btn" onclick="deleteWidget(\''+w.id+'\')" style="color:#d47070">&#10005;</button>' +
    '</div>' : '';

  var dragAttrs = em ?
    'draggable="true" ' +
    'onmousedown="dragWidgetId=\''+w.id+'\'" ' +
    'ondragstart="onWDragStart(event,\''+w.id+'\')" ' +
    'ondragend="onWDragEnd(event)" ' +
    'ondragover="onWDragOver(event,\''+w.id+'\')" ' +
    'ondragleave="onWDragLeave(event)" ' +
    'ondrop="onWDrop(event,\''+w.id+'\')"' : '';

  return '<div class="widget" id="widget-'+w.id+'" '+dragAttrs+'>'+chrome+renderWidgetInner(w)+'</div>';
}

function renderWidgetInner(w) {
  var d = w.data || {};
  switch(w.type) {
    case 'text':
      return '<div class="w-text content">'+(d.html||'')+'</div>';
    case 'quote':
      return '<div class="w-quote"><div class="qt">'+escHtml(d.text||'')+'</div><div class="qa">'+escHtml(d.attr||'')+'</div></div>';
    case 'callout':
      return '<div class="w-callout"><div class="ci">'+(d.icon||'\ud83d\udccc')+'</div><div><div class="ct">'+escHtml(d.title||'')+'</div><div class="cb">'+escHtml(d.body||'')+'</div></div></div>';
    case 'character':
      return '<div class="w-char"><div class="w-char-portrait"><span class="w-char-initial">'+escHtml(d.initial||'?')+'</span></div>' +
        '<div class="w-char-body"><div class="w-char-name">'+escHtml(d.name||'')+'</div><div class="w-char-role">'+escHtml(d.role||'')+'</div>' +
        '<div class="w-char-desc">'+escHtml(d.desc||'')+'</div>' +
        '<div class="w-char-tags">'+(d.tags||[]).map(function(t){return '<span class="char-tag">'+escHtml(t)+'</span>';}).join('')+'</div></div></div>';
    case 'location':
      return '<div class="w-location"><div class="w-loc-header"><span class="w-loc-icon">'+(d.icon||'\ud83d\udccd')+'</span><div><div class="w-loc-name">'+escHtml(d.name||'')+'</div><div class="w-loc-type">'+escHtml(d.type||'')+'</div></div></div>' +
        '<div class="w-loc-body"><div class="w-loc-desc">'+escHtml(d.desc||'')+'</div>' +
        '<div class="loc-stats"><div class="loc-stat"><span class="loc-stat-val">'+escHtml(d.stat1||'\u2014')+'</span><span class="loc-stat-lbl">'+escHtml(d.lbl1||'')+'</span></div>' +
        '<div class="loc-stat"><span class="loc-stat-val">'+escHtml(d.stat2||'\u2014')+'</span><span class="loc-stat-lbl">'+escHtml(d.lbl2||'')+'</span></div>' +
        '<div class="loc-stat"><span class="loc-stat-val">'+escHtml(d.stat3||'\u2014')+'</span><span class="loc-stat-lbl">'+escHtml(d.lbl3||'')+'</span></div></div></div></div>';
    case 'faction':
      return '<div class="w-faction"><div class="faction-emblem">'+(d.emblem||'\u2694\ufe0f')+'</div><div class="faction-info"><div class="faction-name">'+escHtml(d.name||'')+'</div><div class="faction-type">'+escHtml(d.type||'')+'</div><div class="faction-desc">'+escHtml(d.desc||'')+'</div></div></div>';
    case 'seasons':
      var sInfo = [{k:'spring',icon:'\ud83c\udf38',name:'Spring'},{k:'summer',icon:'\u2600\ufe0f',name:'Summer'},{k:'autumn',icon:'\ud83c\udf42',name:'Autumn'},{k:'winter',icon:'\u2744\ufe0f',name:'Winter'}];
      var scols = sInfo.map(function(s){
        var sd = d[s.k]||{temp:'\u2014',desc:''};
        var n = parseFloat(sd.temp); if(isNaN(n)) n=10;
        var h = Math.max(6,Math.min(52,((n+20)/60)*52));
        var col = n<0?'#5a9fd4':n<10?'#7ab8d4':n<20?'#8ab87a':n<28?'#c9a84c':'#d47050';
        return '<div class="season-col"><div class="season-name">'+s.name+'</div><div class="season-bar"><div class="season-bar-fill" style="height:'+h+'px;background:'+col+'"></div></div><span class="season-icon">'+s.icon+'</span><div class="season-temp">'+escHtml(sd.temp)+'</div><div class="season-desc">'+escHtml(sd.desc)+'</div></div>';
      }).join('');
      return '<div class="w-seasons"><div class="w-seasons-title">\ud83c\udf0d '+escHtml(d.location||'Climate')+'</div><div class="seasons-grid">'+scols+'</div></div>';
    case 'timeline':
      var evHtml = (d.events||[]).map(function(ev){
        return '<div class="tl-event"><div class="tl-dot'+(ev.major?' major':'')+'"></div><div class="tl-year">'+escHtml(ev.year||'')+'</div><div class="tl-event-title">'+escHtml(ev.title||'')+'</div><div class="tl-event-desc">'+escHtml(ev.desc||'')+'</div></div>';
      }).join('');
      return '<div class="w-timeline"><div class="tl-title">\ud83d\udcc5 '+escHtml(d.title||'Timeline')+'</div><div class="tl-track">'+evHtml+'</div></div>';
    case 'stats':
      var sRows = (d.stats||[]).map(function(s){
        return '<div class="stat-row"><div class="stat-label">'+escHtml(s.label)+'</div><div class="stat-track"><div class="stat-fill" style="width:'+s.val+'%"></div></div><div class="stat-val">'+s.val+'%</div></div>';
      }).join('');
      return '<div class="w-stats"><div class="stats-title">'+escHtml(d.title||'Stats')+'</div>'+sRows+'</div>';
    case 'table':
      var cols = d.cols||['Column 1','Column 2'];
      var rows = d.rows||[['','']];
      return '<div class="w-table"><table class="wiki-table"><thead><tr>'+cols.map(function(c){return '<th>'+escHtml(c)+'</th>';}).join('')+'</tr></thead><tbody>'+rows.map(function(r){return '<tr>'+r.map(function(c){return '<td>'+escHtml(c)+'</td>';}).join('')+'</tr>';}).join('')+'</tbody></table></div>';
    case 'divider':
      return '<div class="w-divider"><span class="w-divider-sym">'+(d.symbol||'\u2726')+'</span></div>';
    case 'map':
      var pins = (d.pins||[]).map(function(p){
        return '<span class="map-pin" style="left:'+p.x+'%;top:'+p.y+'%">'+(p.emoji||'\ud83d\udccd')+'</span>' +
               '<span class="map-pin-label" style="left:'+p.x+'%;top:'+p.y+'%">'+escHtml(p.label||'')+'</span>';
      }).join('');
      return '<div class="w-map"><div class="map-area">'+pins+'</div><div class="map-caption">'+escHtml(d.caption||'')+'</div></div>';
    default:
      return '<div class="w-text content"><p style="color:var(--text-dim)">Unknown widget: '+escHtml(w.type)+'</p></div>';
  }
}

// ═══════════════════════════════════════════
//  WIDGET DRAG & DROP
// ═══════════════════════════════════════════
function onWDragStart(e,wid){ dragWidgetId=wid; var el=document.getElementById('widget-'+wid); if(el)el.classList.add('dragging'); e.dataTransfer.effectAllowed='move'; }
function onWDragEnd(e){ document.querySelectorAll('.widget').forEach(function(w){w.classList.remove('dragging','drop-above','drop-below');}); dragWidgetId=null; }
function onWDragOver(e,wid){ e.preventDefault(); if(!dragWidgetId||dragWidgetId===wid) return; var el=document.getElementById('widget-'+wid); if(!el) return; document.querySelectorAll('.widget').forEach(function(w){w.classList.remove('drop-above','drop-below');}); var rect=el.getBoundingClientRect(); el.classList.add(e.clientY<rect.top+rect.height/2?'drop-above':'drop-below'); }
function onWDragLeave(e){ e.currentTarget.classList.remove('drop-above','drop-below'); }
function onWDrop(e,targetId){
  e.preventDefault();
  document.querySelectorAll('.widget').forEach(function(w){w.classList.remove('drop-above','drop-below');});
  if(!dragWidgetId||dragWidgetId===targetId) return;
  if(!customPages[currentPage]) customPages[currentPage]={title:getMeta(currentPage).title,subtitle:getMeta(currentPage).subtitle,widgets:getWidgets(currentPage)};
  var ws=customPages[currentPage].widgets;
  var fi=ws.findIndex(function(w){return w.id===dragWidgetId;});
  var ti=ws.findIndex(function(w){return w.id===targetId;});
  if(fi<0||ti<0) return;
  var moved=ws.splice(fi,1)[0];
  var el=document.getElementById('widget-'+targetId);
  var rect=el.getBoundingClientRect();
  var insertAfter=e.clientY>rect.top+rect.height/2;
  var newTi=ws.findIndex(function(w){return w.id===targetId;});
  ws.splice(insertAfter?newTi+1:newTi,0,moved);
  savePages();
  var canvas=document.getElementById('canvas-'+currentPage);
  if(canvas) canvas.innerHTML=ws.map(function(w){return renderWidget(w,true);}).join('');
}

// ═══════════════════════════════════════════
//  WIDGET CRUD
// ═══════════════════════════════════════════
function addWidget(type) {
  var defaults = {
    text:{html:'<p>Write your content here\u2026</p>'},
    quote:{text:'Enter your quote here.',attr:'Attribution'},
    callout:{icon:'\ud83d\udccc',title:'Callout Title',body:'Callout body text.'},
    character:{name:'Character Name',role:'Title or Role',desc:'A brief description.',tags:['Tag'],initial:'?'},
    location:{icon:'\ud83d\udccd',name:'Location Name',type:'Location Type',desc:'A brief description.',stat1:'\u2014',lbl1:'Stat 1',stat2:'\u2014',lbl2:'Stat 2',stat3:'\u2014',lbl3:'Stat 3'},
    faction:{emblem:'\u2694\ufe0f',name:'Faction Name',type:'Faction Type',desc:'A brief description.'},
    seasons:{location:'Region Name',spring:{temp:'10\u00b0C',desc:''},summer:{temp:'25\u00b0C',desc:''},autumn:{temp:'13\u00b0C',desc:''},winter:{temp:'0\u00b0C',desc:''}},
    timeline:{title:'Timeline',events:[{year:'Year',title:'Event',desc:'Description.',major:false}]},
    stats:{title:'Stats',stats:[{label:'Item A',val:80},{label:'Item B',val:55}]},
    table:{cols:['Column 1','Column 2','Column 3'],rows:[['','',''],['','','']]},
    divider:{symbol:'\u2726'},
    map:{caption:'Map caption',pins:[{x:30,y:40,emoji:'\ud83d\udccd',label:'Location'}]}
  };
  var id='w'+Date.now().toString(36);
  var widget={id:id,type:type,data:defaults[type]||{}};
  if(!customPages[currentPage]) customPages[currentPage]={title:getMeta(currentPage).title,subtitle:getMeta(currentPage).subtitle,widgets:getWidgets(currentPage)};
  customPages[currentPage].widgets.push(widget);
  savePages();
  var canvas=document.getElementById('canvas-'+currentPage);
  if(canvas) canvas.innerHTML=customPages[currentPage].widgets.map(function(w){return renderWidget(w,true);}).join('');
  setTimeout(function(){openWidgetEditor(id);},60);
}

function deleteWidget(wid) {
  if(!customPages[currentPage]) customPages[currentPage]={title:getMeta(currentPage).title,subtitle:getMeta(currentPage).subtitle,widgets:getWidgets(currentPage)};
  customPages[currentPage].widgets=customPages[currentPage].widgets.filter(function(w){return w.id!==wid;});
  savePages();
  var el=document.getElementById('widget-'+wid); if(el) el.remove();
}

function saveWidgetData(wid,newData) {
  if(!customPages[currentPage]) customPages[currentPage]={title:getMeta(currentPage).title,subtitle:getMeta(currentPage).subtitle,widgets:getWidgets(currentPage)};
  var ws=customPages[currentPage].widgets;
  var w=null; for(var i=0;i<ws.length;i++){if(ws[i].id===wid){w=ws[i];break;}}
  if(w){w.data=newData;savePages();}
  var updated=null; for(var i=0;i<ws.length;i++){if(ws[i].id===wid){updated=ws[i];break;}}
  if(updated){var el=document.getElementById('widget-'+wid); if(el) el.outerHTML=renderWidget(updated,true);}
  closeModal();
}

// ═══════════════════════════════════════════
//  WIDGET EDITORS
// ═══════════════════════════════════════════
function openWidgetEditor(wid) {
  var ws=customPages[currentPage]?customPages[currentPage].widgets:getDefaultWidgets(currentPage);
  var w=null; for(var i=0;i<ws.length;i++){if(ws[i].id===wid){w=ws[i];break;}}
  if(!w) return;
  var d=w.data||{};
  var body='';

  if(w.type==='text') {
    body='<div class="fmt-bar"><button class="fmt-btn" onclick="wfe(\'bold\')"><b>B</b></button><button class="fmt-btn" onclick="wfe(\'italic\')"><i>I</i></button><button class="fmt-btn" onclick="wfe(\'underline\')"><u>U</u></button><div class="fmt-sep"></div><button class="fmt-btn" onclick="wfb(\'h2\')">H2</button><button class="fmt-btn" onclick="wfb(\'h3\')">H3</button><button class="fmt-btn" onclick="wfb(\'p\')">&para;</button><div class="fmt-sep"></div><button class="fmt-btn" onclick="wfe(\'insertUnorderedList\')">&bull; list</button><button class="fmt-btn" onclick="wInsertQuote()">&ldquo; quote</button><div class="fmt-sep"></div><button class="fmt-btn" onclick="wfe(\'removeFormat\')">clear</button></div><div class="editable-content content" id="we-html" contenteditable="true" spellcheck="true" style="min-height:160px">'+(d.html||'')+'</div><p class="edit-hint">Select text and use the toolbar to format.</p>';
  } else if(w.type==='quote') {
    body='<label class="fl">Quote Text</label><textarea id="we-text" rows="3">'+escHtml(d.text||'')+'</textarea><label class="fl">Attribution</label><input type="text" id="we-attr" value="'+escHtml(d.attr||'')+'">';
  } else if(w.type==='callout') {
    body='<label class="fl">Icon (emoji)</label><input type="text" id="we-icon" value="'+escHtml(d.icon||'\ud83d\udccc')+'" style="width:70px"><label class="fl">Title</label><input type="text" id="we-title" value="'+escHtml(d.title||'')+'"><label class="fl">Body Text</label><textarea id="we-body">'+escHtml(d.body||'')+'</textarea>';
  } else if(w.type==='character') {
    body='<div class="modal-row"><div><label class="fl">Name</label><input type="text" id="we-name" value="'+escHtml(d.name||'')+'"></div><div><label class="fl">Initial/Emoji</label><input type="text" id="we-initial" value="'+escHtml(d.initial||'?')+'" style="width:70px"></div></div><label class="fl">Role / Title</label><input type="text" id="we-role" value="'+escHtml(d.role||'')+'"><label class="fl">Description</label><textarea id="we-desc">'+escHtml(d.desc||'')+'</textarea><label class="fl">Tags (comma-separated)</label><input type="text" id="we-tags" value="'+escHtml((d.tags||[]).join(', '))+'">';
  } else if(w.type==='location') {
    body='<div class="modal-row"><div><label class="fl">Icon (emoji)</label><input type="text" id="we-icon" value="'+escHtml(d.icon||'\ud83d\udccd')+'" style="width:70px"></div><div><label class="fl">Name</label><input type="text" id="we-name" value="'+escHtml(d.name||'')+'"></div></div><label class="fl">Type</label><input type="text" id="we-type" value="'+escHtml(d.type||'')+'"><label class="fl">Description</label><textarea id="we-desc">'+escHtml(d.desc||'')+'</textarea><label class="fl">Stat 1</label><div class="modal-row"><input type="text" id="we-s1" placeholder="Value" value="'+escHtml(d.stat1||'')+'"><input type="text" id="we-l1" placeholder="Label" value="'+escHtml(d.lbl1||'')+'"></div><label class="fl">Stat 2</label><div class="modal-row"><input type="text" id="we-s2" placeholder="Value" value="'+escHtml(d.stat2||'')+'"><input type="text" id="we-l2" placeholder="Label" value="'+escHtml(d.lbl2||'')+'"></div><label class="fl">Stat 3</label><div class="modal-row"><input type="text" id="we-s3" placeholder="Value" value="'+escHtml(d.stat3||'')+'"><input type="text" id="we-l3" placeholder="Label" value="'+escHtml(d.lbl3||'')+'"></div>';
  } else if(w.type==='faction') {
    body='<div class="modal-row"><div><label class="fl">Emblem (emoji)</label><input type="text" id="we-emblem" value="'+escHtml(d.emblem||'\u2694\ufe0f')+'" style="width:70px"></div><div><label class="fl">Name</label><input type="text" id="we-name" value="'+escHtml(d.name||'')+'"></div></div><label class="fl">Type</label><input type="text" id="we-type" value="'+escHtml(d.type||'')+'"><label class="fl">Description</label><textarea id="we-desc">'+escHtml(d.desc||'')+'</textarea>';
  } else if(w.type==='seasons') {
    var sfields=['spring','summer','autumn','winter'].map(function(s){
      var sd=d[s]||{temp:'',desc:''};
      return '<div class="season-edit-box"><div class="se-title">'+s+'</div><input type="text" id="we-'+s+'-temp" placeholder="e.g. 14\u00b0C" value="'+escHtml(sd.temp||'')+'"><input type="text" id="we-'+s+'-desc" placeholder="Short description" value="'+escHtml(sd.desc||'')+'"></div>';
    }).join('');
    body='<label class="fl">Location / Region Name</label><input type="text" id="we-loc" value="'+escHtml(d.location||'')+'"><label class="fl" style="margin-top:16px">Seasons</label><div class="season-edit-grid">'+sfields+'</div>';
  } else if(w.type==='timeline') {
    var evRows=(d.events||[]).map(function(ev,i){
      return '<div class="tl-ev-wrap"><div class="tl-ev-top"><input class="ev-yr" type="text" placeholder="Year/Era" value="'+escHtml(ev.year||'')+'"><input class="ev-ti" type="text" placeholder="Event title" value="'+escHtml(ev.title||'')+'"><button class="ev-rm" onclick="this.closest(\'.tl-ev-wrap\').remove()">&#10005;</button></div><div class="tl-ev-bot"><textarea placeholder="Description (optional)">'+escHtml(ev.desc||'')+'</textarea><label class="ev-major"><input type="checkbox" '+(ev.major?'checked':'')+'>Major event</label></div></div>';
    }).join('');
    body='<label class="fl">Title</label><input type="text" id="we-tl-title" value="'+escHtml(d.title||'Timeline')+'"><label class="fl" style="margin-top:14px">Events</label><div id="tl-ev-list" style="margin-top:6px">'+evRows+'</div><button class="add-row-btn" onclick="addTlEvRow()">+ Add Event</button>';
  } else if(w.type==='stats') {
    var statRows=(d.stats||[]).map(function(s){
      return '<div class="stat-edit-row"><input type="text" class="stat-lbl" placeholder="Label" value="'+escHtml(s.label||'')+'"><input type="range" class="stat-range" min="0" max="100" value="'+s.val+'" oninput="this.nextElementSibling.textContent=this.value+\'%\'"><span class="sv">'+s.val+'%</span><button class="stat-rm" onclick="this.closest(\'.stat-edit-row\').remove()">&#10005;</button></div>';
    }).join('');
    body='<label class="fl">Title</label><input type="text" id="we-st-title" value="'+escHtml(d.title||'Stats')+'"><label class="fl" style="margin-top:14px">Stats</label><div id="stat-list" style="margin-top:6px">'+statRows+'</div><button class="add-row-btn" onclick="addStatRow()">+ Add Stat</button>';
  } else if(w.type==='table') {
    var cols2=d.cols||['Col 1','Col 2']; var rows2=d.rows||[['','']];
    var thHtml=cols2.map(function(c,i){return '<th><input type="text" value="'+escHtml(c)+'"><button class="del-btn" onclick="rmTableCol(this)">&#10005;</button></th>';}).join('');
    var tbHtml=rows2.map(function(r){return '<tr>'+r.map(function(c){return '<td><input type="text" value="'+escHtml(c)+'"></td>';}).join('')+'<td><button class="del-btn" onclick="this.closest(\'tr\').remove()">&#10005;</button></td></tr>';}).join('');
    body='<div class="table-edit"><table><thead><tr>'+thHtml+'<th><button class="del-btn" onclick="addTableCol()">+ col</button></th></tr></thead><tbody>'+tbHtml+'</tbody></table></div><button class="add-row-btn" style="margin-top:6px" onclick="addTableRow()">+ row</button>';
  } else if(w.type==='divider') {
    body='<label class="fl">Symbol</label><input type="text" id="we-symbol" value="'+escHtml(d.symbol||'\u2726')+'" style="width:80px">';
  } else if(w.type==='map') {
    var pinRows=(d.pins||[]).map(function(p){
      return '<div class="map-pin-row"><input class="pin-emoji" type="text" placeholder="\ud83d\udccd" value="'+escHtml(p.emoji||'\ud83d\udccd')+'"><input class="pin-label" type="text" placeholder="Label" value="'+escHtml(p.label||'')+'"><input class="pin-xy" type="number" placeholder="X%" value="'+p.x+'" min="0" max="100"><input class="pin-xy" type="number" placeholder="Y%" value="'+p.y+'" min="0" max="100"><button class="stat-rm" onclick="this.closest(\'.map-pin-row\').remove()">&#10005;</button></div>';
    }).join('');
    body='<label class="fl">Caption</label><input type="text" id="we-caption" value="'+escHtml(d.caption||'')+'"><label class="fl" style="margin-top:14px">Pins</label><div id="pin-list" style="margin-top:6px">'+pinRows+'</div><button class="add-row-btn" onclick="addPinRow()">+ Add Pin</button>';
  }

  var typeName=w.type.charAt(0).toUpperCase()+w.type.slice(1);
  document.getElementById('modal-root').innerHTML=
    '<div class="modal-bg" id="modal-overlay" onclick="closeModalOnBg(event)">' +
      '<div class="modal">' +
        '<div class="modal-title">Edit Widget \u2014 '+typeName+'</div>' +
        body +
        '<div class="modal-actions"><button class="btn btn-cancel" onclick="closeModal()">Cancel</button><button class="btn btn-save" onclick="collectAndSave(\''+wid+'\',\''+w.type+'\')">&#10003; Apply</button></div>' +
      '</div>' +
    '</div>';
}

function collectAndSave(wid,type) {
  function gv(id){var el=document.getElementById(id);return el?el.value||el.innerText:'';}
  var data={};
  if(type==='text'){data={html:document.getElementById('we-html')?document.getElementById('we-html').innerHTML:''};}
  else if(type==='quote'){data={text:gv('we-text'),attr:gv('we-attr')};}
  else if(type==='callout'){data={icon:gv('we-icon'),title:gv('we-title'),body:gv('we-body')};}
  else if(type==='character'){data={name:gv('we-name'),initial:gv('we-initial'),role:gv('we-role'),desc:gv('we-desc'),tags:gv('we-tags').split(',').map(function(t){return t.trim();}).filter(Boolean)};}
  else if(type==='location'){data={icon:gv('we-icon'),name:gv('we-name'),type:gv('we-type'),desc:gv('we-desc'),stat1:gv('we-s1'),lbl1:gv('we-l1'),stat2:gv('we-s2'),lbl2:gv('we-l2'),stat3:gv('we-s3'),lbl3:gv('we-l3')};}
  else if(type==='faction'){data={emblem:gv('we-emblem'),name:gv('we-name'),type:gv('we-type'),desc:gv('we-desc')};}
  else if(type==='seasons'){
    data={location:gv('we-loc')};
    ['spring','summer','autumn','winter'].forEach(function(s){data[s]={temp:gv('we-'+s+'-temp'),desc:gv('we-'+s+'-desc')};});
  }
  else if(type==='timeline'){
    data={title:gv('we-tl-title'),events:[]};
    document.querySelectorAll('#tl-ev-list .tl-ev-wrap').forEach(function(wrap){
      var top=wrap.querySelector('.tl-ev-top'); var bot=wrap.querySelector('.tl-ev-bot');
      var yr=top?top.querySelector('.ev-yr'):''; var ti=top?top.querySelector('.ev-ti'):'';
      var ta=bot?bot.querySelector('textarea'):null; var cb=bot?bot.querySelector('input[type=checkbox]'):null;
      data.events.push({year:yr?yr.value:'',title:ti?ti.value:'',desc:ta?ta.value:'',major:cb?cb.checked:false});
    });
  }
  else if(type==='stats'){
    data={title:gv('we-st-title'),stats:[]};
    document.querySelectorAll('#stat-list .stat-edit-row').forEach(function(row){
      var lbl=row.querySelector('.stat-lbl'); var rng=row.querySelector('.stat-range');
      data.stats.push({label:lbl?lbl.value:'',val:parseInt(rng?rng.value:50)||50});
    });
  }
  else if(type==='table'){
    var hds=[]; document.querySelectorAll('.table-edit thead input[type=text]').forEach(function(i){hds.push(i.value);});
    var rws=[]; document.querySelectorAll('.table-edit tbody tr').forEach(function(tr){var r=[];tr.querySelectorAll('input[type=text]').forEach(function(i){r.push(i.value);});rws.push(r);});
    data={cols:hds,rows:rws};
  }
  else if(type==='divider'){data={symbol:gv('we-symbol')};}
  else if(type==='map'){
    data={caption:gv('we-caption'),pins:[]};
    document.querySelectorAll('#pin-list .map-pin-row').forEach(function(row){
      var ins=row.querySelectorAll('input');
      data.pins.push({emoji:ins[0]?ins[0].value:'\ud83d\udccd',label:ins[1]?ins[1].value:'',x:parseInt(ins[2]?ins[2].value:50)||50,y:parseInt(ins[3]?ins[3].value:50)||50});
    });
  }
  saveWidgetData(wid,data);
}

// Formatting helpers for text editor
function wfe(cmd){var el=document.getElementById('we-html');if(el)el.focus();document.execCommand(cmd,false,null);}
function wfb(tag){var el=document.getElementById('we-html');if(el)el.focus();document.execCommand('formatBlock',false,tag);}
function wInsertQuote(){var el=document.getElementById('we-html');if(!el)return;el.focus();var sel=window.getSelection();var txt=sel&&sel.toString()?sel.toString():'Quote text here';document.execCommand('insertHTML',false,'<blockquote>'+txt+'<cite>\u2014 Source</cite></blockquote><p><br></p>');}

// Dynamic row helpers
function addTlEvRow(){var l=document.getElementById('tl-ev-list');if(!l)return;var d=document.createElement('div');d.className='tl-ev-wrap';d.innerHTML='<div class="tl-ev-top"><input class="ev-yr" type="text" placeholder="Year/Era"><input class="ev-ti" type="text" placeholder="Event title"><button class="ev-rm" onclick="this.closest(\'.tl-ev-wrap\').remove()">&#10005;</button></div><div class="tl-ev-bot"><textarea placeholder="Description (optional)"></textarea><label class="ev-major"><input type="checkbox">Major event</label></div>';l.appendChild(d);}
function addStatRow(){var l=document.getElementById('stat-list');if(!l)return;var d=document.createElement('div');d.className='stat-edit-row';d.innerHTML='<input type="text" class="stat-lbl" placeholder="Label"><input type="range" class="stat-range" min="0" max="100" value="50" oninput="this.nextElementSibling.textContent=this.value+\'%\'"><span class="sv">50%</span><button class="stat-rm" onclick="this.closest(\'.stat-edit-row\').remove()">&#10005;</button>';l.appendChild(d);}
function addPinRow(){var l=document.getElementById('pin-list');if(!l)return;var d=document.createElement('div');d.className='map-pin-row';d.innerHTML='<input class="pin-emoji" type="text" placeholder="\ud83d\udccd" value="\ud83d\udccd"><input class="pin-label" type="text" placeholder="Label"><input class="pin-xy" type="number" placeholder="X%" value="50" min="0" max="100"><input class="pin-xy" type="number" placeholder="Y%" value="50" min="0" max="100"><button class="stat-rm" onclick="this.closest(\'.map-pin-row\').remove()">&#10005;</button>';l.appendChild(d);}
function addTableCol(){var te=document.querySelector('.table-edit table');if(!te)return;var ths=te.querySelectorAll('thead tr th');var addBtn=ths[ths.length-1];var nth=document.createElement('th');nth.innerHTML='<input type="text" value="Column"><button class="del-btn" onclick="rmTableCol(this)">&#10005;</button>';te.querySelector('thead tr').insertBefore(nth,addBtn);te.querySelectorAll('tbody tr').forEach(function(tr){var ntd=document.createElement('td');ntd.innerHTML='<input type="text">';tr.insertBefore(ntd,tr.lastElementChild);});}
function rmTableCol(btn){var td=btn.parentElement;var idx=Array.from(td.parentElement.children).indexOf(td);document.querySelector('.table-edit table').querySelectorAll('tr').forEach(function(tr){if(tr.children[idx])tr.removeChild(tr.children[idx]);});}
function addTableRow(){var tbody=document.querySelector('.table-edit tbody');if(!tbody)return;var colCount=document.querySelectorAll('.table-edit thead th').length-1;var tr=document.createElement('tr');for(var i=0;i<colCount;i++){var td=document.createElement('td');td.innerHTML='<input type="text">';tr.appendChild(td);}var del=document.createElement('td');del.innerHTML='<button class="del-btn" onclick="this.closest(\'tr\').remove()">&#10005;</button>';tr.appendChild(del);tbody.appendChild(tr);}

function closeModal(){document.getElementById('modal-root').innerHTML='';}
function closeModalOnBg(e){if(e.target.id==='modal-overlay')closeModal();}

// ═══════════════════════════════════════════
//  NEW PAGE MODAL
// ═══════════════════════════════════════════
function openNewPageModal(section) {
  var opts=SECTIONS.map(function(s){return '<option value="'+s.id+'" '+(s.id===section?'selected':'')+'>'+s.label+'</option>';}).join('');
  document.getElementById('modal-root').innerHTML=
    '<div class="modal-bg" id="modal-overlay" onclick="closeModalOnBg(event)">' +
      '<div class="modal" style="width:440px">' +
        '<div class="modal-title">Create New Page</div>' +
        '<label class="fl">Title</label><input type="text" id="np-title" placeholder="e.g. The Pale Emperor">' +
        '<label class="fl">Subtitle</label><input type="text" id="np-sub" placeholder="e.g. Last ruler of the Unified Empire">' +
        '<label class="fl">Section</label><select id="np-sec">'+opts+'</select>' +
        '<label class="fl">Opening paragraph (optional)</label><textarea id="np-body" placeholder="Brief introduction\u2026"></textarea>' +
        '<div class="modal-actions"><button class="btn btn-cancel" onclick="closeModal()">Cancel</button><button class="btn btn-save" onclick="createNewPage()">Create Page</button></div>' +
      '</div>' +
    '</div>';
  setTimeout(function(){var el=document.getElementById('np-title');if(el)el.focus();},60);
}

function createNewPage() {
  var title=(document.getElementById('np-title')||{}).value||'';
  var sub=(document.getElementById('np-sub')||{}).value||'';
  var body=(document.getElementById('np-body')||{}).value||'';
  var section=(document.getElementById('np-sec')||{}).value||'overview';
  title=title.trim(); if(!title){var el=document.getElementById('np-title');if(el)el.focus();return;}
  var key='p-'+title.toLowerCase().replace(/[^a-z0-9]+/g,'-').replace(/^-|-$/g,'')+'-'+Date.now().toString(36);
  var bodyHtml=body.trim()?'<p>'+body.trim().replace(/\n\n/g,'</p><p>').replace(/\n/g,' ')+'</p>':'<p style="color:var(--text-dim);font-style:italic">Click \u2712 Edit to start writing.</p>';
  customPages[key]={title:title,subtitle:sub||'A Theria Wiki article',widgets:[{id:'w0',type:'text',data:{html:bodyHtml}}]};
  if(!customSidebarLinks[section]) customSidebarLinks[section]=[];
  customSidebarLinks[section].push({label:title,key:key});
  savePages(); saveSidebarLinks(); buildSidebar(); closeModal(); showPage(key);
}

// ═══════════════════════════════════════════
//  SEARCH & SIDEBAR TOGGLE
// ═══════════════════════════════════════════
function toggleSidebar(){document.getElementById('sidebar').classList.toggle('open');document.getElementById('overlay').classList.toggle('show');}

function handleSearch(e) {
  if(e.key!=='Enter') return;
  var q=e.target.value.trim().toLowerCase(); e.target.value='';
  for(var key in customPages){if(customPages[key].title&&customPages[key].title.toLowerCase().indexOf(q)>=0){showPage(key);return;}}
  var m={theria:'home',welcome:'home',magic:'magic',weave:'magic',bestiary:'bestiary',creature:'bestiary',faction:'factions',conclave:'factions',location:'locations',veranthas:'locations',race:'species',species:'species',vaeren:'species',character:'characters',history:'history',sundering:'history',timeline:'history',research:'research',geography:'geography',calendar:'calendar',economy:'economy'};
  for(var k in m){if(q.indexOf(k)>=0){showPage(m[k]);return;}}
  showPage('stub');
}

// ═══════════════════════════════════════════
//  UTIL
// ═══════════════════════════════════════════
function escHtml(s){return String(s===undefined||s===null?'':s).replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;').replace(/"/g,'&quot;');}

// ═══════════════════════════════════════════
//  BOOT
// ═══════════════════════════════════════════
loadData().then(function(){
  buildSidebar();
  showPage('home');
}).catch(function(){
  buildSidebar();
  showPage('home');
});
</script>
</body>
</html>

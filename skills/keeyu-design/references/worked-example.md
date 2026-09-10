# Worked Example

> A complete, runnable build for one A4 page using every component in the
> system. It assumes nothing is available to clone: the hero, the dot grid and
> the page shell are all built from primitives here. Paste the preamble from
> `build-guide.md`, then the helpers, then this.

If the document you are building has a Figma page to clone the hero and grid
from, clone them: it is faster and guaranteed to match. Use this when there is
nothing to clone, when you are starting a new document family, or when you need
to check what a cloned node is supposed to contain.

## The hero, from primitives

One blurred brand wash inside a clipping frame, and nothing over it. The hero is
smooth: if a build puts a second child in it, that child does not belong there.

```js
const BRAND_HERO={type:"GRADIENT_LINEAR",
  gradientTransform:[[-0.701,0.009,0.764],[0.525,-0.595,0.466]],
  gradientStops:[{position:0.10,color:{r:0.847,g:0.965,b:1,a:1}},
                 {position:0.20,color:{r:0.612,g:0.875,b:0.953,a:1}},
                 {position:0.60,color:{r:0.988,g:0.882,b:0.855,a:1}},
                 {position:1.00,color:{r:1,g:0.325,b:0.192,a:1}}]};

function buildHero(parent,y){
  const h=figma.createFrame(); parent.appendChild(h);
  h.name="hero"; h.resize(1440,684); h.clipsContent=true;
  h.fills=[{type:"SOLID",color:C.paper}];

  const g=figma.createRectangle(); h.appendChild(g);
  g.name="gradient"; g.resize(1751,554); g.x=-100; g.y=130; g.opacity=0.80;
  g.fills=[BRAND_HERO];
  g.effects=[{type:"LAYER_BLUR",blurType:"PROGRESSIVE",radius:0,
              startRadius:98.8,startOffset:{x:0.5,y:0},endOffset:{x:0.5,y:1},
              visible:true}];

  h.x=-100; h.y=y;          // -329 on page 1, 1506 on every page after
  return h;
}
```

## The dot grid, from primitives

The texture itself is a component: each tile is one vector of 300 beziers, so it
is instanced, never hand-placed. If `Texture / Dot Grid Page 1240x1754` is not
in the file, create it once on the Reference page from
`Texture / Dot Grid Tile 400x300` and point at it thereafter.

```js
async function buildDotGrid(parent,W,H,texKey){
  const dg=figma.createFrame(); parent.appendChild(dg);
  dg.name="dot grid"; dg.resize(W,H); dg.fills=[]; dg.clipsContent=true;

  const fade=figma.createRectangle(); dg.appendChild(fade);
  fade.name="fade"; fade.resize(W,H); fade.x=0; fade.y=0;
  fade.fills=[{type:"GRADIENT_LINEAR",gradientTransform:[[0,1,0],[-1,0,1]],
    gradientStops:[{position:0,   color:{r:0,g:0,b:0,a:0}},
                   {position:0.35,color:{r:0,g:0,b:0,a:0.06}},
                   {position:0.70,color:{r:0,g:0,b:0,a:0.225}},
                   {position:1,   color:{r:0,g:0,b:0,a:0.5}}]}];
  fade.isMask=true; fade.maskType="ALPHA";

  const comp=await figma.importComponentByKeyAsync(texKey);
  const tex=comp.createInstance(); dg.appendChild(tex); tex.x=0; tex.y=0;

  const scrim=figma.createRectangle(); dg.appendChild(scrim);
  scrim.name="scrim"; scrim.resize(W-1,H-18); scrim.x=1; scrim.y=9;
  const P=0.9803921580314636;
  scrim.fills=[{type:"GRADIENT_LINEAR",gradientTransform:[[0,1,0],[-1,0,1]],
    gradientStops:[{position:0,color:{r:P,g:P,b:P,a:1}},
                   {position:1,color:{r:P,g:P,b:P,a:0}}]}];
  return dg;
}
```

Z-order, once both exist on the frame: clip the hero to the page and measure
coverage. Over 80 per cent, or hero at the foot, the grid goes **in front of**
the hero. Otherwise the grid goes **behind** it.

```js
const cover=(Math.min(f.height,hero.y+hero.height)-Math.max(0,hero.y))/f.height;
const gridInFront = cover>0.8 || (hero.y+hero.height/2) > f.height/2;
f.insertChild(gridInFront?1:0, dg);
f.insertChild(gridInFront?0:1, hero);
```

## The page shell

```js
function shell(pg,name,x,footerLeft,pageNo,total){
  const f=figma.createFrame(); f.name=name; f.resize(PW,PH); f.x=x; f.y=0;
  f.fills=[{type:"SOLID",color:C.paper}]; f.clipsContent=true;
  pg.appendChild(f);
  aT(f,"Geist","Regular",13,C.muted,footerLeft,M,1696,700);
  aT(f,"Geist","Regular",13,C.muted,pageNo+" / "+total,PW-M-120,1696,120,{align:"RIGHT"});
  const col=AL(f,"VERTICAL",CW,0); col.name="content"; col.x=M; col.y=154;
  return {f,col};
}
```

Place the logo instance at (89, 70) at 130 x 30. It is a placed asset, never
type, and never redrawn from primitives.

## A page that uses everything

```js
const {f,col}=shell(pg,"Example · 1",0,"Example Document",1,1);

// header: title, then a meta line only if the artefact is per customer
const head=AL(col,"VERTICAL",null,20); head.layoutSizingHorizontal="FILL";
T(head,"Roboto Serif","Light",72,C.ink,"Example Document",{lh:112,ls:-0.2});
T(head,"Geist","Regular",19,C.body,
  "Example Customer (Parent Group)   ·   Example Document: March 2026",{lh:150,ls:-0.2});

const dw=AL(col,"VERTICAL",null,0,[40,0,0,0]);
dw.layoutSizingHorizontal="FILL"; line(dw,C.rule);

// intro, 780 wide, never full content width
const intro=AL(col,"VERTICAL",780,0,[30,0,0,0]);
T(intro,"Geist","Regular",17,C.body,"One or two sentences of source prose.",{lh:140,ls:-0.2});

// section heading: 50 when it opens a document, 62 after a stat row or a table
const s1=AL(col,"VERTICAL",null,0,[50,0,0,0]); s1.layoutSizingHorizontal="FILL";
T(s1,"Roboto Serif","Light",40,C.ink,"Milestones",{ls:-0.2});

// schedule rows, with the term as a chip
const sched=AL(col,"VERTICAL",null,0,[30,0,0,0]); sched.layoutSizingHorizontal="FILL";
function schedRow(term,meaning,pair){
  const r=AL(sched,"HORIZONTAL",null,0,[18,0,18,0]);
  r.layoutSizingHorizontal="FILL"; r.counterAxisAlignItems="MIN";
  const a=AL(r,"VERTICAL",240,0);
  if(pair) chip(a,term,pair); else T(a,"Geist","Medium",15,C.strong,term,{lh:150});
  const b=AL(r,"VERTICAL",788,0); T(b,"Geist","Regular",15,C.body,meaning,{lh:150,ls:-0.2});
}
schedRow("Credentials due","Day 7 from the Scoping Session Date.",CHIP.teal);
line(sched);
schedRow("Target go-live","Day 30 from the Scoping Session Date.",CHIP.teal);

// a table in the gradient border box, with chips in the header and a status column
const s2=AL(col,"VERTICAL",null,0,[62,0,0,0]); s2.layoutSizingHorizontal="FILL";
T(s2,"Roboto Serif","Light",40,C.ink,"Guarantees by Track",{ls:-0.2});
const wrap=AL(col,"VERTICAL",null,0,[30,0,0,0]); wrap.layoutSizingHorizontal="FILL";
const tbl=AL(wrap,"VERTICAL",null,0); tbl.layoutSizingHorizontal="FILL";
const WCOL=[258,242,242,242];
function trow(cells,header){
  const r=AL(tbl,"HORIZONTAL",null,0,[14,0,14,0]);
  r.layoutSizingHorizontal="FILL"; r.counterAxisAlignItems="MIN";
  cells.forEach((txt,i)=>{
    const c0=AL(r,"VERTICAL",WCOL[i],0);
    if(!txt) return;
    if(header) chip(c0,txt,CHIP.teal);
    else if(i===0) T(c0,"Geist","Regular",15,C.soft,txt,{lh:130,ls:-0.2});
    else T(c0,"Geist","Regular",15,C.strong,txt,{lh:130,ls:-0.2});
  });
}
trow(["","Track 1: Pure M2M","Track 2: 12-Mo, Monthly","Track 3: Annual Prepaid"],true);
line(tbl);
trow(["Money-back guarantee","None","30-day","60-day"]);
line(tbl);
trow(["ROI protection","None","1 month","2 months"]);
gradientBox(tbl,WCOL);

// a tile grid where the source lists categories with values
const s3=AL(col,"VERTICAL",null,0,[62,0,0,0]); s3.layoutSizingHorizontal="FILL";
T(s3,"Roboto Serif","Light",40,C.ink,"Known Integrations",{ls:-0.2});
tileGrid(col,[
  ["Storefronts","Shopify Plus. 6 storefronts across regional brands."],
  ["ERP","NetSuite. Single instance managing all 6 storefronts."],
  ["Middleware","Celigo. Shopify to NetSuite via API."],
  ["3PLs and carriers","Bleckmann, Radial, Invenco, Mainfreight. 24 carriers."],
  ["Helpdesk","Gorgias. 20 agents, scaling to 65 at peak."],
  ["Returns","NAVA. Global coverage except NZ."]]);

// a numbered list of five or more, two columns, coral because these are problems
const s4=AL(col,"VERTICAL",null,0,[62,0,0,0]); s4.layoutSizingHorizontal="FILL";
T(s4,"Roboto Serif","Light",32,C.ink,"Pain Points",{lh:124,ls:0});
numberedTwoCol(s4,[
  "No real-time carrier visibility across 24 carriers.",
  "Royal Mail lost-in-transit exposure in the UK market.",
  "75% reactive and 25% proactive CX operations.",
  "Fragmented systems with no centralised operational view.",
  "NAVA and Gorgias disconnect on returns.",
  "Peak season scaling cost."],CHIP.coral);

// closing block: a standalone rule in a 30/30 wrapper, then the block itself
const cr=AL(col,"VERTICAL",null,0,[30,0,30,0]); cr.layoutSizingHorizontal="FILL"; line(cr);
const cb=AL(col,"VERTICAL",null,0); cb.layoutSizingHorizontal="FILL";
T(cb,"Roboto Serif","Light",34,C.ink,"In short",{lh:124});
const cw2=AL(cb,"VERTICAL",880,0,[12,0,0,0]);
T(cw2,"Geist","Regular",16,C.body,"The closing sentence, from the source.",{lh:140});
```

## Verify before you stop

Run this over every frame you built. It catches the faults that have actually
shipped in this system, and it returns numbers rather than opinions.

```js
const EM=String.fromCharCode(8212);
const S={FRAME:1,RECTANGLE:1,COMPONENT:1,INSTANCE:1};
function audit(f){
  const all=f.findAll(()=>true);
  const rules=all.filter(x=>x.name==="rule");
  const edge=[];
  for(const x of all){ if(!S[x.type])continue;
    const w=[x.strokeTopWeight,x.strokeRightWeight,x.strokeBottomWeight,x.strokeLeftWeight];
    if(w.some(v=>v===undefined))continue;
    if(!(w[0]===w[1]&&w[1]===w[2]&&w[2]===w[3])) edge.push(x.name); }
  const txt=all.filter(x=>x.type==="TEXT");
  const hero=f.children.find(c=>c.name==="hero");
  const dgN=f.children.find(c=>c.name==="dot grid");
  const col=f.children.find(c=>c.name==="content");
  return {page:f.name,
    rulesAllLines:rules.every(r=>r.type==="LINE"),
    badEdgeStrokes:edge,                         // must be empty, no exemptions
    heroChildren:hero?hero.children.length:0,    // must be 1: the wash only
    heroY:hero?Math.round(hero.y):null,          // -329 page 1, 1506 after
    dotGridChildren:dgN?dgN.children.length:0,   // must be 3: fade, texture, scrim
    logo:(f.children.find(c=>c.name==="Logo")||{}).type,   // must be INSTANCE
    contentBottom:col?Math.round(col.y+col.height):null,
    clearsFooter:col?(col.y+col.height)<1696:null,
    emDashes:txt.filter(t=>(t.characters||"").indexOf(EM)!==-1).length,
    capsMicroLabels:txt.filter(t=>{const s=(t.characters||"").trim();
      return s.length>1&&s===s.toUpperCase()&&/[A-Z]/.test(s)&&t.fontSize<13;}).length};
}
```

Everything must come back clean: `rulesAllLines` true, `badEdgeStrokes` empty,
`heroChildren` 1, `dotGridChildren` 3, `logo` INSTANCE, `clearsFooter` true,
`emDashes` 0, `capsMicroLabels` 0. `badEdgeStrokes` takes no exemptions now:
there is no legitimate single-edge stroke anywhere in the system, so any hit is
a defect. `heroChildren` above 1 means something has been laid over the wash,
and the fix is to delete it.

## Balancing pages

`contentBottom` is the tool for this. A document reads as designed when its
pages are within a few hundred pixels of each other, and as unfinished when one
page ends at 1600 and the next at 640.

Move a whole block, never part of one: take the section heading and its rows
together, set the moved heading's top padding to 0 since it now opens the page,
and give the block that follows it on the old page the 62 it inherits. Never
split a heading from its first row, and never split a graphic from its caption.

A page that still runs light after balancing is correct. White space at the foot
of a page is the system working; a graphic added to fill it is not.

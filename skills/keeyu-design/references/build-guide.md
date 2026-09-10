# Build Guide

> How to construct a Keeyu document with the Figma MCP. Load the `figma-use`
> skill first; this file assumes its rules (append before position, font loading,
> 0–1 colour range, return node IDs).

## Cadence

- One page per `use_figma` call. Never build three pages in one script.
- Screenshot after each page.
- Do not read `.height` off an auto-layout frame you are still filling; the value
  is stale. Let a single vertical auto-layout column own all stacking, and give
  each block its own top padding. Never accumulate `y` manually.

## Preamble

Paste this at the top of every build script.

```js
const PW=1240, PH=1754, M=84, CW=1072;
const HEADW=444, RESPW=514;   // comparison row columns

const C={
  white:{r:1,g:1,b:1}, ink:{r:0,g:0,b:0}, strong:{r:0.102,g:0.102,b:0.102},
  body:{r:0.302,g:0.329,b:0.329}, soft:{r:0.475,g:0.494,b:0.510},
  muted:{r:0.604,g:0.627,b:0.651}, rule:{r:0.878,g:0.878,b:0.878},
  hair:{r:0.925,g:0.925,b:0.925}, track:{r:0.937,g:0.937,b:0.937},
  cardB:{r:0.918,g:0.918,b:0.918}, well:{r:0.976,g:0.976,b:0.976},
  connector:{r:0.796,g:0.796,b:0.796},
  coral:{r:0.965,g:0.506,b:0.416}, teal:{r:0.247,g:0.655,b:0.718},
};

const CORAL_H={type:"GRADIENT_LINEAR",gradientTransform:[[1,0,0],[0,1,0]],
  gradientStops:[{position:0,color:{r:0.988,g:0.651,b:0.580,a:1}},
                 {position:1,color:{r:0.965,g:0.506,b:0.416,a:1}}]};
const TEAL_H={type:"GRADIENT_LINEAR",gradientTransform:[[1,0,0],[0,1,0]],
  gradientStops:[{position:0,color:{r:0.373,g:0.745,b:0.784,a:1}},
                 {position:1,color:{r:0.247,g:0.655,b:0.718,a:1}}]};
const CORAL_V={...CORAL_H,gradientTransform:[[0,1,0],[-1,0,1]]};
const TEAL_V ={...TEAL_H, gradientTransform:[[0,1,0],[-1,0,1]]};
const BRAND={type:"GRADIENT_LINEAR",gradientTransform:[[0.48,-0.44,0.47],[0.27,0.62,0.01]],
  gradientStops:[{position:0.10,color:{r:0.847,g:0.965,b:1,a:1}},
                 {position:0.20,color:{r:0.612,g:0.875,b:0.953,a:1}},
                 {position:0.60,color:{r:0.988,g:0.882,b:0.855,a:1}},
                 {position:0.90,color:{r:1,g:0.325,b:0.192,a:1}}]};

const coralFXh=[
  {type:"INNER_SHADOW",color:{r:1,g:1,b:1,a:0.45},offset:{x:0,y:1},radius:0,spread:0,visible:true,blendMode:"NORMAL"},
  {type:"DROP_SHADOW",color:{r:0.965,g:0.506,b:0.416,a:0.60},offset:{x:0,y:8},radius:18,spread:-6,visible:true,blendMode:"NORMAL"}];
const tealFXh=[
  {type:"INNER_SHADOW",color:{r:1,g:1,b:1,a:0.40},offset:{x:0,y:1},radius:0,spread:0,visible:true,blendMode:"NORMAL"},
  {type:"DROP_SHADOW",color:{r:0.247,g:0.655,b:0.718,a:0.55},offset:{x:0,y:10},radius:20,spread:-8,visible:true,blendMode:"NORMAL"}];
const coralFXv=[coralFXh[0],{...coralFXh[1],offset:{x:0,y:12},radius:22,spread:-8}];
const tealFXv =[tealFXh[0], {...tealFXh[1], offset:{x:0,y:10},radius:20,spread:-8}];
const cardFX=[
  {type:"DROP_SHADOW",color:{r:0,g:0,b:0,a:0.05},offset:{x:0,y:3},radius:6,spread:0,visible:true,blendMode:"NORMAL"},
  {type:"DROP_SHADOW",color:{r:0,g:0,b:0,a:0.04},offset:{x:0,y:1},radius:1,spread:0,visible:true,blendMode:"NORMAL"}];

const asFill=c=>Array.isArray(c)?c
  :((c&&c.type&&c.type.indexOf("GRADIENT")===0)?[c]:[{type:"SOLID",color:c}]);

await Promise.all([
  figma.loadFontAsync({family:"Geist",style:"Regular"}),
  figma.loadFontAsync({family:"Geist",style:"Medium"}),
  figma.loadFontAsync({family:"Roboto Serif",style:"Light"}),
]);

// vertical or horizontal auto-layout frame, hugs height
function AL(p,dir,w,gap,pad,fill,r){
  const f=figma.createFrame(); p.appendChild(f);
  f.layoutMode=dir; f.itemSpacing=gap||0;
  const q=pad||[0,0,0,0];
  f.paddingTop=q[0]; f.paddingRight=q[1]; f.paddingBottom=q[2]; f.paddingLeft=q[3];
  f.fills=fill?asFill(fill):[]; if(r!==undefined)f.cornerRadius=r;
  f.clipsContent=false;
  if(w){ f.resize(w,10); f.layoutSizingHorizontal="FIXED"; }
  f.layoutSizingVertical="HUG";
  return f;
}
// text inside an auto-layout parent
function T(p,fam,sty,size,col,chars,o){
  o=o||{}; const t=figma.createText(); p.appendChild(t);
  t.fontName={family:fam,style:sty}; t.fontSize=size; t.characters=chars;
  t.fills=[{type:"SOLID",color:col}];
  if(o.lh) t.lineHeight={unit:"PERCENT",value:o.lh};
  if(o.ls!==undefined) t.letterSpacing={unit:"PERCENT",value:o.ls};
  t.textAutoResize="HEIGHT";
  t.layoutSizingHorizontal=(o.hug?"HUG":"FILL");
  if(o.align) t.textAlignHorizontal=o.align;
  return t;
}
// absolutely positioned rect / text, for inside graphic wells
function aR(p,x,y,w,h,fill,r,fx){
  const n=figma.createRectangle(); p.appendChild(n); n.resize(w,h);
  n.fills=asFill(fill); if(r!==undefined)n.cornerRadius=r; if(fx)n.effects=fx;
  n.x=x; n.y=y; return n;
}
function aT(p,fam,sty,size,col,chars,x,y,w,o){
  o=o||{}; const t=figma.createText(); p.appendChild(t);
  t.fontName={family:fam,style:sty}; t.fontSize=size; t.characters=chars;
  t.fills=[{type:"SOLID",color:col}];
  if(o.lh) t.lineHeight={unit:"PERCENT",value:o.lh};
  if(o.ls!==undefined) t.letterSpacing={unit:"PERCENT",value:o.ls};
  if(w){ t.resize(w,t.height); t.textAutoResize="HEIGHT"; }
  if(o.align) t.textAlignHorizontal=o.align;
  t.x=x; t.y=y; return t;
}
// graphic well, fixed height, absolute children
function well(parent,h){
  const wrap=AL(parent,"VERTICAL",null,0,[20,0,0,0]);
  wrap.layoutSizingHorizontal="FILL";
  const box=figma.createFrame(); wrap.appendChild(box); box.resize(CW,h);
  box.fills=[{type:"SOLID",color:C.well}];
  box.strokes=[{type:"SOLID",color:C.hair}]; box.strokeWeight=1;
  box.cornerRadius=22; box.clipsContent=false; box.name="graphic";
  box.layoutSizingHorizontal="FILL"; box.layoutSizingVertical="FIXED";
  return box;
}
// THE ONLY way to draw a rule, divider or row separator.
// A real LINE node in the auto-layout flow. Never a rectangle, never a frame stroke.
function line(parent,col,w){
  const n=figma.createLine(); parent.appendChild(n);
  n.name="rule"; n.resize(w||CW,0);
  n.strokes=[{type:"SOLID",color:col||C.hair}];
  n.strokeWeight=1;
  n.layoutSizingHorizontal="FILL";
  return n;
}
```

## Rules and dividers

Every rule in a Keeyu document is a real `LINE` node with a 1 px stroke, filling
the width, sitting in the auto-layout flow as its own child, named `rule`.

Two things are **not** lines and must never be used as one:

1. **A frame with a stroke and three edges zeroed.** `strokeTopWeight = 1` with
   the other three at `0` is a box pretending to be a line. It cannot be
   selected, moved, recoloured or deleted without editing the container, and it
   silently changes shape when the frame's padding changes.
2. **A 1 px rectangle with a fill.** It looks identical in a screenshot and is
   wrong in the file: it has no stroke, so stroke weight, colour, dash and cap
   controls do nothing, and a designer opening the file has to delete and
   redraw it to change anything.

`figma.createLine()`, `resize(width, 0)`, a `hair` stroke, `strokeWeight = 1`,
`layoutSizingHorizontal = "FILL"`. Do not set `layoutSizingVertical` on a line.

The main header divider is the same line inside a padding-only wrapper (top
padding 40, no fill, no stroke). A wrapper that exists purely to carry padding
is fine; a wrapper faking the line itself is not.

The only frames in the entire system that carry strokes are the graphic well and
the white cards inside it, and both of those have **all four edges** on because
they are genuinely boxes. If a build script contains `strokeTopWeight`,
`strokeBottomWeight`, `strokeLeftWeight` or `strokeRightWeight` at all, it is
wrong.

## Page shell

```js
function shell(name,x,footerLeft,pageNo){
  const f=figma.createFrame(); f.name=name; f.resize(PW,PH); f.x=x; f.y=0;
  f.fills=[{type:"SOLID",color:C.white}]; f.clipsContent=true;
  figma.currentPage.appendChild(f);
  aT(f,"Geist","Regular",13,C.muted,footerLeft,M,1696,700);
  aT(f,"Geist","Regular",13,C.muted,pageNo,PW-M-120,1696,120,{align:"RIGHT"});
  return f;
}
```

Place the logo instance at (89, 70) after creating the shell. Every page gets a
`hero` clone inserted as its first child so it sits behind the content: page 1
at (-100, -329), every following page at (-100, 1506).

The same rule applies to the systems graphic: clone the approved instance rather
than rebuilding it, then retype the five card labels and the caption.

## Pain point row

```js
function cmpRow(parent,title,labelA,heard,labelB,fixed){
  // separator: a real line in a wrapper padded 30 above and 30 below
  const sep=AL(parent,"VERTICAL",null,0,[30,0,30,0]);
  sep.layoutSizingHorizontal="FILL"; line(sep);

  const row=AL(parent,"HORIZONTAL",null,0,null);
  row.layoutSizingHorizontal="FILL"; row.name="row";
  row.primaryAxisAlignItems="SPACE_BETWEEN"; row.counterAxisAlignItems="MIN";

  const h=AL(row,"VERTICAL",444,0); 
  T(h,"Roboto Serif","Light",34,C.ink,title,{lh:124,ls:-0.2});

  const right=AL(row,"VERTICAL",514,15);

  const a=AL(right,"VERTICAL",null,0); a.layoutSizingHorizontal="FILL";
  T(a,"Geist","Medium",18,C.coral,labelA,{lh:150});
  T(a,"Geist","Regular",15,C.soft,heard,{lh:130,ls:-0.2});

  line(right,null,514);

  const b=AL(right,"VERTICAL",null,0); b.layoutSizingHorizontal="FILL";
  T(b,"Geist","Medium",18,C.teal,labelB,{lh:150});
  T(b,"Geist","Regular",15,C.strong,fixed,{lh:130,ls:-0.2});

  return row;
}
```

Add a graphic by creating a vertical wrapper on the row with top padding 20 and
gap 15, putting the serif caption in it, then calling `well(...)`.

## Sweep before you finish

Two passes over every page once the build is done, before the screenshot:

1. **Glow on every page.** Page 1 carries a `hero` clone at (-100, -329). Every
   page after it carries one at (-100, 1506), inserted as the first child. Check
   the count matches the page count. Never delete one: a `hero` sitting low on a
   continuation page is the design, not a stray.
2. **Balance.** Read the content column bottom on every page. A section heading
   sitting alone at the foot of a page with its rows overleaf is the failure to
   look for. Move the heading, its intro and its first row forward together, and
   set the moved heading's top padding to 0 since it now opens the page.

## Common failures

| Symptom | Cause |
|---|---|
| Blocks stacked on top of each other at the same y | Read `.height` off an auto-layout frame before it reflowed. Use one column with per-block padding. |
| `fills failed validation … color.r missing` | Passed a gradient object where a solid colour was expected. Route every fill through `asFill`. |
| Table or card borders doubled or broken | Cells hugging instead of filling row height. Set `layoutSizingVertical="FILL"` on every cell in a row. |
| Text overflowing its container | Set a fixed width then read `.height` in the same tick. Set width, set `textAutoResize="HEIGHT"`, then position on the next statement. |
| A separator cannot be selected, or moves when the row is edited | It is a frame stroke with three edges zeroed, not a line. Replace with `line(parent)`. |
| Stat numerals collide with each other | The 695 stat row is too narrow for these numerals. Widen the wrapper to full content width. |
| A numeral wraps inside a comparison bar | The bar is too narrow. Widen the bar, do not reduce the font size. |
| Continuation pages look bare and unbranded | Missing the bottom glow. Every page after page 1 needs a `hero` clone at (-100, 1506). |
| A deck slide looks thin and half empty | Not a spacing problem. The slide carries too little. Pair it with its neighbour, get to six or eight items, give every item a label, a headline and a body line, and rule between them. |
| A void opens in the middle of a slide | Leftover height was added to the gaps between blocks. Put it into row padding, or centre the whole column, and leave the block rhythm fixed. |
| A cloned graphic has its contents stranded on the left | It was stretched to full width. Absolutely positioned children do not reflow. Keep the native 1072 and centre it. |
| Two headlines stacked with no gap, fighting each other | Stage direction promoted to a serif headline. A channel note or duration is Geist 15 direction, not a 32 serif heading. |
| Stat numerals sit off to the left of their labels | The column hugs but nothing centres it. Set `counterAxisAlignItems = "CENTER"` on the column and `textAlignHorizontal = "CENTER"` on both texts. |
| Frames land on the wrong Figma page | `figma.currentPage` is not stable between `use_figma` calls. Resolve the page by name, `await page.loadAsync()`, `await figma.setCurrentPageAsync(page)`, and append to that page object, never to `figma.currentPage`. |
| `page.children` comes back empty on a page you know has content | The page is not loaded. `await page.loadAsync()` first. |
| Graphic looks flat | Missing the inner white highlight or the coloured glow. Both are required. |
| A placed graphic bleeds past the margin, or its contents sit at the wrong scale, after you shrank it | `resize()` on a frame moves the edges and leaves absolutely positioned children where they were. Use `rescale(factor)`, then set `x`/`y`. `resize()` is only correct on a frame whose fill *is* the image. |
| An image fill shows the wrong region, or source text from the page it was cropped out of | The crop is wrong at the source, not in Figma. Fix it in place with `scaleMode = "CROP"` and an `imageTransform` that selects the region you want, keeping that region's aspect equal to the frame's so it does not distort. Do not try to re-upload: asset upload is blocked and the user drops images in manually. |
| A text node reads as centred after you resized it | `textAlignHorizontal` survives the resize. Set it explicitly to `"LEFT"` whenever you rehouse a text node into a new column. |
| Merging two slides leaves one column running to the footer and the other stopping halfway | Do not distribute the leftover. Merge along the long axis: give the taller list its own column and let the shorter block sit at the top of its own. An unequal column bottom is correct Keeyu. A gap stretched open to even them up is not. |
| Rehousing a node into another frame throws "Cannot write to node with unloaded font" | `figma.loadFontAsync` for Roboto Serif Light, Geist Regular and Geist Medium at the top of **every** `use_figma` call that touches existing text, not just calls that create it. |


---

## Chips, boxes and grids: the helpers

Paste these under the preamble. They depend on `AL`, `T`, `line`, `C`, `asFill`
and `cardFX` from it. Together with the preamble they are enough to build any of
the four components with no reference file open and no Figma document to clone
from.

```js
// The brand 4-stop on the card border transform. Used for every gradient border.
const BRAND_BORDER={type:"GRADIENT_LINEAR",
  gradientTransform:[[0.48,-0.44,0.47],[0.27,0.62,0.01]],
  gradientStops:[{position:0.10,color:{r:0.847,g:0.965,b:1,a:1}},
                 {position:0.20,color:{r:0.612,g:0.875,b:0.953,a:1}},
                 {position:0.60,color:{r:0.988,g:0.882,b:0.855,a:1}},
                 {position:1.00,color:{r:1,g:0.325,b:0.192,a:1}}]};

const rgb=(r,g,b)=>({r:r/255,g:g/255,b:b/255});
const CHIP={
  teal : {light:rgb(0x5F,0xBE,0xC8), base:rgb(0x3F,0xA7,0xB7)},
  coral: {light:rgb(0xF9,0xA8,0x98), base:rgb(0xF6,0x81,0x6A)},
  grey : {light:rgb(0xB4,0xB8,0xBD), base:rgb(0x9A,0xA0,0xA6)},
};

// A chip. `pair` is CHIP.teal / CHIP.coral / CHIP.grey.
// `fixW` forces the text box width so a column of chips matches: 9 for one
// digit, 15 for two. Omit it for a word label such as "Confirmed".
// `k` scales the whole chip; 1 for a status, 1.3 for a list numeral.
function chip(parent,label,pair,fixW,k){
  k=k||1;
  const f=figma.createFrame(); parent.appendChild(f);
  f.name="chip"; f.layoutMode="HORIZONTAL"; f.itemSpacing=0;
  f.paddingTop=4*k; f.paddingBottom=4*k; f.paddingLeft=7*k; f.paddingRight=7*k;
  f.counterAxisAlignItems="CENTER";
  f.cornerRadius=6*k; f.clipsContent=true;
  f.fills=[{type:"SOLID",color:{r:1,g:1,b:1}},
           {type:"GRADIENT_LINEAR",gradientTransform:[[1,0,0],[0,1,0]],
            gradientStops:[{position:0,color:Object.assign({},pair.light,{a:1})},
                           {position:1,color:Object.assign({},pair.base ,{a:1})}]}];
  f.effects=[{type:"DROP_SHADOW",color:Object.assign({},pair.base,{a:0.55}),
              offset:{x:0,y:10*k},radius:20*k,spread:-8*k,
              visible:true,blendMode:"NORMAL"}];
  const t=figma.createText(); f.appendChild(t);
  t.fontName={family:"Geist",style:"Medium"}; t.fontSize=11*k;
  t.characters=label;
  t.fills=[{type:"SOLID",color:{r:1,g:1,b:1}}];
  t.lineHeight={unit:"PERCENT",value:130};
  t.letterSpacing={unit:"PERCENT",value:-0.2};
  t.textAutoResize="HEIGHT";
  if(fixW){ t.layoutSizingHorizontal="FIXED"; t.resize(fixW*k,t.height);
            t.textAlignHorizontal="CENTER"; }
  else    { t.textAutoResize="WIDTH_AND_HEIGHT"; t.layoutSizingHorizontal="HUG"; }
  f.layoutSizingHorizontal="HUG"; f.layoutSizingVertical="HUG";
  return f;
}

// Turn a table frame into the gradient border box. Call it AFTER the rows are
// in, then renarrow the columns with colWidths.
function gradientBox(tbl,colWidths){
  tbl.paddingTop=28; tbl.paddingBottom=28; tbl.paddingLeft=44; tbl.paddingRight=44;
  tbl.strokes=[BRAND_BORDER]; tbl.strokeWeight=1; tbl.cornerRadius=22;
  tbl.fills=[]; tbl.layoutSizingHorizontal="FILL";
  if(colWidths) for(const r of tbl.children){
    if(r.type!=="FRAME") continue;
    r.children.forEach((c,i)=>{ if(c.type==="FRAME"&&colWidths[i]){
      c.resize(colWidths[i],c.height); c.layoutSizingHorizontal="FIXED"; }});
  }
  return tbl;
}

// Tile grid. `items` is [[label, detail], ...]; three to a row.
function tileGrid(parent,items,perRow){
  perRow=perRow||3;
  const wrap=AL(parent,"VERTICAL",null,0,[20,0,0,0]);
  wrap.layoutSizingHorizontal="FILL";
  const box=figma.createFrame(); wrap.appendChild(box);
  box.name="graphic"; box.layoutMode="VERTICAL"; box.itemSpacing=24;
  box.paddingTop=28; box.paddingBottom=28; box.paddingLeft=44; box.paddingRight=44;
  box.fills=[{type:"SOLID",color:C.well}];
  box.strokes=[{type:"SOLID",color:C.hair}]; box.strokeWeight=1;
  box.cornerRadius=22; box.clipsContent=false;
  box.layoutSizingHorizontal="FILL"; box.layoutSizingVertical="HUG";
  const tiles=[];
  for(let r=0;r*perRow<items.length;r++){
    const row=figma.createFrame(); box.appendChild(row);
    row.name="row"; row.layoutMode="HORIZONTAL"; row.itemSpacing=24;
    row.paddingTop=0;row.paddingRight=0;row.paddingBottom=0;row.paddingLeft=0;
    row.fills=[]; row.clipsContent=false;
    row.layoutSizingHorizontal="FILL"; row.layoutSizingVertical="HUG";
    row.counterAxisAlignItems="MIN";
    for(let k=0;k<perRow;k++){
      const it=items[r*perRow+k]; if(!it) break;
      const tile=figma.createFrame(); row.appendChild(tile);
      tile.name="tile"; tile.layoutMode="VERTICAL"; tile.itemSpacing=6;
      tile.paddingTop=22;tile.paddingBottom=22;tile.paddingLeft=22;tile.paddingRight=22;
      tile.fills=[{type:"SOLID",color:{r:1,g:1,b:1}}];
      tile.strokes=[BRAND_BORDER]; tile.strokeWeight=1;
      tile.cornerRadius=12; tile.effects=cardFX; tile.clipsContent=false;
      tile.layoutSizingHorizontal="FILL";
      T(tile,"Geist","Medium",16,C.strong,it[0]);
      T(tile,"Geist","Regular",14,C.soft,it[1],{lh:140});
      tiles.push(tile);
    }
  }
  // equal heights per row: hug the row, fill the tiles
  for(const t of tiles) t.layoutSizingVertical="FILL";
  return box;
}

// Two-column numbered list. `items` is an array of body strings; the numeral is
// the 1-based index. `pair` is CHIP.coral for problems, CHIP.teal otherwise.
function numberedTwoCol(parent,items,pair){
  const wrap=figma.createFrame(); parent.appendChild(wrap);
  wrap.name="items"; wrap.layoutMode="HORIZONTAL"; wrap.itemSpacing=45;
  wrap.paddingTop=25; wrap.paddingRight=0; wrap.paddingBottom=0; wrap.paddingLeft=0;
  wrap.fills=[]; wrap.clipsContent=false;
  wrap.counterAxisAlignItems="MIN";
  wrap.layoutSizingHorizontal="HUG"; wrap.layoutSizingVertical="HUG";
  const half=Math.ceil(items.length/2), cols=[];
  for(let i=0;i<2;i++){
    const cf=figma.createFrame(); wrap.appendChild(cf);
    cf.layoutMode="VERTICAL"; cf.itemSpacing=22;
    cf.paddingTop=12; cf.paddingRight=0; cf.paddingBottom=0; cf.paddingLeft=0;
    cf.fills=[]; cf.clipsContent=false;
    cf.resize(450,10); cf.layoutSizingHorizontal="FIXED";
    cf.layoutSizingVertical="HUG"; cf.counterAxisAlignItems="MIN";
    cols.push(cf);
  }
  items.forEach((body,i)=>{
    const row=figma.createFrame(); cols[i<half?0:1].appendChild(row);
    row.layoutMode="HORIZONTAL"; row.itemSpacing=19;
    row.paddingTop=0;row.paddingRight=0;row.paddingBottom=0;row.paddingLeft=0;
    row.fills=[]; row.clipsContent=false;
    row.layoutSizingHorizontal="FILL"; row.layoutSizingVertical="HUG";
    row.counterAxisAlignItems="MIN";
    const holder=figma.createFrame(); row.appendChild(holder);
    holder.name="num"; holder.layoutMode="VERTICAL"; holder.itemSpacing=0;
    holder.paddingTop=0;holder.paddingRight=0;holder.paddingBottom=0;holder.paddingLeft=0;
    holder.fills=[]; holder.clipsContent=false;
    holder.layoutSizingHorizontal="HUG"; holder.layoutSizingVertical="HUG";
    holder.counterAxisAlignItems="MIN";
    chip(holder,String(i+1),pair,9,1.3);
    T(row,"Geist","Regular",15,C.body,body,{lh:150,ls:-0.2});
  });
  return wrap;
}
```

### Where each one goes

| Source shape | Component |
|---|---|
| A status per row | `chip` in a `MAX`-aligned cell |
| Parallel options as table headers | `chip` per header cell |
| A milestone term in a schedule row | `chip` in the term column |
| Any table | `gradientBox(tbl, widths)` |
| Categories each with a value | `tileGrid` |
| A numbered list of five or more | `numberedTwoCol` |

### Failures these introduce

| Symptom | Cause |
|---|---|
| Chips in a column have ragged right edges | Geist has no tabular figures. Pass `fixW` 9 or 15 to `chip`. |
| A 1.3x chip looks like it is peeling off the page | The shadow was not scaled with it. `chip` handles this; do not scale by hand. |
| Table text collides with its gradient border | Columns were not renarrowed. Pass `colWidths` summing to `CW - 88`. |
| Tiles in a row are different heights | The tiles were left hugging. Set every tile `layoutSizingVertical="FILL"`. |
| A tile grid stretches its contents to the left | It was built with absolute x and y. Build it in auto-layout. |
| The numbered list runs one long column | `numberedTwoCol` was not used, or was used on a list of four. |
| The gap between numeral and text looks huge | A fixed-width holder was left at 44 after the numeral became a chip. Hug the holder. |

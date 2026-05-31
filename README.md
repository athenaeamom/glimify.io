[index (3).html](https://github.com/user-attachments/files/28442919/index.3.html)

<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width,initial-scale=1.0"/>
<meta name="description" content="Glimify — Free Content Calendar, Font Studio and Creator Tools"/>
<title>Glimify ✦ Content OS</title>
<link rel="icon" href="data:image/svg+xml,<svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 100 100'><text y='.9em' font-size='90'>✦</text></svg>"/>
<script src="https://unpkg.com/react@18/umd/react.production.min.js"></script>
<script src="https://unpkg.com/react-dom@18/umd/react-dom.production.min.js"></script>
<script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/@supabase/supabase-js@2/dist/umd/supabase.min.js"></script>
<style>
*,*::before,*::after{box-sizing:border-box;margin:0;padding:0}
html,body{background:#0A0A0A;color:#fff;min-height:100vh}
#root{min-height:100vh}
::-webkit-scrollbar{width:4px;height:4px}
::-webkit-scrollbar-track{background:transparent}
::-webkit-scrollbar-thumb{background:#2a2a2a;border-radius:10px}
</style>
</head>
<body>
<div id="root"></div>
<script type="text/babel" data-presets="react">
const {useState,useEffect,useRef,useCallback}=React;
const {createClient}=supabase;



/* ─── BRAND ─────────────────────────────────────────── */
const B = {
  pink:"#FF3EA5", lime:"#D9FB60", black:"#000000",
  bg:"#0A0A0A", surface:"#111111", surface2:"#171717", surface3:"#1e1e1e",
  border:"#1e1e1e", border2:"#2a2a2a", text:"#FFFFFF",
  muted:"#666", green:"#34D399", blue:"#60A5FA",
  purple:"#A78BFA", orange:"#F97316", yellow:"#F59E0B", red:"#EF4444",
};

/* ─── RESPONSIVE ─────────────────────────────────────── */
function useBreakpoint() {
  const [w, setW] = useState(typeof window !== "undefined" ? window.innerWidth : 800);
  useEffect(() => {
    const h = () => setW(window.innerWidth);
    window.addEventListener("resize", h);
    return () => window.removeEventListener("resize", h);
  }, []);
  return { isMobile: w < 640, isTablet: w >= 640 && w < 1024, isDesktop: w >= 1024, w };
}

/* ─── CONSTANTS ──────────────────────────────────────── */
const PLATFORMS   = ["Instagram","Reels","Carousel","Threads","Facebook","YouTube","TikTok","Stories"];
const PILLARS     = ["Education","Inspiration","Entertainment","Promotion","Behind-the-Scenes","Community","Trending","Personal"];
const FORMATS     = {Instagram:"Static",Reels:"Video",Carousel:"Slides",Threads:"Thread",Facebook:"Post",YouTube:"Long-form",TikTok:"Short Video",Stories:"Story"};
const P_ICON      = {Instagram:"📸",Reels:"🎬",Carousel:"🎠",Threads:"🧵",Facebook:"📘",YouTube:"▶️",TikTok:"🎵",Stories:"⭕"};
const P_COLOR     = {Education:B.blue,Inspiration:B.lime,Entertainment:B.pink,Promotion:B.orange,"Behind-the-Scenes":B.purple,Community:B.green,Trending:B.yellow,Personal:"#E8499A"};
const TIMES       = ["6:00 AM","7:00 AM","8:00 AM","9:00 AM","12:00 PM","3:00 PM","6:00 PM","7:00 PM","8:00 PM","9:00 PM"];
const MONTH_NAMES = ["January","February","March","April","May","June","July","August","September","October","November","December"];
const DAY_NAMES   = ["Sun","Mon","Tue","Wed","Thu","Fri","Sat"];
const STATUS_CFG  = {
  published: {c:B.lime,  label:"● Live"},
  scheduled: {c:B.blue,  label:"◷ Sched"},
  draft:     {c:B.muted, label:"◌ Draft"},
};

const HOOKS = [
  "Nobody talks about this but…",
  "Here's what took me 3 years to learn:",
  "Stop doing this if you want results:",
  "The truth about [topic] that no one tells you:",
  "This changed everything for me:",
  "If I started over, I'd do this instead:",
  "Most people get this completely wrong:",
  "I tested this for 30 days — here's what happened:",
  "The one thing separating beginners from experts:",
  "This worked better than I expected:",
  "Nobody prepared me for this:",
  "The mistake I see every creator make:",
  "What they don't tell you about [topic]:",
  "This single shift 10x'd my results:",
  "Here's your sign to stop [habit]:",
];

const TIPS_2026 = {
  Instagram:["Carousels with 7–10 slides get 3× more reach than single posts","Keyword-first captions boost search discoverability","Post 7–9am or 6–8pm local time","Collab posts with micro-influencers outperform boosted posts","Stories with polls every 3 days keeps retention high"],
  Reels:["Hook must land in 0.3s — text overlay on frame 1","Trending audio used within 48hrs gets algorithm push","Loop trick: end = beginning for replay boost","Add 3 niche hashtags + 1 broad, nothing more","Original audio is being prioritized in 2026"],
  Carousel:["First slide = scroll-stopper, last slide = strong CTA","'Swipe to see the twist' hooks perform 40% better","Teach something in 5 slides or less","Consistent brand colours across all slides","Save-worthy educational carousels dominate reach"],
  Threads:["Conversational, lowercase tone outperforms polished copy","Ask a question in every thread — replies = reach","Controversial (but safe) takes go viral fast","Series threads build followers quickly","Engage with replies within first 30 mins"],
  Facebook:["Long-form personal stories dominate organic reach","Facebook Groups posts get 5× more engagement","Video posts autoplay = higher watch time metric","Nostalgia content performs well for 30–45 demo","'Comment your answer' CTAs boost visibility"],
  YouTube:["Thumbnail + Title decides 90% of CTR — test both","First 30s must re-sell the promise of the title","Chapter markers improve watch time significantly","Shorts feeding into long-form is the #1 growth strategy","Post every 2 weeks consistently over sporadic"],
  TikTok:["Native text overlays signal original content","Duets and stitches of trending content = fast reach","Post 3×/day during first 30 days for growth","POV format has the highest share rate in 2026","Keep videos under 45s for max completion rate"],
  Stories:["Polls and questions every other day for engagement","Use 'tap to reveal' trick for high interaction","Behind-the-scenes daily stories build connection","Story highlights as a free media kit for prospects","Link stickers in stories = highest swipe-up rates"],
};

const CONTENT_IDEAS = [
  {idea:"5 things I wish I knew before becoming an EA",          platform:"Carousel",  pillar:"Education",       format:"Slides"},
  {idea:"A day in my life as an Executive Assistant",            platform:"Reels",     pillar:"Behind-the-Scenes",format:"Video"},
  {idea:"The email template that saves me 2 hours daily",        platform:"Instagram", pillar:"Education",       format:"Static"},
  {idea:"Unpopular opinion: busy ≠ productive for EAs",         platform:"Threads",   pillar:"Inspiration",     format:"Thread"},
  {idea:"How I managed 3 executives at once",                    platform:"YouTube",   pillar:"Education",       format:"Long-form"},
  {idea:"Tools every EA should have in 2026",                    platform:"Carousel",  pillar:"Promotion",       format:"Slides"},
  {idea:"When your boss asks you to do the impossible…",         platform:"TikTok",    pillar:"Entertainment",   format:"Short Video"},
  {idea:"My exact morning routine as a C-suite EA",              platform:"Reels",     pillar:"Personal",        format:"Video"},
  {idea:"The one skill that got me promoted twice",              platform:"Instagram", pillar:"Inspiration",     format:"Static"},
  {idea:"How to set boundaries without losing your job",         platform:"Threads",   pillar:"Education",       format:"Thread"},
  {idea:"Behind the scenes: planning a board meeting",           platform:"Stories",   pillar:"Behind-the-Scenes",format:"Story"},
  {idea:"What no EA training prepares you for",                  platform:"Carousel",  pillar:"Education",       format:"Slides"},
  {idea:"EA salary negotiation — what actually works",           platform:"YouTube",   pillar:"Promotion",       format:"Long-form"},
  {idea:"3 calendar mistakes costing your executive time",       platform:"Reels",     pillar:"Education",       format:"Video"},
  {idea:"The most underrated EA skill nobody talks about",       platform:"Threads",   pillar:"Trending",        format:"Thread"},
];

/* ─── FONT DATA — ALL 245 FONTS FROM GLIMIFY FONT GENERATOR ── */
const FONT_CATS = ["All","Blog Serifs","Logo Fonts","Elegant Pairings","Elegant Canva","Modern Display","Modern Ligature","Branding Serif","Old Money","Luxury Canva","Minimalist Brands","Contemporary Script","Creative Fabrica","Best Free Fonts","Vintage & Retro","Romantic & Girly","Playful & Creative","Elegant Serif","Elegant Script"];
const FONT_DATA = [
  /* ── Blog Serifs ── */
  {n:"Austin (Aire Pro)",f:"'Cormorant Garamond',serif",w:"300",s:"normal",cat:"Blog Serifs"},
  {n:"Barcelona (Butler)",f:"'Libre Baskerville',serif",w:"700",s:"normal",cat:"Blog Serifs"},
  {n:"Chicago (Garamond)",f:"'EB Garamond',serif",w:"700",s:"normal",cat:"Blog Serifs"},
  {n:"Dallas (Crimson Text)",f:"'Crimson Text',serif",w:"400",s:"normal",cat:"Blog Serifs"},
  {n:"Istanbul (Lora)",f:"'Lora',serif",w:"400",s:"normal",cat:"Blog Serifs"},
  {n:"Los Angeles (Lusitana)",f:"'Lusitana',serif",w:"400",s:"normal",cat:"Blog Serifs"},
  {n:"Milan (Mirador)",f:"'Abril Fatface',serif",w:"400",s:"normal",cat:"Blog Serifs"},
  {n:"New York City (Narziss)",f:"'Bellota',cursive",w:"400",s:"italic",cat:"Blog Serifs"},
  {n:"Philadelphia (Playfair)",f:"'Playfair Display',serif",w:"400",s:"normal",cat:"Blog Serifs"},
  {n:"Rome (Roboto Slab)",f:"'Roboto Slab',serif",w:"300",s:"normal",cat:"Blog Serifs"},
  {n:"San Francisco (Silk Serif)",f:"'Source Serif 4',serif",w:"300",s:"normal",cat:"Blog Serifs"},
  {n:"Tokyo (Zilla Slab)",f:"'Zilla Slab',serif",w:"400",s:"normal",cat:"Blog Serifs"},
  /* ── Logo Fonts ── */
  {n:"Black Mango",f:"'DM Serif Display',serif",w:"400",s:"normal",cat:"Logo Fonts"},
  {n:"August Script",f:"'Euphoria Script',cursive",w:"400",s:"normal",cat:"Logo Fonts"},
  {n:"Abigail",f:"'Cormorant Garamond',serif",w:"300",s:"normal",cat:"Logo Fonts"},
  {n:"Ivy Presto Display",f:"'Playfair Display',serif",w:"400",s:"italic",cat:"Logo Fonts"},
  {n:"Coast",f:"'Josefin Sans',sans-serif",w:"700",s:"normal",cat:"Logo Fonts"},
  {n:"Rinstonia Script",f:"'Mrs Saint Delafield',cursive",w:"400",s:"normal",cat:"Logo Fonts"},
  {n:"Botanica",f:"'Cinzel',serif",w:"400",s:"normal",cat:"Logo Fonts"},
  {n:"Adrianna",f:"'Josefin Sans',sans-serif",w:"300",s:"normal",cat:"Logo Fonts"},
  {n:"Goldenbook",f:"'EB Garamond',serif",w:"400",s:"italic",cat:"Logo Fonts"},
  /* ── Elegant Pairings ── */
  {n:"L'Argentine (Christo)",f:"'Cormorant Garamond',serif",w:"300",s:"normal",cat:"Elegant Pairings"},
  {n:"Florentino (Harietta)",f:"'DM Serif Display',serif",w:"400",s:"normal",cat:"Elegant Pairings"},
  {n:"Carlo Monaco (Muse)",f:"'Cinzel',serif",w:"700",s:"normal",cat:"Elegant Pairings"},
  {n:"Muse (Preston)",f:"'Josefin Sans',sans-serif",w:"300",s:"normal",cat:"Elegant Pairings"},
  {n:"Clio (Constantine)",f:"'Cormorant Garamond',serif",w:"400",s:"italic",cat:"Elegant Pairings"},
  {n:"Harietta (Florentino)",f:"'Playfair Display',serif",w:"400",s:"italic",cat:"Elegant Pairings"},
  {n:"Dear Ivy (Clio)",f:"'Bellota',cursive",w:"400",s:"normal",cat:"Elegant Pairings"},
  {n:"Constantine (L'Argentine)",f:"'Libre Baskerville',serif",w:"700",s:"normal",cat:"Elegant Pairings"},
  {n:"Olive & Figs (Harietta)",f:"'Cormorant Garamond',serif",w:"700",s:"italic",cat:"Elegant Pairings"},
  /* ── Elegant Canva ── */
  {n:"Dawn (Brown Sugar)",f:"'Cinzel',serif",w:"400",s:"normal",cat:"Elegant Canva"},
  {n:"Crest (Stolen Love)",f:"'Josefin Sans',sans-serif",w:"700",s:"normal",cat:"Elegant Canva"},
  {n:"Misty (Black Mango)",f:"'DM Serif Display',serif",w:"400",s:"normal",cat:"Elegant Canva"},
  {n:"Serene (Black Gold)",f:"'Cormorant Garamond',serif",w:"300",s:"normal",cat:"Elegant Canva"},
  {n:"Cloudy (Tan Pearl)",f:"'Playfair Display',serif",w:"400",s:"italic",cat:"Elegant Canva"},
  {n:"Wind (Higuen Elegant)",f:"'Bodoni Moda',serif",w:"400",s:"normal",cat:"Elegant Canva"},
  {n:"Dreamy (Tan Mon Cheri)",f:"'Libre Baskerville',serif",w:"400",s:"italic",cat:"Elegant Canva"},
  {n:"Pearl (Ansam)",f:"'Cinzel',serif",w:"700",s:"normal",cat:"Elegant Canva"},
  {n:"Vogue (Catchy Mager)",f:"'Cinzel',serif",w:"400",s:"normal",cat:"Elegant Canva"},
  {n:"Coco (Hatton)",f:"'Cormorant Garamond',serif",w:"700",s:"normal",cat:"Elegant Canva"},
  {n:"Business (Atteron)",f:"'Josefin Sans',sans-serif",w:"700",s:"normal",cat:"Elegant Canva"},
  {n:"Luxury (Cinzel Decorative)",f:"'Cinzel Decorative',serif",w:"700",s:"normal",cat:"Elegant Canva"},
  {n:"York (Ansam)",f:"'Zilla Slab',serif",w:"700",s:"normal",cat:"Elegant Canva"},
  {n:"Feminine (Lovely May)",f:"'Josefin Sans',sans-serif",w:"300",s:"normal",cat:"Elegant Canva"},
  {n:"Dream (Black Mango)",f:"'Playfair Display',serif",w:"400",s:"normal",cat:"Elegant Canva"},
  /* ── Modern Display ── */
  {n:"Manhattan (De Valencia)",f:"'Cinzel',serif",w:"400",s:"normal",cat:"Modern Display"},
  {n:"Hong Kong (Onyx)",f:"'Bodoni Moda',serif",w:"700",s:"normal",cat:"Modern Display"},
  {n:"Vienna (Text Me One)",f:"'Cormorant Garamond',serif",w:"300",s:"normal",cat:"Modern Display"},
  {n:"Los Angeles (Parley Bold)",f:"'Josefin Sans',sans-serif",w:"700",s:"normal",cat:"Modern Display"},
  {n:"Budapest (Modern No.20)",f:"'Libre Baskerville',serif",w:"700",s:"normal",cat:"Modern Display"},
  {n:"Barcelona (Californian FB)",f:"'Cardo',serif",w:"400",s:"normal",cat:"Modern Display"},
  {n:"London (Avenir Next)",f:"'Lato',sans-serif",w:"300",s:"normal",cat:"Modern Display"},
  {n:"Frosted Tulip (Playfair)",f:"'Playfair Display',serif",w:"400",s:"normal",cat:"Modern Display"},
  {n:"Paris (Ostrich Sans)",f:"'Raleway',sans-serif",w:"300",s:"normal",cat:"Modern Display"},
  {n:"Tokyo (Baron Neue)",f:"'Fjalla One',sans-serif",w:"400",s:"normal",cat:"Modern Display"},
  {n:"Montreal (Winter Sans)",f:"'Oswald',sans-serif",w:"300",s:"normal",cat:"Modern Display"},
  {n:"Chicago (Cinzel)",f:"'Cinzel',serif",w:"700",s:"normal",cat:"Modern Display"},
  {n:"Bangkok (New York)",f:"'Merriweather',serif",w:"700",s:"normal",cat:"Modern Display"},
  {n:"Seoul (High Tide)",f:"'Josefin Slab',serif",w:"700",s:"normal",cat:"Modern Display"},
  {n:"Berlin (Goudy Old Style)",f:"'Goudy Bookletter 1911',serif",w:"400",s:"normal",cat:"Modern Display"},
  {n:"Milan (Museo Slab)",f:"'Rokkitt',serif",w:"400",s:"normal",cat:"Modern Display"},
  {n:"Sydney (Klavika)",f:"'Open Sans',sans-serif",w:"300",s:"normal",cat:"Modern Display"},
  {n:"Casablanca (Perpetua)",f:"'IM Fell English',serif",w:"400",s:"normal",cat:"Modern Display"},
  /* ── Modern Ligature ── */
  {n:"Gimolla (Modern Ligature)",f:"'Cormorant Garamond',serif",w:"300",s:"normal",cat:"Modern Ligature"},
  {n:"Gimola Uppercase",f:"'Cinzel',serif",w:"400",s:"normal",cat:"Modern Ligature"},
  {n:"Gaxob Display",f:"'GFS Didot',serif",w:"400",s:"normal",cat:"Modern Ligature"},
  {n:"Ligature Thin Serif",f:"'DM Serif Display',serif",w:"400",s:"normal",cat:"Modern Ligature"},
  {n:"Ligature Script Oval",f:"'Libre Caslon Display',serif",w:"400",s:"normal",cat:"Modern Ligature"},
  /* ── Branding Serif ── */
  {n:"Riyadh (Romile)",f:"'Cinzel',serif",w:"400",s:"normal",cat:"Branding Serif"},
  {n:"Havana (Stainger)",f:"'Libre Baskerville',serif",w:"700",s:"normal",cat:"Branding Serif"},
  {n:"Auckland (Valiety)",f:"'Cormorant Garamond',serif",w:"700",s:"normal",cat:"Branding Serif"},
  {n:"Sydney (Westlake)",f:"'Abril Fatface',serif",w:"400",s:"normal",cat:"Branding Serif"},
  {n:"Shanghai (White Space)",f:"'Playfair Display',serif",w:"700",s:"normal",cat:"Branding Serif"},
  {n:"Mumbai (Konfista)",f:"'EB Garamond',serif",w:"400",s:"italic",cat:"Branding Serif"},
  {n:"Budapest (Miracle World)",f:"'DM Serif Display',serif",w:"400",s:"normal",cat:"Branding Serif"},
  {n:"Zürich (Miftah)",f:"'Alfa Slab One',serif",w:"400",s:"normal",cat:"Branding Serif"},
  {n:"Palermo (Goldbugs)",f:"'Bitter',serif",w:"400",s:"italic",cat:"Branding Serif"},
  /* ── Old Money ── */
  {n:"Old Money Script",f:"'Great Vibes',cursive",w:"400",s:"normal",cat:"Old Money"},
  {n:"Old Money Bold Serif",f:"'Bodoni Moda',serif",w:"700",s:"normal",cat:"Old Money"},
  {n:"The Seasons (Luxury)",f:"'Cormorant Garamond',serif",w:"400",s:"italic",cat:"Old Money"},
  {n:"Bodoni FLF / Didact Gothic",f:"'Didact Gothic',sans-serif",w:"400",s:"normal",cat:"Old Money"},
  {n:"Sloop Script / Montserrat",f:"'Montserrat',sans-serif",w:"400",s:"normal",cat:"Old Money"},
  {n:"Playfair Display SC",f:"'Playfair Display SC',serif",w:"400",s:"normal",cat:"Old Money"},
  {n:"Times New Roman Formal",f:"'IM Fell English',serif",w:"400",s:"normal",cat:"Old Money"},
  {n:"Symphony Script",f:"'Allura',cursive",w:"400",s:"normal",cat:"Old Money"},
  {n:"Perandory Display",f:"'Abril Fatface',serif",w:"400",s:"normal",cat:"Old Money"},
  {n:"Birague Script",f:"'Sacramento',cursive",w:"400",s:"normal",cat:"Old Money"},
  /* ── Luxury Canva ── */
  {n:"Tangerine Bold",f:"'Tangerine',cursive",w:"700",s:"normal",cat:"Luxury Canva"},
  {n:"Sloop Script / Lancelot",f:"'Lancelot',cursive",w:"400",s:"normal",cat:"Luxury Canva"},
  {n:"Tan Pearl / Quicksand",f:"'Quicksand',sans-serif",w:"400",s:"normal",cat:"Luxury Canva"},
  {n:"The Seasons / Josefin",f:"'EB Garamond',serif",w:"400",s:"italic",cat:"Luxury Canva"},
  {n:"Pinyon Script / Garamond",f:"'Pinyon Script',cursive",w:"400",s:"normal",cat:"Luxury Canva"},
  {n:"Parisienne / Ovo",f:"'Parisienne',cursive",w:"400",s:"normal",cat:"Luxury Canva"},
  {n:"Le Jour Serif / Alta",f:"'Cinzel',serif",w:"700",s:"normal",cat:"Luxury Canva"},
  {n:"Coterie / Raleway",f:"'Raleway',sans-serif",w:"700",s:"normal",cat:"Luxury Canva"},
  {n:"Dream Avenue",f:"'Dancing Script',cursive",w:"700",s:"normal",cat:"Luxury Canva"},
  {n:"Manison Condensed",f:"'Josefin Slab',serif",w:"400",s:"normal",cat:"Luxury Canva"},
  {n:"Cinzel Decorative",f:"'Cinzel Decorative',serif",w:"400",s:"normal",cat:"Luxury Canva"},
  {n:"Safira March",f:"'Josefin Sans',sans-serif",w:"400",s:"normal",cat:"Luxury Canva"},
  /* ── Minimalist Brands ── */
  {n:"Carves (Montserrat)",f:"'Montserrat',sans-serif",w:"900",s:"normal",cat:"Minimalist Brands"},
  {n:"Brand (Richy)",f:"'Cinzel',serif",w:"700",s:"normal",cat:"Minimalist Brands"},
  {n:"Ginger (Lato)",f:"'Lato',sans-serif",w:"300",s:"normal",cat:"Minimalist Brands"},
  {n:"Angle (Mojiko)",f:"'Cormorant Garamond',serif",w:"300",s:"normal",cat:"Minimalist Brands"},
  {n:"Grande (Open Sans)",f:"'Open Sans',sans-serif",w:"300",s:"normal",cat:"Minimalist Brands"},
  {n:"Raleway Light",f:"'Raleway',sans-serif",w:"200",s:"normal",cat:"Minimalist Brands"},
  {n:"Josefin Sans Light",f:"'Josefin Sans',sans-serif",w:"300",s:"normal",cat:"Minimalist Brands"},
  /* ── Contemporary Script ── */
  {n:"Allison Style Script",f:"'Alex Brush',cursive",w:"400",s:"normal",cat:"Contemporary Script"},
  {n:"Sanzia",f:"'Sacramento',cursive",w:"400",s:"normal",cat:"Contemporary Script"},
  {n:"Amoret Script",f:"'Mrs Saint Delafield',cursive",w:"400",s:"normal",cat:"Contemporary Script"},
  {n:"Southern Love",f:"'Zeyada',cursive",w:"400",s:"normal",cat:"Contemporary Script"},
  {n:"Ever Enigmatic",f:"'Meie Script',cursive",w:"400",s:"normal",cat:"Contemporary Script"},
  {n:"Stay Bright",f:"'Qwitcher Grypen',cursive",w:"400",s:"normal",cat:"Contemporary Script"},
  {n:"Jack and Rose",f:"'La Belle Aurore',cursive",w:"400",s:"normal",cat:"Contemporary Script"},
  {n:"Stay Classy Script",f:"'Give You Glory',cursive",w:"400",s:"normal",cat:"Contemporary Script"},
  {n:"Lemon and Mint",f:"'Loved by the King',cursive",w:"400",s:"normal",cat:"Contemporary Script"},
  {n:"Silver South Script",f:"'Herr Von Muellerhoff',cursive",w:"400",s:"normal",cat:"Contemporary Script"},
  {n:"Opulent Solid",f:"'Ruthie',cursive",w:"400",s:"normal",cat:"Contemporary Script"},
  {n:"Sunydale",f:"'Dawning of a New Day',cursive",w:"400",s:"normal",cat:"Contemporary Script"},
  {n:"Pinot",f:"'Just Another Hand',cursive",w:"400",s:"normal",cat:"Contemporary Script"},
  {n:"The Styled Edit",f:"'Covered by Your Grace',cursive",w:"400",s:"normal",cat:"Contemporary Script"},
  /* ── Creative Fabrica ── */
  {n:"Sunflower (Glass Antiqua)",f:"'Glass Antiqua',serif",w:"400",s:"normal",cat:"Creative Fabrica"},
  {n:"Foxglove (Soria)",f:"'Cormorant Garamond',serif",w:"700",s:"normal",cat:"Creative Fabrica"},
  {n:"Poppy (Cutive Mono)",f:"'Cutive Mono',monospace",w:"400",s:"normal",cat:"Creative Fabrica"},
  {n:"Laurel (Romantic Couple)",f:"'Norican',cursive",w:"400",s:"normal",cat:"Creative Fabrica"},
  {n:"Violet (Milonga)",f:"'Milonga',serif",w:"400",s:"normal",cat:"Creative Fabrica"},
  {n:"Snowdrop (Sat. Champagne)",f:"'Cookie',cursive",w:"400",s:"normal",cat:"Creative Fabrica"},
  {n:"Daffodil (Lancelot)",f:"'Lancelot',cursive",w:"400",s:"normal",cat:"Creative Fabrica"},
  {n:"Nettle (Berkshire Swash)",f:"'Berkshire Swash',cursive",w:"400",s:"normal",cat:"Creative Fabrica"},
  {n:"Larch (CS Mulan)",f:"'Cinzel',serif",w:"700",s:"normal",cat:"Creative Fabrica"},
  {n:"Anemone (Gogoia)",f:"'Josefin Sans',sans-serif",w:"700",s:"normal",cat:"Creative Fabrica"},
  {n:"Heliotrope (Buffalo Script)",f:"'Oleo Script',cursive",w:"400",s:"normal",cat:"Creative Fabrica"},
  {n:"Hazel (Averia Serif)",f:"'Averia Serif Libre',serif",w:"400",s:"normal",cat:"Creative Fabrica"},
  {n:"Coltsfoot (Bellota)",f:"'Bellota',cursive",w:"700",s:"normal",cat:"Creative Fabrica"},
  {n:"Phlox (Tenor Sans)",f:"'Tenor Sans',sans-serif",w:"400",s:"normal",cat:"Creative Fabrica"},
  {n:"Cornflower (Alegreya)",f:"'Alegreya',serif",w:"400",s:"italic",cat:"Creative Fabrica"},
  {n:"Primrose (Ostrich Sans)",f:"'Raleway',sans-serif",w:"300",s:"normal",cat:"Creative Fabrica"},
  {n:"Snapdragon (Augusta Script)",f:"'Euphoria Script',cursive",w:"400",s:"normal",cat:"Creative Fabrica"},
  {n:"Celandine (Forum)",f:"'Forum',cursive",w:"400",s:"normal",cat:"Creative Fabrica"},
  {n:"Blue Sage (Cherry Swash)",f:"'Cherry Swash',cursive",w:"700",s:"normal",cat:"Creative Fabrica"},
  {n:"Yarrow (Alice)",f:"'Alice',serif",w:"400",s:"normal",cat:"Creative Fabrica"},
  {n:"Daisy (Spinwerad)",f:"'Fredericka the Great',serif",w:"400",s:"normal",cat:"Creative Fabrica"},
  /* ── Best Free Fonts ── */
  {n:"Camellia (Golden)",f:"'Kaushan Script',cursive",w:"400",s:"normal",cat:"Best Free Fonts"},
  {n:"Tulip (Smoothies)",f:"'Pacifico',cursive",w:"400",s:"normal",cat:"Best Free Fonts"},
  {n:"Freesia (Party Confetti)",f:"'Fjalla One',sans-serif",w:"400",s:"normal",cat:"Best Free Fonts"},
  {n:"Petunia (Delia Vinsmoke)",f:"'Courgette',cursive",w:"400",s:"normal",cat:"Best Free Fonts"},
  {n:"Rosemary (Simple Free)",f:"'Oswald',sans-serif",w:"700",s:"normal",cat:"Best Free Fonts"},
  {n:"Gardenia (Ontel)",f:"'Dancing Script',cursive",w:"700",s:"normal",cat:"Best Free Fonts"},
  {n:"Alpinia (Soria)",f:"'Cormorant Garamond',serif",w:"700",s:"normal",cat:"Best Free Fonts"},
  {n:"Orchid (Lovetle)",f:"'Josefin Sans',sans-serif",w:"400",s:"normal",cat:"Best Free Fonts"},
  {n:"Wisteria (Wonderful Future)",f:"'Libre Baskerville',serif",w:"700",s:"normal",cat:"Best Free Fonts"},
  {n:"Verbena (Casual)",f:"'Raleway',sans-serif",w:"900",s:"normal",cat:"Best Free Fonts"},
  {n:"Sunflower (Christaline)",f:"'Satisfy',cursive",w:"400",s:"normal",cat:"Best Free Fonts"},
  {n:"Marigold (Yemila)",f:"'DM Serif Display',serif",w:"400",s:"normal",cat:"Best Free Fonts"},
  {n:"Oxalis (Fresh Juice)",f:"'Lilita One',cursive",w:"400",s:"normal",cat:"Best Free Fonts"},
  {n:"Lavender (Cute Oscars)",f:"'Quicksand',sans-serif",w:"600",s:"normal",cat:"Best Free Fonts"},
  {n:"Daisy (Rumaniaya)",f:"'Niconne',cursive",w:"400",s:"normal",cat:"Best Free Fonts"},
  {n:"Lotus (Wordan)",f:"'Norican',cursive",w:"400",s:"normal",cat:"Best Free Fonts"},
  {n:"Pansy (Andutione)",f:"'Arizonia',cursive",w:"400",s:"normal",cat:"Best Free Fonts"},
  {n:"Daffodil (Alphakind)",f:"'Alfa Slab One',serif",w:"400",s:"normal",cat:"Best Free Fonts"},
  {n:"Peony (Floridin)",f:"'Cherry Swash',cursive",w:"700",s:"normal",cat:"Best Free Fonts"},
  {n:"Forsythia (Emanie)",f:"'Delius Swash Caps',cursive",w:"400",s:"normal",cat:"Best Free Fonts"},
  {n:"Amaryllis (Quanto)",f:"'Lobster Two',cursive",w:"400",s:"italic",cat:"Best Free Fonts"},
  /* ── Vintage & Retro ── */
  {n:"Vintage Trademark",f:"'Alfa Slab One',serif",w:"400",s:"normal",cat:"Vintage & Retro"},
  {n:"Brand Apparel Script",f:"'Lobster',cursive",w:"400",s:"normal",cat:"Vintage & Retro"},
  {n:"Sale Swash Script",f:"'Yellowtail',cursive",w:"400",s:"normal",cat:"Vintage & Retro"},
  {n:"Daily Deal Script",f:"'Rochester',cursive",w:"400",s:"normal",cat:"Vintage & Retro"},
  {n:"Best Offer Bold",f:"'Abril Fatface',serif",w:"400",s:"normal",cat:"Vintage & Retro"},
  {n:"Trendy Store Script",f:"'Oleo Script',cursive",w:"700",s:"normal",cat:"Vintage & Retro"},
  {n:"Retro Design Script",f:"'Playball',cursive",w:"400",s:"normal",cat:"Vintage & Retro"},
  {n:"Premium Quality",f:"'Oswald',sans-serif",w:"300",s:"normal",cat:"Vintage & Retro"},
  {n:"Genuine Original",f:"'Goudy Bookletter 1911',serif",w:"400",s:"normal",cat:"Vintage & Retro"},
  /* ── Romantic & Girly ── */
  {n:"Summer Muse",f:"'Playfair Display',serif",w:"400",s:"normal",cat:"Romantic & Girly"},
  {n:"Sweet Summer Script",f:"'Great Vibes',cursive",w:"400",s:"normal",cat:"Romantic & Girly"},
  {n:"Dear Diary Script",f:"'Italianno',cursive",w:"400",s:"normal",cat:"Romantic & Girly"},
  {n:"Lovely Whimsy Script",f:"'Allura',cursive",w:"400",s:"normal",cat:"Romantic & Girly"},
  {n:"Velvet Whisper Script",f:"'Parisienne',cursive",w:"400",s:"normal",cat:"Romantic & Girly"},
  {n:"Honey Darling Script",f:"'Tangerine',cursive",w:"700",s:"normal",cat:"Romantic & Girly"},
  {n:"Lovely Letters Script",f:"'Dancing Script',cursive",w:"400",s:"normal",cat:"Romantic & Girly"},
  {n:"Vouge Elite Serif",f:"'Cormorant Garamond',serif",w:"300",s:"normal",cat:"Romantic & Girly"},
  {n:"Soft Romance Script",f:"'Euphoria Script',cursive",w:"400",s:"normal",cat:"Romantic & Girly"},
  {n:"Golden Kiss Script",f:"'Imperial Script',cursive",w:"400",s:"normal",cat:"Romantic & Girly"},
  /* ── Playful & Creative ── */
  {n:"New Post (Paradiso)",f:"'Amatic SC',cursive",w:"700",s:"normal",cat:"Playful & Creative"},
  {n:"Amazing (Bropella)",f:"'Fredericka the Great',serif",w:"400",s:"normal",cat:"Playful & Creative"},
  {n:"Creative (Liber)",f:"'Josefin Slab',serif",w:"700",s:"normal",cat:"Playful & Creative"},
  {n:"Stunning (Raks)",f:"'Lobster Two',cursive",w:"700",s:"italic",cat:"Playful & Creative"},
  {n:"Masterpiece (Ardent)",f:"'Forum',cursive",w:"400",s:"normal",cat:"Playful & Creative"},
  {n:"Eloquence (Carl Brown)",f:"'Cinzel',serif",w:"400",s:"normal",cat:"Playful & Creative"},
  {n:"Gorgeous (Narnia)",f:"'Cherry Swash',cursive",w:"700",s:"normal",cat:"Playful & Creative"},
  {n:"Beautiful (Silver Garden)",f:"'Bellota',cursive",w:"400",s:"italic",cat:"Playful & Creative"},
  {n:"Aesthetic (Beckan)",f:"'Berkshire Swash',cursive",w:"400",s:"normal",cat:"Playful & Creative"},
  {n:"Glamorous (Sometimes)",f:"'Kaushan Script',cursive",w:"400",s:"normal",cat:"Playful & Creative"},
  /* ── Elegant Serif ── */
  {n:"Playfair Display",f:"'Playfair Display',serif",w:"400",s:"normal",cat:"Elegant Serif"},
  {n:"Playfair Display Bold",f:"'Playfair Display',serif",w:"700",s:"normal",cat:"Elegant Serif"},
  {n:"Playfair Display Italic",f:"'Playfair Display',serif",w:"400",s:"italic",cat:"Elegant Serif"},
  {n:"Cormorant Garamond Light",f:"'Cormorant Garamond',serif",w:"300",s:"normal",cat:"Elegant Serif"},
  {n:"Cormorant Garamond Italic",f:"'Cormorant Garamond',serif",w:"400",s:"italic",cat:"Elegant Serif"},
  {n:"Bodoni Moda",f:"'Bodoni Moda',serif",w:"400",s:"normal",cat:"Elegant Serif"},
  {n:"DM Serif Display",f:"'DM Serif Display',serif",w:"400",s:"normal",cat:"Elegant Serif"},
  {n:"DM Serif Display Italic",f:"'DM Serif Display',serif",w:"400",s:"italic",cat:"Elegant Serif"},
  {n:"Cinzel Regular",f:"'Cinzel',serif",w:"400",s:"normal",cat:"Elegant Serif"},
  {n:"Cinzel Bold",f:"'Cinzel',serif",w:"700",s:"normal",cat:"Elegant Serif"},
  {n:"Cinzel Decorative Bold",f:"'Cinzel Decorative',serif",w:"700",s:"normal",cat:"Elegant Serif"},
  {n:"GFS Didot",f:"'GFS Didot',serif",w:"400",s:"normal",cat:"Elegant Serif"},
  {n:"Spectral Light",f:"'Spectral',serif",w:"300",s:"normal",cat:"Elegant Serif"},
  {n:"Spectral Bold",f:"'Spectral',serif",w:"700",s:"normal",cat:"Elegant Serif"},
  {n:"Vidaloka",f:"'Vidaloka',serif",w:"400",s:"normal",cat:"Elegant Serif"},
  {n:"EB Garamond",f:"'EB Garamond',serif",w:"400",s:"normal",cat:"Elegant Serif"},
  {n:"EB Garamond Italic",f:"'EB Garamond',serif",w:"400",s:"italic",cat:"Elegant Serif"},
  {n:"Libre Baskerville",f:"'Libre Baskerville',serif",w:"400",s:"normal",cat:"Elegant Serif"},
  {n:"Lora Regular",f:"'Lora',serif",w:"400",s:"normal",cat:"Elegant Serif"},
  {n:"Lora Italic",f:"'Lora',serif",w:"400",s:"italic",cat:"Elegant Serif"},
  {n:"Merriweather",f:"'Merriweather',serif",w:"400",s:"normal",cat:"Elegant Serif"},
  {n:"Abril Fatface",f:"'Abril Fatface',serif",w:"400",s:"normal",cat:"Elegant Serif"},
  {n:"Crimson Text",f:"'Crimson Text',serif",w:"400",s:"normal",cat:"Elegant Serif"},
  {n:"Crimson Text Italic",f:"'Crimson Text',serif",w:"400",s:"italic",cat:"Elegant Serif"},
  {n:"Lusitana",f:"'Lusitana',serif",w:"400",s:"normal",cat:"Elegant Serif"},
  {n:"Roboto Slab",f:"'Roboto Slab',serif",w:"400",s:"normal",cat:"Elegant Serif"},
  {n:"Zilla Slab",f:"'Zilla Slab',serif",w:"400",s:"normal",cat:"Elegant Serif"},
  /* ── Elegant Script ── */
  {n:"Great Vibes",f:"'Great Vibes',cursive",w:"400",s:"normal",cat:"Elegant Script"},
  {n:"Sacramento",f:"'Sacramento',cursive",w:"400",s:"normal",cat:"Elegant Script"},
  {n:"Allura",f:"'Allura',cursive",w:"400",s:"normal",cat:"Elegant Script"},
  {n:"Alex Brush",f:"'Alex Brush',cursive",w:"400",s:"normal",cat:"Elegant Script"},
  {n:"Italianno",f:"'Italianno',cursive",w:"400",s:"normal",cat:"Elegant Script"},
  {n:"Tangerine Regular",f:"'Tangerine',cursive",w:"400",s:"normal",cat:"Elegant Script"},
  {n:"Tangerine Bold",f:"'Tangerine',cursive",w:"700",s:"normal",cat:"Elegant Script"},
  {n:"Pinyon Script",f:"'Pinyon Script',cursive",w:"400",s:"normal",cat:"Elegant Script"},
  {n:"Euphoria Script",f:"'Euphoria Script',cursive",w:"400",s:"normal",cat:"Elegant Script"},
  {n:"Mr Dafoe",f:"'Mr Dafoe',cursive",w:"400",s:"normal",cat:"Elegant Script"},
  {n:"Imperial Script",f:"'Imperial Script',cursive",w:"400",s:"normal",cat:"Elegant Script"},
  {n:"Mrs Saint Delafield",f:"'Mrs Saint Delafield',cursive",w:"400",s:"normal",cat:"Elegant Script"},
  {n:"Rouge Script",f:"'Rouge Script',cursive",w:"400",s:"normal",cat:"Elegant Script"},
  {n:"Arizonia",f:"'Arizonia',cursive",w:"400",s:"normal",cat:"Elegant Script"},
  {n:"Aguafina Script",f:"'Aguafina Script',cursive",w:"400",s:"normal",cat:"Elegant Script"},
  {n:"Zeyada",f:"'Zeyada',cursive",w:"400",s:"normal",cat:"Elegant Script"},
  {n:"Herr Von Muellerhoff",f:"'Herr Von Muellerhoff',cursive",w:"400",s:"normal",cat:"Elegant Script"},
  {n:"Meie Script",f:"'Meie Script',cursive",w:"400",s:"normal",cat:"Elegant Script"},
  {n:"Ruthie",f:"'Ruthie',cursive",w:"400",s:"normal",cat:"Elegant Script"},
  {n:"Loved by the King",f:"'Loved by the King',cursive",w:"400",s:"normal",cat:"Elegant Script"},
  {n:"La Belle Aurore",f:"'La Belle Aurore',cursive",w:"400",s:"normal",cat:"Elegant Script"},
  {n:"Give You Glory",f:"'Give You Glory',cursive",w:"400",s:"normal",cat:"Elegant Script"},
  {n:"Covered by Your Grace",f:"'Covered by Your Grace',cursive",w:"400",s:"normal",cat:"Elegant Script"},
  {n:"Dawning of a New Day",f:"'Dawning of a New Day',cursive",w:"400",s:"normal",cat:"Elegant Script"},
];

const GFONTS = "https://fonts.googleapis.com/css2?family=Nunito:wght@400;600;700;800;900&family=Playfair+Display:ital,wght@0,400;0,700;1,400;1,700&family=Playfair+Display+SC:wght@400;700&family=Cinzel:wght@400;700&family=Cinzel+Decorative:wght@400;700&family=Josefin+Sans:wght@300;400;700&family=Josefin+Slab:ital,wght@0,300;0,400;0,700;1,400&family=Montserrat:wght@400;700;900&family=Lancelot&family=Quicksand:wght@400;600&family=Raleway:wght@200;300;400;700;900&family=Libre+Baskerville:ital,wght@0,400;0,700;1,400&family=Lato:wght@300;400;700&family=Open+Sans:wght@300;400&family=Tangerine:wght@400;700&family=Pinyon+Script&family=Parisienne&family=Berkshire+Swash&family=Cherry+Swash:wght@400;700&family=Oleo+Script:wght@400;700&family=Cookie&family=Allura&family=Alex+Brush&family=Euphoria+Script&family=Kaushan+Script&family=Lobster&family=Lobster+Two:ital,wght@0,400;0,700;1,400&family=Pacifico&family=Satisfy&family=Crimson+Text:ital,wght@0,400;0,600;1,400&family=Vidaloka&family=Spectral:ital,wght@0,300;0,400;0,700;1,400&family=GFS+Didot&family=IM+Fell+English:ital@0;1&family=Fredericka+the+Great&family=Alfa+Slab+One&family=Fjalla+One&family=Bitter:ital,wght@0,400;0,700;1,400&family=Lora:ital,wght@0,400;0,700;1,400&family=Merriweather:ital,wght@0,300;0,400;0,700;1,400&family=EB+Garamond:ital,wght@0,400;0,700;1,400&family=Cormorant+Garamond:ital,wght@0,300;0,400;0,700;1,400&family=Bodoni+Moda:ital,wght@0,400;0,700;1,400&family=DM+Serif+Display:ital@0;1&family=Abril+Fatface&family=Oswald:wght@300;400;700&family=Dancing+Script:wght@400;700&family=Great+Vibes&family=Sacramento&family=Imperial+Script&family=Arizonia&family=Didact+Gothic&family=Tenor+Sans&family=Bellota:ital,wght@0,400;0,700;1,400&family=Source+Serif+4:wght@300;400&family=Roboto+Slab:wght@300;400;700&family=Zilla+Slab:ital,wght@0,300;0,400;0,700;1,400&family=Rokkitt:wght@400;700&family=Cardo:ital,wght@0,400;0,700;1,400&family=Goudy+Bookletter+1911&family=Libre+Caslon+Display&family=Lusitana:wght@400;700&family=Italianno&family=Mrs+Saint+Delafield&family=Rouge+Script&family=Aguafina+Script&family=Zeyada&family=Herr+Von+Muellerhoff&family=Meie+Script&family=Ruthie&family=Loved+by+the+King&family=La+Belle+Aurore&family=Give+You+Glory&family=Covered+By+Your+Grace&family=Dawning+of+a+New+Day&family=Just+Another+Hand&family=Amatic+SC:wght@400;700&family=Norican&family=Niconne&family=Mr+Dafoe&family=Qwitcher+Grypen:wght@300;400;700&family=Yellowtail&family=Rochester&family=Playball&family=Lilita+One&family=Forum&family=Alice&family=Alegreya:ital,wght@0,400;0,700;1,400&family=Averia+Serif+Libre:ital,wght@0,300;0,400;0,700;1,400&family=Delius+Swash+Caps&family=Courgette&family=Cutive+Mono&family=Milonga&family=Glass+Antiqua&family=Sanchez:ital@0;1&display=swap";

/* ─── HELPERS ────────────────────────────────────────── */
const uid = () => Math.random().toString(36).slice(2,9);
const getDaysInMonth = (y,m) => new Date(y,m+1,0).getDate();
const makeMonthDays = (year,month) =>
  Array.from({length:getDaysInMonth(year,month)},(_,i)=>{
    const pl=PLATFORMS[i%PLATFORMS.length];
    return {
      id:uid(), date:new Date(year,month,i+1).toISOString(),
      platform:pl, pillar:PILLARS[i%PILLARS.length], format:FORMATS[pl],
      caption:"", hook:"", notes:"", cta:"", hashtags:"", canvaUrl:"",
      time:TIMES[i%TIMES.length], status:"draft", reach:0, engagement:0,
    };
  });
const makeWorkspace = (name,color,emoji) => {
  const n = new Date();
  return {
    id:uid(), name, color, emoji,
    year:n.getFullYear(), month:n.getMonth(),
    days:makeMonthDays(n.getFullYear(),n.getMonth()),
    createdAt:n.toISOString(),
  };
};
const DEFAULT_WS = [
  makeWorkspace("My Brand",B.lime,"✦"),
  makeWorkspace("Client — Sample Co.",B.pink,"🏢"),
];

/* ─── LOGO — exact brand G with 4-point star cutout ──────── */
const Logo = ({size=32, color=B.pink, animate=true}) => {
  const id = `gl_${size}`;
  return (
    <svg width={size} height={size} viewBox="0 0 100 100" fill="none"
      className={animate?"glim-logo-wrap":undefined}
      style={{overflow:"visible",flexShrink:0}}>
      <defs>
        <linearGradient id={`${id}_holo`} x1="0%" y1="0%" x2="100%" y2="100%">
          <stop offset="0%"   stopColor="#FF3EA5"/>
          <stop offset="40%"  stopColor="#FF3EA5"/>
          <stop offset="70%"  stopColor="#E8309A"/>
          <stop offset="100%" stopColor="#FF3EA5"/>
        </linearGradient>
        <filter id={`${id}_glow`} x="-20%" y="-20%" width="140%" height="140%">
          <feGaussianBlur in="SourceGraphic" stdDeviation="2" result="blur"/>
          <feMerge><feMergeNode in="blur"/><feMergeNode in="SourceGraphic"/></feMerge>
        </filter>
        {/* clip the star OUT of the G shape */}
        <mask id={`${id}_mask`}>
          <rect width="100" height="100" fill="white"/>
          {/* 4-point star cutout — sits inside the G counter */}
          <path d="M46 50 L50 39 L54 50 L65 50 L54 56 L57 67 L50 61 L43 67 L46 56 L35 50 Z"
            fill="black"/>
        </mask>
      </defs>
      {/* G shape — thick rounded letter matching brand */}
      <g filter={`url(#${id}_glow)`}>
        {/* outer G arc */}
        <path
          d="M82 28 C74 14 58 8 44 10 C24 13 10 28 10 50 C10 72 26 90 50 90
             C66 90 78 82 84 70 L84 48 L52 48 L52 58 L72 58
             C68 68 60 74 50 74 C34 74 24 63 24 50
             C24 37 34 26 48 26 C57 26 65 30 70 37 Z"
          fill={`url(#${id}_holo)`}
          mask={`url(#${id}_mask)`}
        />
      </g>
      {/* top sparkle star above G */}
      <path className="glim-star-1"
        d="M62 8 L63.4 12.6 L68 14 L63.4 15.4 L62 20 L60.6 15.4 L56 14 L60.6 12.6 Z"
        fill={B.pink} opacity=".9"/>
    </svg>
  );
};

/* Full wordmark — GLIMIFY STUDIO matching brand images */
const LogoWord = ({size=18, showStudio=false}) => (
  <div style={{display:"flex",flexDirection:"column",lineHeight:1}}>
    <span style={{fontSize:size,fontWeight:900,color:B.pink,letterSpacing:1,
      fontFamily:"'Nunito',sans-serif",lineHeight:1,textTransform:"uppercase"}}>
      GLIMIFY
    </span>
    {showStudio&&(
      <span style={{fontSize:size*.45,fontWeight:700,color:B.pink,
        letterSpacing:4,textTransform:"uppercase",
        fontFamily:"'Nunito',sans-serif",textAlign:"center",
        borderTop:`1px solid ${B.pink}55`,marginTop:2,paddingTop:2,opacity:.7}}>
        — STUDIO —
      </span>
    )}
  </div>
);

/* ─── MINI UI ────────────────────────────────────────── */
const Pill = ({label,color}) => (
  <span style={{fontSize:10,fontWeight:600,padding:"2px 8px",borderRadius:20,
    background:`${color}22`,color,border:`1px solid ${color}33`,
    whiteSpace:"nowrap",flexShrink:0}}>{label}</span>
);
const Lbl = ({children}) => (
  <div style={{fontSize:10,color:B.muted,fontWeight:700,letterSpacing:.5,marginBottom:4}}>{children}</div>
);
const FInput = ({value,onChange,placeholder,style={}}) => (
  <input value={value} onChange={onChange} placeholder={placeholder}
    style={{width:"100%",background:B.surface3,border:`1px solid ${B.border2}`,
      color:B.text,borderRadius:8,padding:"9px 11px",fontSize:13,
      boxSizing:"border-box",outline:"none",...style}}/>
);
const FSel = ({value,onChange,options,style={}}) => (
  <select value={value} onChange={onChange}
    style={{width:"100%",background:B.surface3,border:`1px solid ${B.border2}`,
      color:B.text,borderRadius:8,padding:"9px 11px",fontSize:13,
      boxSizing:"border-box",outline:"none",cursor:"pointer",...style}}>
    {options.map(o=>typeof o==="string"
      ?<option key={o} style={{background:B.surface3}}>{o}</option>
      :<option key={o.v} value={o.v} style={{background:B.surface3}}>{o.l}</option>)}
  </select>
);
const Card = ({children,accent,style={}}) => (
  <div style={{background:B.surface,border:`1px solid ${B.border}`,
    borderTop:accent?`2px solid ${accent}`:"none",
    borderRadius:12,padding:16,...style}}>{children}</div>
);
const Toast = ({msg}) => msg?(
  <div style={{position:"fixed",bottom:24,right:24,zIndex:9999,
    background:B.surface2,color:B.lime,fontWeight:800,fontSize:12,
    letterSpacing:2,textTransform:"uppercase",padding:"12px 22px",
    borderLeft:`3px solid ${B.pink}`,borderRadius:"0 10px 10px 0",
    boxShadow:"0 8px 32px rgba(0,0,0,.8)",pointerEvents:"none",
    animation:"glimToast .3s ease"}}>
    {msg}
  </div>
):null;

/* ─── ADS ────────────────────────────────────────────── */
const AD_BRANDS = [
  {name:"Canva Pro",     tagline:"Design anything. Publish everywhere.", color:B.purple, emoji:"🎨"},
  {name:"Notion AI",     tagline:"Your second brain — now smarter.",      color:B.blue,   emoji:"📝"},
  {name:"Buffer",        tagline:"Schedule smarter. Grow faster.",        color:B.lime,   emoji:"📅"},
  {name:"Adobe Express", tagline:"Make content that stops the scroll.",   color:B.pink,   emoji:"✨"},
];
const BANNER_ADS = [
  {label:"🎨 Canva Pro — Design content 10× faster",       cta:"Try Free",    color:B.purple},
  {label:"📅 Buffer — Schedule 30 days of posts in 1hr",   cta:"Get Started", color:B.blue},
  {label:"📊 Later — Visual Instagram planner & analytics", cta:"Explore",     color:B.pink},
  {label:"✨ Adobe Express — Stunning creatives in minutes", cta:"Try Free",    color:B.orange},
];
const BannerAd = ({style={}}) => {
  const ad = BANNER_ADS[Math.floor(Date.now()/10000)%BANNER_ADS.length];
  return (
    <div style={{background:`${ad.color}14`,border:`1px solid ${ad.color}33`,
      borderRadius:10,padding:"10px 14px",display:"flex",alignItems:"center",
      justifyContent:"space-between",gap:10,flexWrap:"wrap",...style}}>
      <div style={{display:"flex",alignItems:"center",gap:8,flex:1,minWidth:0}}>
        <span style={{fontSize:9,color:ad.color,fontWeight:700,background:`${ad.color}22`,
          padding:"1px 6px",borderRadius:4,flexShrink:0,letterSpacing:1}}>SPONSORED</span>
        <span style={{fontSize:12,overflow:"hidden",textOverflow:"ellipsis",whiteSpace:"nowrap"}}>{ad.label}</span>
      </div>
      <a href="#" onClick={e=>e.preventDefault()}
        style={{background:ad.color,color:B.black,fontSize:11,fontWeight:700,
          padding:"5px 12px",borderRadius:20,textDecoration:"none",flexShrink:0}}>
        {ad.cta}
      </a>
    </div>
  );
};
const SidebarAd = () => {
  const ad = AD_BRANDS[Math.floor(Date.now()/8000)%AD_BRANDS.length];
  return (
    <div style={{margin:"10px",background:`linear-gradient(135deg,${ad.color}22,${B.surface2})`,
      border:`1px solid ${ad.color}33`,borderRadius:12,padding:14,textAlign:"center"}}>
      <div style={{fontSize:9,color:ad.color,fontWeight:700,letterSpacing:1,marginBottom:6}}>SPONSORED</div>
      <div style={{fontSize:20,marginBottom:5}}>{ad.emoji}</div>
      <div style={{fontSize:12,fontWeight:700,marginBottom:2}}>{ad.name}</div>
      <div style={{fontSize:10,color:B.muted,marginBottom:10}}>{ad.tagline}</div>
      <a href="#" onClick={e=>e.preventDefault()}
        style={{display:"block",background:ad.color,color:B.black,fontSize:11,
          fontWeight:700,padding:"6px",borderRadius:8,textDecoration:"none"}}>
        Learn More →
      </a>
    </div>
  );
};

/* ══════════════════════════════════════════════════════
   AD GATE — MUST WATCH FULL 15 SECONDS, NO SKIP
══════════════════════════════════════════════════════ */
function AdGate({onComplete}) {
  const [phase,     setPhase]  = useState("intro");
  const [countdown, setCd]     = useState(15);
  const timer = useRef(null);

  const startAd = () => {
    setPhase("watching");
    setCd(15);
    let t = 15;
    timer.current = setInterval(() => {
      t--;
      setCd(t);
      if (t <= 0) { clearInterval(timer.current); setPhase("done"); }
    }, 1000);
  };

  useEffect(() => () => clearInterval(timer.current), []);

  const ad = AD_BRANDS[Math.floor(Date.now()/5000) % AD_BRANDS.length];

  const wrap = {
    position:"fixed",inset:0,background:"#000",zIndex:9000,
    display:"flex",flexDirection:"column",alignItems:"center",
    justifyContent:"center",padding:20,textAlign:"center",
    fontFamily:"'Nunito',system-ui,sans-serif",overflowY:"auto",
  };

  return (
    <div style={wrap}>
      {/* Glimify branding */}
      <div style={{marginBottom:24}}>
        <Logo size={52}/>
        <div style={{marginTop:10,marginBottom:3}}><LogoWord size={26}/></div>
        <div style={{fontSize:10,color:B.muted,letterSpacing:3,textTransform:"uppercase"}}>
          Free Content OS
        </div>
      </div>

      {/* INTRO */}
      {phase==="intro"&&(
        <div style={{width:"100%",maxWidth:440}}>
          <div style={{background:B.surface,border:`1px solid ${B.border2}`,
            borderRadius:16,padding:28,marginBottom:14}}>
            <div style={{fontSize:30,marginBottom:10}}>📢</div>
            <div style={{fontSize:17,fontWeight:800,marginBottom:8}}>
              One quick ad before you start
            </div>
            <div style={{fontSize:13,color:B.muted,lineHeight:1.8,marginBottom:18}}>
              Glimify is <strong style={{color:B.text}}>100% free</strong> forever.
              To keep it running, you must watch a short{" "}
              <strong style={{color:B.lime}}>15-second ad</strong> before each session.
              No skip button.
            </div>
            <div style={{display:"flex",gap:7,justifyContent:"center",flexWrap:"wrap",marginBottom:22}}>
              {["📅 30-Day Calendar","🔤 Font Studio","📊 Analytics","💡 Tips 2026","📋 Monthly Reports","⚡ Brainstorm"].map(f=>(
                <span key={f} style={{background:`${B.pink}18`,border:`1px solid ${B.pink}33`,
                  color:B.pink,fontSize:10,padding:"3px 11px",borderRadius:20}}>{f}</span>
              ))}
            </div>
            <button onClick={startAd}
              style={{width:"100%",background:`linear-gradient(90deg,${B.pink},${B.lime})`,
                border:"none",color:B.black,fontWeight:900,fontSize:15,
                padding:"14px",borderRadius:30,cursor:"pointer",
                fontFamily:"'Nunito',sans-serif"}}>
              Watch Ad &amp; Unlock Glimify →
            </button>
          </div>
          <div style={{fontSize:11,color:B.muted}}>
            Support Glimify by watching · 100% free · no payment needed
          </div>
        </div>
      )}

      {/* WATCHING — NO SKIP */}
      {phase==="watching"&&(
        <div style={{width:"100%",maxWidth:500}}>
          <div style={{background:B.surface,border:`2px solid ${ad.color}`,
            borderRadius:16,overflow:"hidden",marginBottom:12}}>
            {/* ad creative */}
            <div style={{background:`linear-gradient(135deg,${ad.color}33,${B.surface2})`,
              minHeight:210,display:"flex",flexDirection:"column",
              alignItems:"center",justifyContent:"center",
              gap:10,position:"relative",padding:24}}>
              {/* AD label */}
              <div style={{position:"absolute",top:10,left:12,background:"rgba(0,0,0,.75)",
                color:"#fff",fontSize:9,fontWeight:800,padding:"2px 8px",
                borderRadius:4,letterSpacing:2}}>AD</div>
              {/* countdown pill — no X */}
              <div style={{position:"absolute",top:10,right:12,
                background:"rgba(0,0,0,.75)",color:B.lime,fontSize:12,
                fontWeight:900,padding:"4px 12px",borderRadius:20,letterSpacing:1,
                minWidth:50,textAlign:"center"}}>
                {countdown}s
              </div>
              <div style={{fontSize:54}}>{ad.emoji}</div>
              <div style={{fontSize:22,fontWeight:900,color:ad.color}}>{ad.name}</div>
              <div style={{fontSize:14,color:B.muted,maxWidth:300}}>{ad.tagline}</div>
              <a href="#" onClick={e=>e.preventDefault()}
                style={{background:ad.color,color:B.black,fontWeight:800,
                  fontSize:12,padding:"8px 22px",borderRadius:20,
                  textDecoration:"none",marginTop:4}}>
                Learn More
              </a>
              {/* progress bar */}
              <div style={{position:"absolute",bottom:0,left:0,right:0,height:4,background:B.border2}}>
                <div style={{height:"100%",background:ad.color,transition:"width 1s linear",
                  width:`${((15-countdown)/15)*100}%`}}/>
              </div>
            </div>
            <div style={{padding:"10px 16px",display:"flex",
              justifyContent:"space-between",alignItems:"center",
              borderTop:`1px solid ${B.border2}`}}>
              <div style={{fontSize:11,color:B.muted}}>Ad by {ad.name}</div>
              <div style={{fontSize:11,color:B.muted}}>Glimify · Free Content OS</div>
            </div>
          </div>

          {/* status — no skip */}
          <div style={{background:B.surface,border:`1px solid ${B.border2}`,
            borderRadius:12,padding:"14px 18px",marginBottom:10}}>
            <div style={{display:"flex",justifyContent:"space-between",
              alignItems:"center",gap:12}}>
              <div style={{textAlign:"left"}}>
                <div style={{fontSize:13,fontWeight:700,marginBottom:2}}>
                  {countdown>0?"Please watch the full ad…":"Ad complete!"}
                </div>
                <div style={{fontSize:11,color:B.muted}}>
                  {countdown>0?`${countdown} seconds remaining`:"Entering Glimify now…"}
                </div>
              </div>
              {/* dot progress */}
              <div style={{display:"flex",gap:3,flexShrink:0,flexWrap:"wrap",maxWidth:120,justifyContent:"flex-end"}}>
                {Array.from({length:15}).map((_,i)=>(
                  <div key={i} style={{width:6,height:6,borderRadius:"50%",
                    background:i<(15-countdown)?B.lime:B.border2,
                    transition:"background .3s"}}/>
                ))}
              </div>
            </div>
          </div>
          <div style={{fontSize:10,color:B.muted,letterSpacing:.5}}>
            ⚠️ Ad cannot be skipped · helps keep Glimify free for everyone
          </div>
        </div>
      )}

      {/* DONE */}
      {phase==="done"&&(
        <div style={{width:"100%",maxWidth:400}}>
          <div style={{fontSize:52,marginBottom:14}}>🎉</div>
          <div style={{fontSize:22,fontWeight:800,marginBottom:8,color:B.lime}}>
            You're in!
          </div>
          <div style={{fontSize:13,color:B.muted,marginBottom:24,lineHeight:1.7}}>
            Thanks for supporting Glimify. You now have full access for this session. Enjoy!
          </div>
          <button onClick={onComplete}
            style={{width:"100%",background:`linear-gradient(90deg,${B.pink},${B.lime})`,
              border:"none",color:B.black,fontWeight:900,fontSize:15,
              padding:"14px",borderRadius:30,cursor:"pointer",
              fontFamily:"'Nunito',sans-serif"}}>
            Enter Glimify ✦
          </button>
        </div>
      )}
    </div>
  );
}

/* ══════════════════════════════════════════════════════
   SUPABASE CONFIG
   Replace these two values with yours from:
   Supabase Dashboard → Settings → API
══════════════════════════════════════════════════════ */
const SUPA_URL  = "https://YOUR_PROJECT_ID.supabase.co";
const SUPA_ANON = "YOUR_ANON_PUBLIC_KEY";

/* ─── SUPABASE CLIENT — installed via npm, not dynamic import ─── */
/* Run: npm install @supabase/supabase-js  before deploying        */
let _supa = null;
const getSupa = () => {
  if (_supa) return _supa;
  if (SUPA_URL.includes("YOUR_PROJECT")) return null;
  try {
    _supa = createClient(SUPA_URL, SUPA_ANON);
    return _supa;
  } catch { return null; }
};

/* ─── AUTH HELPERS — Magic Link ────────────────────── */
const sendMagicLink = async (email) => {
  const supa = getSupa();
  if (!supa) throw new Error("Supabase not configured yet. Add your keys.");
  const { error } = await supa.auth.signInWithOtp({
    email,
    options: { emailRedirectTo: window.location.origin },
  });
  if (error) throw error;
};

const signOut = async () => {
  const supa = getSupa();
  if (!supa) return;
  await supa.auth.signOut();
};

/* save all workspaces for a user */
const saveToCloud = async (userId, workspaces, wsId) => {
  const supa = getSupa();
  if (!supa || !userId) return;
  await supa.from("glimify_data").upsert({
    user_id: userId,
    workspaces: JSON.stringify(workspaces),
    active_ws_id: wsId,
    updated_at: new Date().toISOString(),
  }, { onConflict: "user_id" });
};

/* load all workspaces for a user */
const loadFromCloud = async (userId) => {
  const supa = getSupa();
  if (!supa || !userId) return null;
  const { data } = await supa
    .from("glimify_data")
    .select("workspaces, active_ws_id")
    .eq("user_id", userId)
    .single();
  if (!data) return null;
  return {
    workspaces: JSON.parse(data.workspaces),
    wsId: data.active_ws_id,
  };
};

/* ─── MAGIC LINK SIGN IN SCREEN ─────────────────────── */
function SignInScreen({ onSkip }) {
  const [email,   setEmail]   = useState("");
  const [sent,    setSent]    = useState(false);
  const [loading, setLoading] = useState(false);
  const [error,   setError]   = useState("");

  const handleSend = async (e) => {
    e.preventDefault();
    if (!email.trim()) return;
    setLoading(true); setError("");
    try {
      await sendMagicLink(email.trim());
      setSent(true);
    } catch(err) {
      setError(err.message || "Could not send link. Check your Supabase config.");
    }
    setLoading(false);
  };

  const supaReady = !SUPA_URL.includes("YOUR_PROJECT");

  return (
    <div style={{
      minHeight:"100vh", background:B.bg,
      fontFamily:"'Nunito',system-ui,sans-serif",
      display:"flex", flexDirection:"column",
      alignItems:"center", justifyContent:"center",
      padding:24, position:"relative", overflow:"hidden",
    }}>
      <div style={{position:"absolute",top:"-10%",left:"-5%",width:400,height:400,
        borderRadius:"50%",background:B.pink,opacity:.06,filter:"blur(80px)",pointerEvents:"none"}}/>
      <div style={{position:"absolute",bottom:"-10%",right:"-5%",width:350,height:350,
        borderRadius:"50%",background:B.lime,opacity:.05,filter:"blur(80px)",pointerEvents:"none"}}/>

      <div style={{textAlign:"center",marginBottom:32}}>
        <Logo size={68} animate/>
        <div style={{marginTop:12,marginBottom:4}}><LogoWord size={26} showStudio/></div>
        <div style={{fontSize:11,color:B.muted,letterSpacing:2,textTransform:"uppercase",marginTop:8}}>
          Your content. Your brand. All in one place.
        </div>
      </div>

      <div style={{width:"100%",maxWidth:420,background:B.surface,
        border:`1px solid ${B.border2}`,borderRadius:20,padding:32,marginBottom:20}}>

        {!sent ? (
          <>
            <div style={{fontSize:20,fontWeight:900,marginBottom:6,textAlign:"center"}}>
              Save your work ✦
            </div>
            <div style={{fontSize:13,color:B.muted,lineHeight:1.7,textAlign:"center",marginBottom:24}}>
              Enter your email and we'll send you a magic link — no password ever. Click it to sign in and your calendar syncs across every device automatically.
            </div>

            {!supaReady && (
              <div style={{background:`${B.yellow}12`,border:`1px solid ${B.yellow}33`,
                borderRadius:10,padding:14,marginBottom:16,textAlign:"center"}}>
                <div style={{fontSize:11,color:B.yellow,fontWeight:700,marginBottom:3}}>⚙️ Supabase keys not set yet</div>
                <div style={{fontSize:10,color:B.muted,lineHeight:1.5}}>
                  Add SUPA_URL and SUPA_ANON to enable cloud save. Data saves to this browser until then.
                </div>
              </div>
            )}

            <form onSubmit={handleSend}>
              <div style={{marginBottom:12}}>
                <label style={{fontSize:10,color:B.muted,fontWeight:700,
                  letterSpacing:1,textTransform:"uppercase",display:"block",marginBottom:6}}>
                  Your Email
                </label>
                <input type="email" value={email} required
                  onChange={e=>setEmail(e.target.value)}
                  placeholder="you@example.com"
                  style={{width:"100%",background:B.surface2,border:`1.5px solid ${B.border2}`,
                    color:B.text,borderRadius:10,padding:"12px 14px",fontSize:14,
                    boxSizing:"border-box",outline:"none",transition:"border-color .2s"}}
                  onFocus={e=>e.target.style.borderColor=B.pink}
                  onBlur={e=>e.target.style.borderColor=B.border2}
                />
              </div>

              {error && (
                <div style={{background:`${B.red}18`,border:`1px solid ${B.red}33`,
                  borderRadius:8,padding:"10px 14px",fontSize:12,color:B.red,marginBottom:12}}>
                  ⚠️ {error}
                </div>
              )}

              <button type="submit" disabled={loading||!email.trim()}
                style={{width:"100%",
                  background:loading||!email.trim()?B.surface2:`linear-gradient(90deg,${B.pink},${B.lime})`,
                  border:"none",
                  color:loading||!email.trim()?B.muted:B.black,
                  fontWeight:900,fontSize:14,padding:"13px",borderRadius:12,
                  cursor:loading||!email.trim()?"not-allowed":"pointer",
                  fontFamily:"'Nunito',sans-serif",marginBottom:12}}>
                {loading?"Sending magic link…":"✦ Send Magic Link"}
              </button>
            </form>

            <div style={{display:"flex",alignItems:"center",gap:10,margin:"4px 0 14px"}}>
              <div style={{flex:1,height:1,background:B.border2}}/>
              <span style={{fontSize:11,color:B.muted}}>or</span>
              <div style={{flex:1,height:1,background:B.border2}}/>
            </div>

            <button onClick={onSkip}
              style={{width:"100%",background:"transparent",border:`1px solid ${B.border2}`,
                color:B.muted,borderRadius:12,padding:"11px",fontSize:13,
                cursor:"pointer",fontFamily:"'Nunito',sans-serif",fontWeight:600}}>
              Continue without saving →
            </button>

            <div style={{fontSize:10,color:B.muted,textAlign:"center",marginTop:14,lineHeight:1.6}}>
              🔒 No password ever · We only use your email to sign you in · Never shared
            </div>
          </>
        ) : (
          <div style={{textAlign:"center",padding:"12px 0"}}>
            <div style={{fontSize:48,marginBottom:16}}>📬</div>
            <div style={{fontSize:20,fontWeight:900,marginBottom:8,color:B.lime}}>
              Check your email!
            </div>
            <div style={{fontSize:13,color:B.muted,lineHeight:1.8,marginBottom:20}}>
              We sent a magic link to<br/>
              <strong style={{color:B.text}}>{email}</strong><br/><br/>
              Click the link in that email and you'll be signed in automatically. The link expires in 1 hour.
            </div>
            <div style={{background:B.surface2,border:`1px solid ${B.border2}`,
              borderRadius:10,padding:14,marginBottom:20,fontSize:12,color:B.muted,lineHeight:1.6}}>
              📌 Can't find it? Check your spam folder. The email comes from Supabase on behalf of Glimify.
            </div>
            <button onClick={()=>{setSent(false);setEmail("");}}
              style={{background:"transparent",border:`1px solid ${B.border2}`,
                color:B.muted,borderRadius:10,padding:"10px 20px",
                fontSize:12,cursor:"pointer",fontFamily:"'Nunito',sans-serif"}}>
              ← Try a different email
            </button>
          </div>
        )}
      </div>

      <div style={{display:"flex",gap:8,flexWrap:"wrap",justifyContent:"center",maxWidth:420}}>
        {["📅 Calendar synced","🏢 Workspaces private","🔄 Any device","🔒 Your data only","💸 Always free"].map(f=>(
          <span key={f} style={{background:B.surface,border:`1px solid ${B.border2}`,
            color:B.muted,fontSize:11,padding:"5px 12px",borderRadius:20}}>{f}</span>
        ))}
      </div>
    </div>
  );
}

/* ─── PROFILE PAGE ──────────────────────────────────── */
/* ─── PROFILE PAGE ──────────────────────────────────── */
function ProfilePage({ user, workspaces, onSignOut, onClose, bp }) {
  const [syncing,  setSyncing]  = useState(false);
  const [syncMsg,  setSyncMsg]  = useState("");
  const [deleting, setDeleting] = useState(false);

  const avatar = user?.user_metadata?.avatar_url;
  const name   = user?.user_metadata?.full_name || user?.email?.split("@")[0] || "Creator";
  const email  = user?.email || "";
  const joined = user?.created_at
    ? new Date(user.created_at).toLocaleDateString("en-US",{month:"long",year:"numeric"})
    : "Today";

  const totalDays   = workspaces.reduce((a,w)=>a+w.days.length, 0);
  const totalPublished = workspaces.reduce((a,w)=>a+w.days.filter(d=>d.status==="published").length, 0);
  const totalCaptions  = workspaces.reduce((a,w)=>a+w.days.filter(d=>d.caption).length, 0);

  const handleManualSync = async () => {
    setSyncing(true); setSyncMsg("");
    try {
      await saveToCloud(user.id, workspaces, workspaces[0]?.id);
      setSyncMsg("✦ Synced successfully!");
    } catch { setSyncMsg("⚠️ Sync failed — check connection"); }
    setSyncing(false);
    setTimeout(()=>setSyncMsg(""),3000);
  };

  return (
    <div style={{position:"fixed",inset:0,background:"rgba(0,0,0,.85)",
      zIndex:500,display:"flex",alignItems:"center",
      justifyContent:"center",padding:20,
      fontFamily:"'Nunito',system-ui,sans-serif"}}>
      <div style={{width:"100%",maxWidth:440,
        background:B.surface,border:`1px solid ${B.border2}`,
        borderRadius:20,overflow:"hidden",
        maxHeight:"90vh",overflowY:"auto"}}>

        {/* header bg */}
        <div style={{background:`linear-gradient(135deg,${B.pink}22,${B.lime}0a)`,
          borderBottom:`1px solid ${B.border2}`,padding:"24px 24px 20px",
          position:"relative"}}>
          <button onClick={onClose}
            style={{position:"absolute",top:16,right:16,
              background:"none",border:"none",color:B.muted,
              fontSize:18,cursor:"pointer"}}>✕</button>

          <div style={{display:"flex",alignItems:"center",gap:14}}>
            {/* avatar */}
            <div style={{position:"relative",flexShrink:0}}>
              {avatar
                ? <img src={avatar} alt={name} width={60} height={60}
                    style={{borderRadius:"50%",border:`2px solid ${B.pink}`,objectFit:"cover"}}/>
                : <div style={{width:60,height:60,borderRadius:"50%",
                    background:`linear-gradient(135deg,${B.pink},${B.lime})`,
                    display:"flex",alignItems:"center",justifyContent:"center",
                    fontSize:24,fontWeight:900,color:B.black}}>
                    {name[0]?.toUpperCase()}
                  </div>
              }
              <div style={{position:"absolute",bottom:0,right:0,
                background:B.lime,borderRadius:"50%",width:16,height:16,
                display:"flex",alignItems:"center",justifyContent:"center",
                fontSize:9,border:`2px solid ${B.surface}`}}>✓</div>
            </div>

            <div style={{minWidth:0}}>
              <div style={{fontSize:17,fontWeight:900,marginBottom:2,
                overflow:"hidden",textOverflow:"ellipsis",whiteSpace:"nowrap"}}>
                {name}
              </div>
              <div style={{fontSize:11,color:B.muted,marginBottom:4,
                overflow:"hidden",textOverflow:"ellipsis"}}>
                {email}
              </div>
              <div style={{display:"inline-flex",alignItems:"center",gap:5,
                background:`${B.lime}22`,border:`1px solid ${B.lime}44`,
                color:B.lime,fontSize:9,fontWeight:800,
                padding:"2px 10px",borderRadius:20,letterSpacing:1}}>
                ✦ GLIMIFY CREATOR
              </div>
            </div>
          </div>

          <div style={{fontSize:10,color:B.muted,marginTop:14}}>
            Member since {joined}
          </div>
        </div>

        {/* stats */}
        <div style={{display:"grid",gridTemplateColumns:"repeat(3,1fr)",
          gap:1,background:B.border2}}>
          {[
            {l:"Total Days",v:totalDays,     c:B.lime},
            {l:"Published", v:totalPublished,c:B.pink},
            {l:"Captions",  v:totalCaptions, c:B.purple},
          ].map(s=>(
            <div key={s.l} style={{background:B.surface,padding:"14px 10px",textAlign:"center"}}>
              <div style={{fontSize:22,fontWeight:900,color:s.c}}>{s.v}</div>
              <div style={{fontSize:9,color:B.muted,marginTop:2}}>{s.l}</div>
            </div>
          ))}
        </div>

        <div style={{padding:20}}>
          {/* workspaces list */}
          <div style={{fontSize:10,color:B.muted,fontWeight:700,
            letterSpacing:1,textTransform:"uppercase",marginBottom:10}}>
            Your Workspaces
          </div>
          {workspaces.map(w=>(
            <div key={w.id} style={{display:"flex",alignItems:"center",gap:10,
              background:B.surface2,border:`1px solid ${B.border2}`,
              borderRadius:10,padding:"10px 14px",marginBottom:8}}>
              <span style={{fontSize:16}}>{w.emoji}</span>
              <div style={{flex:1,minWidth:0}}>
                <div style={{fontSize:13,fontWeight:700,
                  overflow:"hidden",textOverflow:"ellipsis",whiteSpace:"nowrap"}}>
                  {w.name}
                </div>
                <div style={{fontSize:10,color:B.muted}}>
                  {w.days.length} days · {w.days.filter(d=>d.status==="published").length} published
                </div>
              </div>
              <div style={{width:8,height:8,borderRadius:"50%",
                background:w.color||B.lime,flexShrink:0}}/>
            </div>
          ))}

          {/* sync button */}
          <button onClick={handleManualSync} disabled={syncing}
            style={{width:"100%",background:syncing?B.surface2:`${B.lime}22`,
              border:`1px solid ${syncing?B.border2:B.lime}44`,
              color:syncing?B.muted:B.lime,borderRadius:10,
              padding:"11px",fontSize:13,fontWeight:700,
              cursor:syncing?"not-allowed":"pointer",
              fontFamily:"'Nunito',sans-serif",marginTop:4,marginBottom:8}}>
            {syncing?"⏳ Syncing…":"☁️ Sync to Cloud Now"}
          </button>
          {syncMsg&&(
            <div style={{fontSize:11,color:syncMsg.includes("✦")?B.lime:B.red,
              textAlign:"center",marginBottom:8}}>{syncMsg}</div>
          )}

          {/* privacy note */}
          <div style={{background:`${B.green}0a`,border:`1px solid ${B.green}22`,
            borderRadius:8,padding:"10px 14px",fontSize:11,
            color:B.muted,lineHeight:1.6,marginBottom:16}}>
            🔒 Your workspaces are encrypted and private. Only you can see your content. Glimify never shares or reads your data.
          </div>

          {/* sign out */}
          <button onClick={onSignOut}
            style={{width:"100%",background:`${B.red}18`,
              border:`1px solid ${B.red}33`,color:B.red,
              borderRadius:10,padding:"11px",fontSize:13,
              fontWeight:700,cursor:"pointer",
              fontFamily:"'Nunito',sans-serif"}}>
            Sign Out
          </button>
        </div>
      </div>
    </div>
  );
}

/* ══════════════════════════════════════════════════════
   MAIN APP
══════════════════════════════════════════════════════ */
function GlimifyApp() {
  const bp = useBreakpoint();

  useEffect(()=>{
    if(!document.getElementById("gf")){
      const l=document.createElement("link");
      l.id="gf";l.rel="stylesheet";l.href=GFONTS;
      document.head.appendChild(l);
    }
  },[]);

  const [adDone,     setAdDone]     = useState(false);
  const [user,       setUser]       = useState(null);   // Supabase user
  const [authReady,  setAuthReady]  = useState(false);  // finished checking auth
  const [showSignIn, setShowSignIn] = useState(false);  // show sign in screen
  const [showProfile,setShowProfile]= useState(false);  // show profile modal
  const [workspaces, setWS]         = useState(DEFAULT_WS);
  const [wsId,       setWsId]       = useState(DEFAULT_WS[0].id);
  const [tab,        setTab]        = useState("calendar");
  const [selDay,     setSelDay]     = useState(null);
  const [platF,      setPlatF]      = useState("All");
  const [pilF,       setPilF]       = useState("All");
  const [search,     setSearch]     = useState("");
  const [viewMode,   setViewMode]   = useState("list");
  const [toast,      setToast]      = useState("");
  const [newWsOpen,  setNewWsOpen]  = useState(false);
  const [newWsName,  setNwName]     = useState("");
  const [newWsEmoji, setNwEmoji]    = useState("🎯");
  const [newWsColor, setNwColor]    = useState(B.blue);
  const [delConfirm, setDelConfirm] = useState(null);
  /* font */
  const [fontTxt,    setFontTxt]    = useState("Glimify");
  const [fontSz,     setFontSz]     = useState(34);
  const [fontCat,    setFontCat]    = useState("All");
  const [fontSrch,   setFontSrch]   = useState("");
  const [copiedF,    setCopiedF]    = useState(null);
  const [repNotes,   setRepNotes]   = useState("");

  /* ── AUTH INIT — check for existing Supabase session ── */
  useEffect(()=>{
    const initAuth = async () => {
      try {
        const supa = getSupa();
        if (!supa) { setAuthReady(true); return; }

        // Check for OAuth redirect callback
        const { data: { session } } = await supa.auth.getSession();
        if (session?.user) {
          setUser(session.user);
          // Load cloud data for this user
          const cloud = await loadFromCloud(session.user.id);
          if (cloud?.workspaces?.length) {
            setWS(cloud.workspaces);
            if (cloud.wsId) setWsId(cloud.wsId);
          }
        }

        // Listen for auth changes (sign in / sign out)
        supa.auth.onAuthStateChange(async (event, session) => {
          if (event === "SIGNED_IN" && session?.user) {
            setUser(session.user);
            const cloud = await loadFromCloud(session.user.id);
            if (cloud?.workspaces?.length) {
              setWS(cloud.workspaces);
              if (cloud.wsId) setWsId(cloud.wsId);
            }
            setShowSignIn(false);
            setAdDone(true); // signed-in users skip re-watching ad
          }
          if (event === "SIGNED_OUT") {
            setUser(null);
          }
        });
      } catch {}
      setAuthReady(true);
    };
    initAuth();
  },[]);

  /* ── PERSIST — localStorage fallback when not signed in ── */
  useEffect(()=>{
    if (user) return; // cloud handles it
    try{
      const s=localStorage.getItem("glimify_v3");
      if(s){
        const p=JSON.parse(s);
        if(p.workspaces?.length)setWS(p.workspaces);
        if(p.wsId)setWsId(p.wsId);
        if(p.adDone)setAdDone(true);
      }
    }catch{}
  },[user]);

  /* ── SAVE — cloud if signed in, localStorage if not ── */
  useEffect(()=>{
    if(!authReady) return;
    if(user){
      // debounce cloud save 2s after last change
      const t = setTimeout(()=>{ saveToCloud(user.id, workspaces, wsId); }, 2000);
      return ()=>clearTimeout(t);
    } else {
      try{localStorage.setItem("glimify_v3",JSON.stringify({workspaces,wsId,adDone}));}
      catch{}
    }
  },[workspaces,wsId,adDone,user,authReady]);

  const handleSignOut = async () => {
    await signOut();
    setUser(null);
    setShowProfile(false);
    showToast("Signed out — see you soon ✦");
  };

  const ws = workspaces.find(w=>w.id===wsId)||workspaces[0];
  const showToast = msg=>{setToast(msg);setTimeout(()=>setToast(""),2600);};

  const updWs = useCallback(fn=>{
    setWS(prev=>prev.map(w=>w.id===wsId?fn(w):w));
  },[wsId]);

  const updDay = (dayId,field,val)=>{
    updWs(w=>({...w,days:w.days.map(d=>d.id===dayId?{...d,[field]:val}:d)}));
    setSelDay(p=>p?.id===dayId?{...p,[field]:val}:p);
  };

  const changeMonth = delta=>{
    updWs(w=>{
      let m=w.month+delta,y=w.year;
      if(m>11){m=0;y++;} if(m<0){m=11;y--;}
      return{...w,month:m,year:y,days:makeMonthDays(y,m)};
    });
    setSelDay(null);
  };

  const addWs = ()=>{
    if(!newWsName.trim())return;
    const nw=makeWorkspace(newWsName.trim(),newWsColor,newWsEmoji);
    setWS(p=>[...p,nw]);setWsId(nw.id);
    setNewWsOpen(false);setNwName("");
    showToast("Workspace created ✦");
  };
  const deleteWs = id=>{
    if(workspaces.length<=1){showToast("Cannot delete the last workspace");return;}
    const rem=workspaces.filter(w=>w.id!==id);
    setWS(rem);if(wsId===id)setWsId(rem[0].id);
    setDelConfirm(null);showToast("Workspace deleted");
  };

  const published = ws.days.filter(d=>d.status==="published");
  const scheduled = ws.days.filter(d=>d.status==="scheduled");
  const avgEng    = published.length?(published.reduce((a,d)=>a+Number(d.engagement),0)/published.length).toFixed(1):"0.0";
  const topReach  = published.length?Math.max(...published.map(d=>d.reach)):0;

  const filtered = ws.days.filter(d=>{
    const pm=platF==="All"||d.platform===platF;
    const pi=pilF==="All"||d.pillar===pilF;
    const sm=!search||d.caption.toLowerCase().includes(search.toLowerCase())||d.hook.toLowerCase().includes(search.toLowerCase());
    return pm&&pi&&sm;
  });

  const filteredFonts = FONT_DATA.filter(f=>{
    const cm=fontCat==="All"||f.cat===fontCat;
    const sm=!fontSrch||f.n.toLowerCase().includes(fontSrch.toLowerCase())||f.cat.toLowerCase().includes(fontSrch.toLowerCase());
    return cm&&sm;
  });

  const copyFont = (font,idx)=>{
    const css=`font-family: ${font.f};\nfont-weight: ${font.w};\nfont-style: ${font.s};`;
    if(navigator.clipboard&&window.isSecureContext)navigator.clipboard.writeText(css).catch(()=>{});
    setCopiedF(idx);setTimeout(()=>setCopiedF(null),1500);
    showToast(`✦ ${font.n} — copied!`);
  };

  /* ── TABS ── */
  const TABS=[
    {id:"calendar",   label:"Calendar",   icon:"📅"},
    {id:"analytics",  label:"Analytics",  icon:"📊"},
    {id:"report",     label:"Report",     icon:"📋"},
    {id:"tips",       label:"Tips 2026",  icon:"💡"},
    {id:"brainstorm", label:"Brainstorm", icon:"⚡"},
    {id:"fonts",      label:"Font Studio",icon:"🔤"},
    {id:"imagetools", label:"Image Tools",icon:"🖼️"},
    {id:"about",      label:"About",      icon:"✦"},
  ];

  /* ── DAY EDITOR ── */
  const DayEditor=({day})=>{
    const cols2=bp.isMobile?"1fr":"1fr 1fr";
    return(
      <div onClick={e=>e.stopPropagation()}
        style={{marginTop:14,paddingTop:14,borderTop:`1px solid ${B.border2}`}}>
        <div style={{display:"grid",gridTemplateColumns:cols2,gap:8,marginBottom:8}}>
          <div>
            <Lbl>HOOK</Lbl>
            <FInput value={day.hook} onChange={e=>updDay(day.id,"hook",e.target.value)} placeholder="Your scroll-stopper line…"/>
          </div>
          <div>
            <Lbl>POST TIME</Lbl>
            <FSel value={day.time} onChange={e=>updDay(day.id,"time",e.target.value)} options={TIMES}/>
          </div>
        </div>
        <div style={{marginBottom:8}}>
          <Lbl>CAPTION</Lbl>
          <textarea value={day.caption} onChange={e=>updDay(day.id,"caption",e.target.value)}
            placeholder="Write your caption here…" rows={4}
            style={{width:"100%",background:B.surface3,border:`1px solid ${B.border2}`,
              color:B.text,borderRadius:8,padding:"9px 11px",fontSize:13,
              resize:"vertical",boxSizing:"border-box",outline:"none"}}/>
        </div>
        <div style={{display:"grid",gridTemplateColumns:cols2,gap:8,marginBottom:8}}>
          <div>
            <Lbl>CTA</Lbl>
            <FInput value={day.cta} onChange={e=>updDay(day.id,"cta",e.target.value)} placeholder="Save this. DM me. Comment below."/>
          </div>
          <div>
            <Lbl>HASHTAGS</Lbl>
            <FInput value={day.hashtags} onChange={e=>updDay(day.id,"hashtags",e.target.value)} placeholder="#executiveassistant #ea"/>
          </div>
        </div>
        <div style={{display:"grid",gridTemplateColumns:cols2,gap:8,marginBottom:8}}>
          <div>
            <Lbl>CANVA LINK</Lbl>
            <div style={{display:"flex",gap:6}}>
              <FInput value={day.canvaUrl} onChange={e=>updDay(day.id,"canvaUrl",e.target.value)} placeholder="https://canva.com/design/…" style={{flex:1}}/>
              {day.canvaUrl&&(
                <a href={day.canvaUrl} target="_blank" rel="noreferrer"
                  onClick={e=>e.stopPropagation()}
                  style={{background:`${B.purple}22`,border:`1px solid ${B.purple}44`,
                    color:B.purple,borderRadius:8,padding:"9px 11px",
                    fontSize:11,textDecoration:"none",flexShrink:0}}>Open</a>
              )}
            </div>
          </div>
          <div>
            <Lbl>NOTES / CREATIVES</Lbl>
            <FInput value={day.notes} onChange={e=>updDay(day.id,"notes",e.target.value)} placeholder="B-roll needed, template name…"/>
          </div>
        </div>
        <div style={{display:"grid",gridTemplateColumns:cols2,gap:8,marginBottom:10}}>
          <div>
            <Lbl>PLATFORM</Lbl>
            <FSel value={day.platform} onChange={e=>updDay(day.id,"platform",e.target.value)} options={PLATFORMS}/>
          </div>
          <div>
            <Lbl>CONTENT PILLAR</Lbl>
            <FSel value={day.pillar} onChange={e=>updDay(day.id,"pillar",e.target.value)} options={PILLARS}/>
          </div>
        </div>
        <div style={{display:"flex",gap:6}}>
          {["draft","scheduled","published"].map(s=>(
            <button key={s} onClick={()=>updDay(day.id,"status",s)}
              style={{flex:1,padding:"8px 4px",borderRadius:8,fontSize:11,
                cursor:"pointer",fontWeight:day.status===s?700:400,
                border:`1px solid ${day.status===s?STATUS_CFG[s].c:B.border2}`,
                background:day.status===s?`${STATUS_CFG[s].c}18`:"transparent",
                color:day.status===s?STATUS_CFG[s].c:B.muted}}>
              {s.charAt(0).toUpperCase()+s.slice(1)}
            </button>
          ))}
        </div>
      </div>
    );
  };

  /* ══ TAB CONTENTS ══ */
  const CalendarTab=()=>{
    const firstDow=new Date(ws.year,ws.month,1).getDay();
    return(
      <div>
        {/* month nav */}
        <div style={{display:"flex",alignItems:"center",justifyContent:"space-between",marginBottom:14}}>
          <button onClick={()=>changeMonth(-1)}
            style={{background:B.surface2,border:`1px solid ${B.border2}`,
              color:B.text,borderRadius:8,padding:"7px 14px",fontSize:13,cursor:"pointer"}}>
            ← Prev
          </button>
          <div style={{textAlign:"center"}}>
            <div style={{fontSize:bp.isMobile?14:18,fontWeight:800}}>
              {MONTH_NAMES[ws.month]} {ws.year}
            </div>
            <div style={{fontSize:10,color:B.muted}}>
              {ws.days.length} days · {published.length} published · {scheduled.length} scheduled
            </div>
          </div>
          <button onClick={()=>changeMonth(1)}
            style={{background:B.surface2,border:`1px solid ${B.border2}`,
              color:B.text,borderRadius:8,padding:"7px 14px",fontSize:13,cursor:"pointer"}}>
            Next →
          </button>
        </div>

        {/* Coming Soon — AI generator teaser */}
        <div style={{background:`${B.lime}0a`,border:`1px dashed ${B.lime}44`,
          borderRadius:12,padding:14,marginBottom:14,
          display:"flex",alignItems:"center",justifyContent:"space-between",
          flexWrap:"wrap",gap:10}}>
          <div>
            <div style={{fontSize:13,fontWeight:800,color:B.lime,marginBottom:2}}>
              ✦ AI Content Generator — Coming Soon
            </div>
            <div style={{fontSize:11,color:B.muted}}>
              One click to generate 30 days of hooks, captions, CTAs &amp; hashtags. Stay tuned!
            </div>
          </div>
          <span style={{background:`${B.lime}22`,border:`1px solid ${B.lime}44`,
            color:B.lime,fontSize:10,fontWeight:700,padding:"4px 12px",borderRadius:20}}>
            Soon ✦
          </span>
        </div>

        {/* filters */}
        <div style={{display:"flex",gap:8,marginBottom:12,flexWrap:"wrap",alignItems:"center"}}>
          <input value={search} onChange={e=>setSearch(e.target.value)}
            placeholder="🔍 Search…"
            style={{flex:1,minWidth:100,background:B.surface2,border:`1px solid ${B.border2}`,
              color:B.text,borderRadius:8,padding:"7px 11px",fontSize:12,outline:"none"}}/>
          <FSel value={platF} onChange={e=>setPlatF(e.target.value)}
            options={[{v:"All",l:"All Platforms"},...PLATFORMS.map(p=>({v:p,l:p}))]}
            style={{flex:"0 0 auto",width:"auto"}}/>
          <FSel value={pilF} onChange={e=>setPilF(e.target.value)}
            options={[{v:"All",l:"All Pillars"},...PILLARS.map(p=>({v:p,l:p}))]}
            style={{flex:"0 0 auto",width:"auto"}}/>
          <div style={{display:"flex",gap:4,background:B.surface2,
            borderRadius:8,padding:3,border:`1px solid ${B.border2}`}}>
            {[["list","☰"],["grid","⊞"]].map(([m,ic])=>(
              <button key={m} onClick={()=>setViewMode(m)}
                style={{background:viewMode===m?B.surface3:"transparent",border:"none",
                  color:viewMode===m?B.lime:B.muted,borderRadius:6,
                  padding:"5px 10px",fontSize:13,cursor:"pointer"}}>{ic}</button>
            ))}
          </div>
        </div>

        {/* GRID */}
        {viewMode==="grid"&&(
          <div style={{marginBottom:12}}>
            <div style={{display:"grid",gridTemplateColumns:"repeat(7,1fr)",gap:2,marginBottom:4}}>
              {DAY_NAMES.map(d=>(
                <div key={d} style={{textAlign:"center",fontSize:9,color:B.muted,fontWeight:600,padding:"4px 0"}}>{d}</div>
              ))}
            </div>
            <div style={{display:"grid",gridTemplateColumns:"repeat(7,1fr)",gap:2}}>
              {Array.from({length:firstDow}).map((_,i)=><div key={`e${i}`}/>)}
              {ws.days.map(day=>{
                const isSel=selDay?.id===day.id;
                return(
                  <div key={day.id} onClick={()=>setSelDay(isSel?null:day)}
                    style={{background:isSel?`${ws.color||B.lime}22`:B.surface2,
                      border:`1px solid ${isSel?ws.color||B.lime:P_COLOR[day.pillar]||B.border2}`,
                      borderRadius:6,padding:"6px 4px",textAlign:"center",
                      cursor:"pointer",minHeight:44}}>
                    <div style={{fontSize:11,fontWeight:700}}>{new Date(day.date).getDate()}</div>
                    <div style={{fontSize:9,marginTop:1}}>{P_ICON[day.platform]}</div>
                    <div style={{width:5,height:5,borderRadius:"50%",
                      background:STATUS_CFG[day.status]?.c||B.muted,margin:"3px auto 0"}}/>
                  </div>
                );
              })}
            </div>
            {selDay&&(
              <Card style={{marginTop:12,border:`1px solid ${ws.color||B.lime}44`}}>
                <div style={{display:"flex",alignItems:"center",gap:8,marginBottom:4,flexWrap:"wrap"}}>
                  <span style={{fontSize:14}}>{P_ICON[selDay.platform]}</span>
                  <strong style={{fontSize:13}}>
                    {new Date(selDay.date).toLocaleDateString("en-US",{weekday:"long",month:"long",day:"numeric"})}
                  </strong>
                  <Pill label={selDay.pillar} color={P_COLOR[selDay.pillar]}/>
                </div>
                <DayEditor day={selDay}/>
              </Card>
            )}
          </div>
        )}

        {/* LIST */}
        {viewMode==="list"&&(
          <div style={{display:"flex",flexDirection:"column",gap:7}}>
            {filtered.map(day=>{
              const expanded=selDay?.id===day.id;
              const d=new Date(day.date);
              return(
                <div key={day.id} onClick={()=>setSelDay(expanded?null:day)}
                  style={{background:B.surface,
                    border:`1px solid ${expanded?ws.color||B.lime:B.border}`,
                    borderLeft:`3px solid ${P_COLOR[day.pillar]||B.muted}`,
                    borderRadius:11,
                    padding:bp.isMobile?"10px 12px":"12px 14px",
                    cursor:"pointer"}}>
                  <div style={{display:"flex",alignItems:"center",gap:bp.isMobile?8:10}}>
                    <div style={{minWidth:36,textAlign:"center",flexShrink:0}}>
                      <div style={{fontSize:9,color:B.muted,textTransform:"uppercase"}}>
                        {d.toLocaleDateString("en-US",{weekday:"short"})}
                      </div>
                      <div style={{fontSize:bp.isMobile?17:19,fontWeight:800,lineHeight:1.1}}>
                        {d.getDate()}
                      </div>
                      <div style={{fontSize:9,color:B.muted}}>
                        {d.toLocaleDateString("en-US",{month:"short"})}
                      </div>
                    </div>
                    <div style={{width:1,height:36,background:B.border2,flexShrink:0}}/>
                    <div style={{flex:1,minWidth:0}}>
                      <div style={{display:"flex",alignItems:"center",gap:6,marginBottom:3,flexWrap:"wrap"}}>
                        <span style={{fontSize:12}}>{P_ICON[day.platform]}</span>
                        <span style={{fontSize:11,fontWeight:600}}>{day.platform}</span>
                        {!bp.isMobile&&<Pill label={day.pillar} color={P_COLOR[day.pillar]}/>}
                        <span style={{fontSize:10,color:B.muted,marginLeft:"auto",flexShrink:0}}>
                          {day.time}
                        </span>
                      </div>
                      <div style={{fontSize:11,
                        color:day.hook||day.caption?B.text:B.muted,
                        opacity:day.hook||day.caption?1:.4,
                        overflow:"hidden",textOverflow:"ellipsis",whiteSpace:"nowrap"}}>
                        {day.hook||day.caption||"No content yet — tap to edit"}
                      </div>
                    </div>
                    <div style={{display:"flex",flexDirection:"column",alignItems:"flex-end",gap:3,flexShrink:0}}>
                      <span style={{fontSize:10,color:STATUS_CFG[day.status]?.c,
                        background:`${STATUS_CFG[day.status]?.c}18`,
                        padding:"2px 7px",borderRadius:20}}>
                        {STATUS_CFG[day.status]?.label}
                      </span>
                      {day.reach>0&&(
                        <span style={{fontSize:10,color:B.pink}}>🔥{day.reach.toLocaleString()}</span>
                      )}
                    </div>
                  </div>
                  {expanded&&<DayEditor day={day}/>}
                </div>
              );
            })}
          </div>
        )}
        <BannerAd style={{marginTop:18}}/>
      </div>
    );
  };

  const AnalyticsTab=()=>{
    const top=published.length?published.reduce((a,b)=>b.reach>a.reach?b:a):null;
    const bot=published.length?published.reduce((a,b)=>b.engagement<a.engagement?b:a):null;
    return(
      <div style={{display:"flex",flexDirection:"column",gap:12}}>
        {!connected.meta&&!connected.google&&(
          <Card style={{borderTop:`2px solid ${B.yellow}`,padding:14}}>
            <div style={{display:"flex",gap:10}}>
              <span style={{fontSize:20,flexShrink:0}}>⚡</span>
              <div>
                <div style={{fontSize:12,fontWeight:700,color:B.yellow,marginBottom:2}}>
                  Connect accounts for live analytics
                </div>
                <div style={{fontSize:11,color:B.muted,lineHeight:1.5}}>
                  Link Meta or Google in Integrations to pull real data. Mark posts as Published and enter reach/engagement to see stats here.
                </div>
              </div>
            </div>
          </Card>
        )}
        {top&&(
          <Card accent={B.lime}>
            <div style={{fontSize:10,color:B.lime,fontWeight:700,letterSpacing:1,marginBottom:8}}>🏆 TOP PERFORMING POST</div>
            <div style={{fontSize:bp.isMobile?12:14,fontWeight:600,marginBottom:10,lineHeight:1.5}}>
              "{top.hook||top.caption||"No content written yet"}"
            </div>
            <div style={{display:"flex",gap:8,flexWrap:"wrap"}}>
              {[[top.platform,B.blue],[top.format,B.lime],[top.time,B.pink],
                [`${top.reach.toLocaleString()} reach`,B.green],[`${top.engagement}% eng`,B.yellow]].map(([v,c])=>(
                <div key={v} style={{background:`${c}18`,borderRadius:7,padding:"5px 11px",fontSize:12,fontWeight:600,color:c}}>{v}</div>
              ))}
            </div>
          </Card>
        )}
        {bot&&(
          <Card accent={B.red}>
            <div style={{fontSize:10,color:B.red,fontWeight:700,letterSpacing:1,marginBottom:8}}>⚠️ NEEDS IMPROVEMENT</div>
            <div style={{fontSize:bp.isMobile?11:13,color:B.muted,marginBottom:10,lineHeight:1.5}}>
              "{bot.hook||bot.caption||"No content written yet"}"
            </div>
            <div style={{display:"flex",gap:8,flexWrap:"wrap"}}>
              {[[bot.platform,B.red],[`${bot.reach} reach`,B.red],[`${bot.engagement}% eng`,B.red]].map(([v,c])=>(
                <div key={v} style={{background:`${c}18`,borderRadius:7,padding:"5px 11px",fontSize:12,fontWeight:600,color:c}}>{v}</div>
              ))}
            </div>
          </Card>
        )}
        <Card>
          <div style={{fontSize:10,color:B.muted,fontWeight:700,letterSpacing:1,marginBottom:12}}>CONTENT PILLAR DISTRIBUTION</div>
          {PILLARS.map(p=>{
            const cnt=ws.days.filter(d=>d.pillar===p).length;
            const pct=Math.round((cnt/ws.days.length)*100);
            return(
              <div key={p} style={{marginBottom:8}}>
                <div style={{display:"flex",justifyContent:"space-between",marginBottom:3}}>
                  <span style={{fontSize:11}}>{p}</span>
                  <span style={{fontSize:11,color:P_COLOR[p]}}>{cnt} · {pct}%</span>
                </div>
                <div style={{background:B.surface2,borderRadius:4,height:5}}>
                  <div style={{background:P_COLOR[p],height:"100%",borderRadius:4,
                    width:`${pct}%`,transition:"width .6s"}}/>
                </div>
              </div>
            );
          })}
        </Card>
        <Card>
          <div style={{fontSize:10,color:B.muted,fontWeight:700,letterSpacing:1,marginBottom:12}}>PLATFORM BREAKDOWN</div>
          <div style={{display:"grid",gridTemplateColumns:bp.isMobile?"repeat(4,1fr)":"repeat(8,1fr)",gap:8}}>
            {PLATFORMS.map(p=>{
              const cnt=ws.days.filter(d=>d.platform===p).length;
              return(
                <div key={p} style={{background:B.surface2,borderRadius:8,padding:"10px 6px",textAlign:"center"}}>
                  <div style={{fontSize:16,marginBottom:2}}>{P_ICON[p]}</div>
                  <div style={{fontSize:12,fontWeight:700}}>{cnt}</div>
                  <div style={{fontSize:9,color:B.muted}}>{p}</div>
                </div>
              );
            })}
          </div>
        </Card>
        <BannerAd/>
      </div>
    );
  };

  const ReportTab=()=>{
    // repNotes state is hoisted to main app level
    const repData=published.map(d=>({
      date:new Date(d.date).toLocaleDateString("en-US",{month:"short",day:"numeric"}),
      platform:d.platform,pillar:d.pillar,reach:d.reach,eng:d.engagement,
      hook:d.hook||d.caption||"—",
    }));
    return(
      <div>
        <div style={{background:`${B.lime}0a`,border:`1px solid ${B.lime}33`,
          borderRadius:12,padding:16,marginBottom:14}}>
          <div style={{fontSize:bp.isMobile?14:16,fontWeight:800,marginBottom:6}}>
            📋 Monthly Review — {MONTH_NAMES[ws.month]} {ws.year}
          </div>
          <div style={{fontSize:12,color:B.muted,marginBottom:12,lineHeight:1.6}}>
            Track your published content performance. Fill in reach and engagement on each post, then use this report to review your month.
          </div>
          <div style={{display:"grid",gridTemplateColumns:bp.isMobile?"repeat(2,1fr)":"repeat(4,1fr)",gap:8,marginBottom:14}}>
            {[
              {l:"Posts Published",v:published.length,c:B.lime},
              {l:"Scheduled",v:scheduled.length,c:B.blue},
              {l:"Avg Engagement",v:`${avgEng}%`,c:B.purple},
              {l:"Top Reach",v:topReach>0?topReach.toLocaleString():"—",c:B.pink},
            ].map(s=>(
              <div key={s.l} style={{background:B.surface2,borderRadius:8,padding:"10px 12px",
                borderTop:`2px solid ${s.c}`}}>
                <div style={{fontSize:18,fontWeight:800,color:s.c}}>{s.v}</div>
                <div style={{fontSize:10,color:B.muted,marginTop:2}}>{s.l}</div>
              </div>
            ))}
          </div>
          {/* notes area */}
          <Lbl>YOUR NOTES / KEY WINS THIS MONTH</Lbl>
          <textarea value={repNotes} onChange={e=>setRepNotes(e.target.value)}
            placeholder="Write your monthly reflections, wins, what to improve next month…"
            rows={4}
            style={{width:"100%",background:B.surface3,border:`1px solid ${B.border2}`,
              color:B.text,borderRadius:8,padding:"10px 12px",fontSize:13,
              resize:"vertical",boxSizing:"border-box",outline:"none"}}/>
          <div style={{fontSize:11,color:B.muted,marginTop:6,display:"flex",alignItems:"center",gap:6}}>
            <span style={{background:`${B.lime}22`,border:`1px solid ${B.lime}33`,color:B.lime,
              fontSize:9,fontWeight:700,padding:"2px 8px",borderRadius:20}}>AI SOON</span>
            <span>AI-powered analysis coming soon — will auto-generate this report for you</span>
          </div>
        </div>

        {/* published posts table */}
        {repData.length>0?(
          <Card>
            <div style={{fontSize:11,color:B.muted,fontWeight:700,letterSpacing:1,marginBottom:12}}>
              PUBLISHED POSTS THIS MONTH
            </div>
            <div style={{overflowX:"auto"}}>
              <table style={{width:"100%",borderCollapse:"collapse",fontSize:12}}>
                <thead>
                  <tr style={{borderBottom:`1px solid ${B.border2}`}}>
                    {["Date","Platform","Pillar","Reach","Eng %","Hook/Caption"].map(h=>(
                      <th key={h} style={{textAlign:"left",padding:"6px 8px",
                        fontSize:9,color:B.muted,fontWeight:700,
                        letterSpacing:1,textTransform:"uppercase",
                        whiteSpace:"nowrap"}}>{h}</th>
                    ))}
                  </tr>
                </thead>
                <tbody>
                  {repData.map((r,i)=>(
                    <tr key={i} style={{borderBottom:`1px solid ${B.border}`}}>
                      <td style={{padding:"8px",color:B.muted,whiteSpace:"nowrap"}}>{r.date}</td>
                      <td style={{padding:"8px",whiteSpace:"nowrap"}}>{P_ICON[r.platform]} {r.platform}</td>
                      <td style={{padding:"8px"}}><Pill label={r.pillar} color={P_COLOR[r.pillar]}/></td>
                      <td style={{padding:"8px",color:B.green,fontWeight:600}}>{r.reach>0?r.reach.toLocaleString():"—"}</td>
                      <td style={{padding:"8px",color:B.yellow,fontWeight:600}}>{r.eng>0?`${r.eng}%`:"—"}</td>
                      <td style={{padding:"8px",color:B.muted,maxWidth:180,overflow:"hidden",
                        textOverflow:"ellipsis",whiteSpace:"nowrap"}}>{r.hook}</td>
                    </tr>
                  ))}
                </tbody>
              </table>
            </div>
          </Card>
        ):(
          <Card style={{textAlign:"center",padding:32}}>
            <div style={{fontSize:32,marginBottom:10}}>📊</div>
            <div style={{fontSize:13,fontWeight:600,marginBottom:6}}>No published posts yet</div>
            <div style={{fontSize:12,color:B.muted}}>Mark posts as Published in the Calendar to see them here.</div>
          </Card>
        )}
        <BannerAd style={{marginTop:14}}/>
      </div>
    );
  };

  const TipsTab=()=>(
    <div>
      <div style={{background:`${B.lime}11`,border:`1px solid ${B.lime}33`,borderRadius:10,
        padding:12,marginBottom:14,fontSize:11,color:B.muted,lineHeight:1.5}}>
        ✦ Updated with 2026 algorithm changes — what's working right now across every platform
      </div>
      {PLATFORMS.map((p,pi)=>(
        <div key={p}>
          <Card style={{marginBottom:10}}>
            <div style={{fontSize:13,fontWeight:700,marginBottom:10,
              display:"flex",gap:8,alignItems:"center"}}>
              <span>{P_ICON[p]}</span>
              <span>{p}</span>
              <span style={{fontSize:10,color:B.muted,fontWeight:400}}>· 2026</span>
            </div>
            {TIPS_2026[p]?.map((tip,i)=>(
              <div key={i} style={{display:"flex",gap:10,padding:"7px 0",
                borderBottom:`1px solid ${B.border2}`}}>
                <span style={{color:B.lime,fontSize:12,flexShrink:0}}>→</span>
                <span style={{fontSize:12,lineHeight:1.55}}>{tip}</span>
              </div>
            ))}
          </Card>
          {pi===3&&<BannerAd style={{marginBottom:10}}/>}
        </div>
      ))}
    </div>
  );

  const BrainstormTab=()=>(
    <div>
      {/* Hook Library */}
      <Card style={{marginBottom:14}}>
        <div style={{fontSize:13,fontWeight:700,marginBottom:10}}>🎲 Hook Library</div>
        <div style={{fontSize:11,color:B.muted,marginBottom:10}}>
          Click "Use" to drop a hook into the next empty day in your calendar.
        </div>
        {HOOKS.map((h,i)=>(
          <div key={i} style={{display:"flex",justifyContent:"space-between",
            alignItems:"center",padding:"8px 0",
            borderBottom:`1px solid ${B.border2}`,gap:10}}>
            <span style={{fontSize:12,flex:1}}>{h}</span>
            <button onClick={()=>{
              const d=ws.days.find(x=>!x.hook);
              if(d){updDay(d.id,"hook",h);showToast("Hook added ✦");}
              else showToast("All days already have hooks!");
            }}
              style={{background:`${B.lime}18`,border:`1px solid ${B.lime}33`,
                color:B.lime,fontSize:10,fontWeight:700,padding:"3px 10px",
                borderRadius:6,cursor:"pointer",flexShrink:0}}>Use</button>
          </div>
        ))}
      </Card>

      {/* Content Ideas Bank */}
      <Card style={{marginBottom:14}}>
        <div style={{fontSize:13,fontWeight:700,marginBottom:4}}>💡 Content Ideas Bank</div>
        <div style={{fontSize:11,color:B.muted,marginBottom:12}}>
          Ready-made content ideas for EA personal brands. Click to copy.
        </div>
        {CONTENT_IDEAS.map((idea,i)=>(
          <div key={i} style={{background:B.surface2,border:`1px solid ${B.border2}`,
            borderRadius:9,padding:12,marginBottom:8,cursor:"pointer"}}
            onClick={()=>{
              navigator.clipboard?.writeText(idea.idea).catch(()=>{});
              showToast("Idea copied ✦");
            }}
            onMouseEnter={e=>e.currentTarget.style.borderColor=B.pink}
            onMouseLeave={e=>e.currentTarget.style.borderColor=B.border2}>
            <div style={{display:"flex",gap:6,marginBottom:6,flexWrap:"wrap"}}>
              <Pill label={idea.platform} color={B.blue}/>
              <Pill label={idea.format} color={B.lime}/>
              <Pill label={idea.pillar} color={P_COLOR[idea.pillar]||B.purple}/>
            </div>
            <div style={{fontSize:12,fontWeight:600}}>{idea.idea}</div>
          </div>
        ))}
      </Card>

      <div style={{background:`${B.lime}0a`,border:`1px dashed ${B.lime}44`,
        borderRadius:12,padding:14,marginBottom:14,textAlign:"center"}}>
        <div style={{fontSize:13,fontWeight:800,color:B.lime,marginBottom:4}}>
          ✦ AI Brainstorm — Coming Soon
        </div>
        <div style={{fontSize:11,color:B.muted}}>
          One click to generate 8 viral content ideas tailored to your niche. Coming when AI is enabled.
        </div>
      </div>

      <BannerAd/>
    </div>
  );

  const FontsTab=()=>(
    <div>
      <div style={{background:`linear-gradient(135deg,${B.pink}15,${B.lime}08)`,
        border:`1px solid ${B.pink}33`,borderRadius:14,padding:16,marginBottom:14}}>
        <div style={{fontSize:bp.isMobile?14:16,fontWeight:800,marginBottom:4}}>
          🔤 Font Style Generator
        </div>
        <div style={{fontSize:12,color:B.muted,marginBottom:12}}>
          Type your text and preview {FONT_DATA.length} Google Fonts. Click any card to copy the CSS to use in Canva, Instagram bios, or anywhere.
        </div>
        <div style={{display:"flex",gap:8,flexWrap:"wrap",alignItems:"center"}}>
          <input value={fontTxt} onChange={e=>setFontTxt(e.target.value)}
            placeholder="✦ Type your text here…"
            style={{flex:1,minWidth:160,background:B.surface,
              border:`2px solid ${B.border2}`,color:B.text,borderRadius:10,
              padding:"10px 14px",fontSize:18,fontWeight:800,
              boxSizing:"border-box",outline:"none",
              fontFamily:"'Nunito',sans-serif",transition:"border-color .2s"}}
            onFocus={e=>e.target.style.borderColor=B.pink}
            onBlur={e=>e.target.style.borderColor=B.border2}/>
          <div style={{flexShrink:0}}>
            <div style={{fontSize:10,color:B.muted,fontWeight:700,marginBottom:3}}>
              SIZE: {fontSz}px
            </div>
            <input type="range" min={14} max={72} value={fontSz}
              onChange={e=>setFontSz(+e.target.value)}
              style={{width:110,accentColor:B.pink,cursor:"pointer"}}/>
          </div>
        </div>
      </div>

      {/* search */}
      <input value={fontSrch} onChange={e=>setFontSrch(e.target.value)}
        placeholder="✦ Search fonts or categories…"
        style={{width:"100%",background:B.surface2,border:`1.5px solid ${B.border2}`,
          color:B.text,borderRadius:10,padding:"10px 16px",fontSize:13,
          outline:"none",marginBottom:12,boxSizing:"border-box"}}
        onFocus={e=>e.target.style.borderColor=B.pink}
        onBlur={e=>e.target.style.borderColor=B.border2}/>

      {/* category filters */}
      <div style={{display:"flex",gap:6,overflowX:"auto",marginBottom:14,paddingBottom:4}}>
        {FONT_CATS.map(cat=>{
          const cnt=cat==="All"?FONT_DATA.length:FONT_DATA.filter(f=>f.cat===cat).length;
          return(
            <button key={cat} onClick={()=>setFontCat(cat)}
              style={{background:fontCat===cat?B.pink:"transparent",
                border:`1.5px solid ${fontCat===cat?B.pink:B.border2}`,
                color:fontCat===cat?B.black:B.muted,
                fontSize:11,fontWeight:fontCat===cat?800:600,
                padding:"6px 14px",borderRadius:20,cursor:"pointer",
                whiteSpace:"nowrap",flexShrink:0,
                fontFamily:"'Nunito',sans-serif",
                boxShadow:fontCat===cat?`0 0 16px ${B.pink}44`:"none"}}>
              {cat==="All"?`✦ All (${cnt})`:cat}{cat!=="All"&&` (${cnt})`}
            </button>
          );
        })}
      </div>

      <BannerAd style={{marginBottom:14}}/>

      {/* font grid */}
      {filteredFonts.length===0?(
        <div style={{textAlign:"center",padding:"40px 20px",color:B.muted,
          fontSize:12,letterSpacing:2}}>
          No fonts found ✦ try a different search
        </div>
      ):(
        <div style={{display:"grid",
          gridTemplateColumns:bp.isMobile?"1fr":bp.isTablet?"repeat(2,1fr)":"repeat(3,1fr)",
          gap:2}}>
          {filteredFonts.map((font,i)=>{
            const copied=copiedF===i;
            return(
              <div key={i} onClick={()=>copyFont(font,i)}
                style={{background:B.surface,
                  border:`1.5px solid ${copied?B.lime:B.border}`,
                  padding:"22px 20px 14px",cursor:"pointer",
                  position:"relative",overflow:"hidden",borderRadius:2,
                  transition:"all .15s"}}
                onMouseEnter={e=>{
                  e.currentTarget.style.borderColor=B.pink;
                  e.currentTarget.style.transform="translateY(-2px)";
                  e.currentTarget.style.boxShadow=`0 8px 24px ${B.pink}20`;
                }}
                onMouseLeave={e=>{
                  e.currentTarget.style.borderColor=copied?B.lime:B.border;
                  e.currentTarget.style.transform="none";
                  e.currentTarget.style.boxShadow="none";
                }}>
                {/* top accent */}
                <div style={{position:"absolute",top:0,left:0,right:0,height:2,
                  background:`linear-gradient(90deg,${B.pink},${B.lime})`,
                  opacity:copied?1:0,transition:"opacity .2s"}}/>
                {/* preview */}
                <div style={{fontFamily:font.f,fontWeight:font.w,fontStyle:font.s,
                  fontSize:fontSz,color:B.text,lineHeight:1.2,
                  marginBottom:12,wordBreak:"break-word",minHeight:40}}>
                  {fontTxt||"Glimify"}
                </div>
                {/* footer */}
                <div style={{display:"flex",justifyContent:"space-between",gap:6}}>
                  <div>
                    <div style={{fontSize:9,letterSpacing:1.5,textTransform:"uppercase",color:B.muted}}>
                      {font.n}
                    </div>
                    <div style={{fontSize:8,color:B.pink,opacity:.6,marginTop:1}}>
                      ✦ {font.cat}
                    </div>
                  </div>
                  <div style={{fontSize:9,fontWeight:900,letterSpacing:1.5,
                    textTransform:"uppercase",color:B.lime,opacity:.7,whiteSpace:"nowrap"}}>
                    {copied?"✦ Copied!":"Copy ✦"}
                  </div>
                </div>
                {/* copied overlay */}
                {copied&&(
                  <div style={{position:"absolute",inset:0,display:"flex",
                    alignItems:"center",justifyContent:"center",
                    background:"rgba(0,0,0,.88)",fontWeight:900,fontSize:13,
                    letterSpacing:3,textTransform:"uppercase",color:B.lime}}>
                    ✦ Copied!
                  </div>
                )}
              </div>
            );
          })}
        </div>
      )}
    </div>
  );

  /* ── IMAGE TOOLS TAB — Original Glimify Creative Hub ── */
  const ImageToolsTab=()=>{
    const [activeGroup, setActiveGroup] = useState("All");

    const TOOL_GROUPS = ["All","✏️ Edit","🔄 Convert","🎨 Design","⚡ Quick Fix"];

    const tools=[
      /* Edit */
      {group:"✏️ Edit", icon:"✨",name:"Make It Sharp",badge:"🔥 Most Used",badgeColor:B.pink,
        desc:"Upload any blurry photo and watch it transform into a crisp, scroll-stopping visual in one click.",
        tags:["Photos","Feed","Reels"],color:B.pink,
        url:"https://tools.picsart.com/image/sharpen/"},
      {group:"✏️ Edit", icon:"✂️",name:"Smart Crop",badge:null,
        desc:"Crop your image to the perfect ratio for any platform — Stories, Feed, YouTube thumbnail, LinkedIn banner.",
        tags:["Social Media","Multi-platform"],color:B.purple,
        url:"https://tools.picsart.com/image/crop/"},
      {group:"✏️ Edit", icon:"↔️",name:"Resize Without Regrets",badge:"📱 Social Ready",badgeColor:B.blue,
        desc:"Resize to any dimension without stretching or distorting. Your image quality stays pristine.",
        tags:["Feed","Stories","Cover"],color:B.blue,
        url:"https://tools.picsart.com/image/resize/"},
      {group:"✏️ Edit", icon:"🔄",name:"Rotate & Straighten",badge:null,
        desc:"Fix tilted shots instantly. Rotate any direction or straighten a crooked horizon in seconds.",
        tags:["Quick Fix","Photos"],color:B.green,
        url:"https://tools.picsart.com/image/rotate/"},
      {group:"✏️ Edit", icon:"🪄",name:"Mirror Effect",badge:"✨ Trending",badgeColor:B.lime,
        desc:"Create symmetrical, aesthetic mirror images that go viral on Instagram and TikTok feeds.",
        tags:["Aesthetic","Viral","Feed"],color:B.lime,
        url:"https://tools.picsart.com/image/mirror/"},
      /* Design */
      {group:"🎨 Design", icon:"🪞",name:"Glow-Up Your Profile Pic",badge:"⭐ Creator Fav",badgeColor:B.pink,
        desc:"Transform any selfie into a polished, professional profile photo sized perfectly for every platform.",
        tags:["Profile","Branding","Creator"],color:B.pink,
        url:"https://tools.picsart.com/design/profile-picture/"},
      {group:"🎨 Design", icon:"✍️",name:"Text on Photo",badge:null,
        desc:"Drop bold captions, quotes, or CTAs directly onto your visuals. Make every post speak louder.",
        tags:["Captions","Quotes","Branding"],color:B.orange,
        url:"https://tools.picsart.com/text/add-text-to-photo/"},
      {group:"🎨 Design", icon:"🎭",name:"Palette Extractor",badge:"✦ New",badgeColor:B.lime,
        desc:"Upload any image and instantly extract its full colour palette. Match your brand to any aesthetic.",
        tags:["Branding","Colour","Design"],color:B.purple,
        url:"https://tools.picsart.com/color/palette-from-image/"},
      /* Convert */
      {group:"🔄 Convert", icon:"⚡",name:"Compress to Post-Ready",badge:"⚡ Instant",badgeColor:B.yellow,
        desc:"Shrink file sizes without visible quality loss. Upload faster, load faster, rank better.",
        tags:["SEO","Speed","Website"],color:B.yellow,
        url:"https://tools.picsart.com/image/compress/"},
      {group:"🔄 Convert", icon:"📸",name:"HEIC → JPG",badge:null,
        desc:"iPhone photos in HEIC? Convert them instantly to JPG so you can use them anywhere.",
        tags:["iPhone","Convert"],color:B.blue,
        url:"https://tools.picsart.com/convert/heic-to-jpg/"},
      {group:"🔄 Convert", icon:"🖼️",name:"JPG ↔ PNG",badge:null,
        desc:"Switch between JPG and PNG in one click. Keep transparency, lose nothing.",
        tags:["Format","Convert"],color:B.green,
        url:"https://tools.picsart.com/convert/jpg-to-png/"},
      {group:"🔄 Convert", icon:"🎨",name:"PNG → SVG",badge:null,
        desc:"Turn raster images into scalable vector graphics. Perfect for logos and graphics that need to scale.",
        tags:["Vectors","Logo","Design"],color:B.purple,
        url:"https://tools.picsart.com/convert/png-to-svg/"},
      {group:"🔄 Convert", icon:"🔁",name:"SVG → PNG",badge:null,
        desc:"Export your SVG vectors as sharp PNG files, ready for any social platform or document.",
        tags:["Export","Social"],color:B.pink,
        url:"https://tools.picsart.com/convert/svg-to-png/"},
      /* Quick Fix */
      {group:"⚡ Quick Fix", icon:"💾",name:"PNG → JPG",badge:null,
        desc:"Need a smaller file fast? Convert PNGs to JPG without signing up or downloading anything.",
        tags:["Fast","Convert"],color:B.orange,
        url:"https://tools.picsart.com/convert/png-to-jpg/"},
    ];

    const filtered = activeGroup==="All" ? tools : tools.filter(t=>t.group===activeGroup);
    const cols = bp.isMobile?"1fr":bp.isTablet?"repeat(2,1fr)":"repeat(3,1fr)";

    return(
      <div>
        {/* HERO */}
        <div style={{position:"relative",overflow:"hidden",
          background:`linear-gradient(135deg,${B.surface} 0%,${B.surface2} 100%)`,
          border:`1px solid ${B.border2}`,borderRadius:18,
          padding:bp.isMobile?"20px 16px":"28px 28px",marginBottom:18}}>
          {/* deco bg sparks */}
          {["top:10px;right:24px","bottom:14px;right:80px","top:50%;right:140px"].map((pos,i)=>(
            <div key={i} style={{position:"absolute",...Object.fromEntries(pos.split(";").map(s=>s.split(":"))),
              fontSize:[28,18,14][i],opacity:.08,pointerEvents:"none"}}>✦</div>
          ))}
          <div style={{display:"inline-flex",alignItems:"center",gap:6,
            background:`${B.pink}22`,border:`1px solid ${B.pink}44`,
            padding:"4px 14px",borderRadius:20,marginBottom:14}}>
            <span style={{fontSize:9,fontWeight:900,letterSpacing:3,
              textTransform:"uppercase",color:B.pink}}>✦ Glimify Creator Tools</span>
          </div>
          <div style={{fontSize:bp.isMobile?20:28,fontWeight:900,lineHeight:1.2,marginBottom:10}}>
            Make images that{" "}
            <span style={{background:`linear-gradient(90deg,${B.pink},${B.lime},${B.purple})`,
              WebkitBackgroundClip:"text",WebkitTextFillColor:"transparent"}}>
              stop the scroll.
            </span>
          </div>
          <div style={{fontSize:13,color:B.muted,lineHeight:1.7,marginBottom:16,maxWidth:520}}>
            14 free, professional-grade creative tools built for content creators, EAs, and small brands who need results — not a learning curve.
          </div>
          <div style={{display:"flex",gap:8,flexWrap:"wrap"}}>
            {[["⚡","Instant Results"],["🔒","No Sign Up Ever"],["💸","100% Free"],["📱","Any Device"],["🚫","No Storage Needed"]].map(([ic,lb])=>(
              <div key={lb} style={{display:"flex",alignItems:"center",gap:5,
                background:B.surface3,border:`1px solid ${B.border2}`,
                padding:"6px 13px",borderRadius:30,fontSize:11,fontWeight:600,color:B.text}}>
                <span>{ic}</span><span>{lb}</span>
              </div>
            ))}
          </div>
        </div>

        {/* GROUP FILTERS */}
        <div style={{display:"flex",gap:6,overflowX:"auto",marginBottom:14,paddingBottom:4}}>
          {TOOL_GROUPS.map(g=>(
            <button key={g} onClick={()=>setActiveGroup(g)}
              style={{background:activeGroup===g?B.pink:"transparent",
                border:`1.5px solid ${activeGroup===g?B.pink:B.border2}`,
                color:activeGroup===g?B.black:B.muted,
                fontSize:11,fontWeight:activeGroup===g?800:600,
                padding:"7px 16px",borderRadius:20,cursor:"pointer",
                whiteSpace:"nowrap",flexShrink:0,
                fontFamily:"'Nunito',sans-serif",
                boxShadow:activeGroup===g?`0 0 18px ${B.pink}44`:"none",
                transition:"all .15s"}}>
              {g} {activeGroup!==g&&<span style={{opacity:.5}}>({g==="All"?tools.length:tools.filter(t=>t.group===g).length})</span>}
            </button>
          ))}
        </div>

        <BannerAd style={{marginBottom:14}}/>

        {/* TOOL CARDS */}
        <div style={{display:"grid",gridTemplateColumns:cols,gap:10,marginBottom:20}}>
          {filtered.map((t,i)=>(
            <a key={i} href={t.url} target="_blank" rel="noreferrer"
              style={{display:"flex",flexDirection:"column",background:B.surface,
                border:`1.5px solid ${B.border}`,borderRadius:14,padding:18,
                textDecoration:"none",color:B.text,position:"relative",
                overflow:"hidden",transition:"all .2s"}}
              onMouseEnter={e=>{
                e.currentTarget.style.borderColor=t.color;
                e.currentTarget.style.transform="translateY(-4px)";
                e.currentTarget.style.boxShadow=`0 14px 36px ${t.color}28`;
                e.currentTarget.style.background=B.surface2;
              }}
              onMouseLeave={e=>{
                e.currentTarget.style.borderColor=B.border;
                e.currentTarget.style.transform="none";
                e.currentTarget.style.boxShadow="none";
                e.currentTarget.style.background=B.surface;
              }}>
              {/* colour top bar */}
              <div style={{position:"absolute",top:0,left:0,right:0,height:3,
                background:`linear-gradient(90deg,${t.color},${t.color}88)`}}/>
              {/* badge */}
              {t.badge&&(
                <div style={{position:"absolute",top:12,right:12,
                  background:`${t.badgeColor||t.color}22`,
                  border:`1px solid ${t.badgeColor||t.color}44`,
                  color:t.badgeColor||t.color,fontSize:9,fontWeight:800,
                  padding:"2px 9px",borderRadius:20,letterSpacing:.5}}>
                  {t.badge}
                </div>
              )}
              {/* icon */}
              <div style={{width:46,height:46,borderRadius:14,
                background:`${t.color}18`,border:`1.5px solid ${t.color}33`,
                display:"flex",alignItems:"center",justifyContent:"center",
                fontSize:22,marginBottom:12}}>
                {t.icon}
              </div>
              <div style={{fontSize:14,fontWeight:800,marginBottom:6,
                paddingRight:t.badge?70:0,lineHeight:1.2}}>{t.name}</div>
              <div style={{fontSize:12,color:B.muted,lineHeight:1.6,
                marginBottom:12,flex:1}}>{t.desc}</div>
              {/* tags */}
              <div style={{display:"flex",gap:5,flexWrap:"wrap",marginBottom:12}}>
                {t.tags.map(tag=>(
                  <span key={tag} style={{fontSize:9,fontWeight:700,
                    background:`${t.color}18`,color:t.color,
                    padding:"2px 8px",borderRadius:20,border:`1px solid ${t.color}33`}}>
                    {tag}
                  </span>
                ))}
              </div>
              {/* CTA */}
              <div style={{display:"flex",alignItems:"center",gap:5,
                fontSize:11,fontWeight:800,color:t.color,
                letterSpacing:.5,textTransform:"uppercase"}}>
                <span>Open Free Tool</span>
                <span style={{fontSize:14}}>→</span>
              </div>
            </a>
          ))}
        </div>

        {/* BOTTOM BANNER — original Glimify copy */}
        <div style={{background:`linear-gradient(135deg,${B.pink}14,${B.lime}09,${B.purple}0c)`,
          border:`1.5px solid ${B.border2}`,borderRadius:18,
          padding:bp.isMobile?"20px 16px":"32px 28px",
          textAlign:"center",marginBottom:14,position:"relative",overflow:"hidden"}}>
          <div style={{position:"absolute",top:12,left:20,fontSize:32,opacity:.05}}>✦</div>
          <div style={{position:"absolute",bottom:12,right:24,fontSize:22,opacity:.06}}>✦</div>
          <div style={{fontSize:bp.isMobile?18:24,fontWeight:900,marginBottom:8,lineHeight:1.2}}>
            All tools.{" "}
            <span style={{color:B.pink}}>Zero cost.</span>{" "}
            <span style={{color:B.lime}}>Total glow-up.</span>
          </div>
          <div style={{fontSize:13,color:B.muted,marginBottom:20,
            lineHeight:1.7,maxWidth:460,margin:"0 auto 20px"}}>
            No account. No watermark. No storage. No nonsense. Just you, your content, and tools that actually work.
          </div>
          <div style={{display:"flex",gap:8,justifyContent:"center",flexWrap:"wrap"}}>
            {[
              {icon:"⚡",label:"Instant Results"},
              {icon:"🔒",label:"Private & Secure"},
              {icon:"✨",label:"Pro Quality"},
              {icon:"📱",label:"Any Device"},
              {icon:"🎨",label:"Creator-Made"},
              {icon:"💸",label:"Always Free"},
            ].map(p=>(
              <div key={p.label} style={{display:"flex",alignItems:"center",gap:6,
                background:B.surface,border:`1.5px solid ${B.border2}`,
                color:B.text,fontSize:12,fontWeight:700,
                padding:"8px 16px",borderRadius:30,transition:"border-color .15s"}}
                onMouseEnter={e=>e.currentTarget.style.borderColor=B.pink}
                onMouseLeave={e=>e.currentTarget.style.borderColor=B.border2}>
                <span>{p.icon}</span><span>{p.label}</span>
              </div>
            ))}
          </div>
        </div>

        <BannerAd/>
      </div>
    );
  };

  /* ── ABOUT TAB ── */
  const AboutTab=()=>(
    <div>
      {/* hero — Athena's story */}
      <div style={{background:`linear-gradient(135deg,${B.pink}18,${B.lime}08)`,
        border:`1px solid ${B.pink}33`,borderRadius:16,
        padding:bp.isMobile?"20px 16px":"28px 28px",marginBottom:16,
        position:"relative",overflow:"hidden"}}>
        {/* sparkle deco */}
        <div style={{position:"absolute",top:16,right:20,fontSize:bp.isMobile?28:40,opacity:.15}}>✦</div>
        <div style={{position:"absolute",bottom:16,right:60,fontSize:20,opacity:.1}}>✦</div>
        <div style={{display:"inline-flex",alignItems:"center",gap:6,
          background:`${B.pink}22`,border:`1px solid ${B.pink}33`,
          padding:"4px 14px",borderRadius:20,marginBottom:14}}>
          <span style={{fontSize:9,fontWeight:800,letterSpacing:3,
            textTransform:"uppercase",color:B.pink}}>✦ Our Story</span>
        </div>
        <div style={{fontSize:bp.isMobile?22:30,fontWeight:900,lineHeight:1.2,marginBottom:14}}>
          Who is Behind{" "}
          <span style={{background:`linear-gradient(90deg,${B.pink},${B.lime})`,
            WebkitBackgroundClip:"text",WebkitTextFillColor:"transparent"}}>
            Glimify?
          </span>
        </div>
        <div style={{fontSize:bp.isMobile?13:15,color:B.muted,lineHeight:1.8,marginBottom:14,maxWidth:640}}>
          Behind Glimify is <strong style={{color:B.text}}>Athena</strong> — a mom of two, a graphic designer, a Social Media Manager, and an Executive Assistant who built something from nothing but ideas, grit, and very little sleep.
        </div>
        <div style={{fontSize:bp.isMobile?13:15,color:B.muted,lineHeight:1.8,marginBottom:14,maxWidth:640}}>
          Glimify was born in <strong style={{color:B.lime}}>2026</strong>, not from a big budget or a fancy office, but from a woman who stayed up past midnight with a mind full of ideas and a heart full of purpose. While juggling debt, family, and a full hustle alongside her husband, Athena did what she always does: she <strong style={{color:B.pink}}>created</strong>.
        </div>
        <div style={{fontSize:bp.isMobile?13:15,color:B.muted,lineHeight:1.8,maxWidth:640}}>
          They call her the <strong style={{color:B.lime}}>Goddess of Fire and Wisdom</strong>, and those who know her understand why. She doesn't wait for the right moment. She builds the moment.
        </div>
        <div style={{marginTop:18,display:"flex",alignItems:"center",gap:10,
          background:B.surface2,borderRadius:12,padding:"12px 16px",
          border:`1px solid ${B.border2}`,maxWidth:500}}>
          <span style={{fontSize:30}}>🔥</span>
          <div style={{fontSize:13,color:B.text,fontStyle:"italic",lineHeight:1.6}}>
            "Glimify is her proof that creativity doesn't need capital. It needs courage."
          </div>
        </div>
      </div>

      {/* mission */}
      <div style={{background:B.surface,border:`1px solid ${B.border2}`,
        borderTop:`2px solid ${B.lime}`,borderRadius:12,padding:20,marginBottom:14}}>
        <div style={{fontSize:11,color:B.lime,fontWeight:700,letterSpacing:2,
          textTransform:"uppercase",marginBottom:10}}>✦ Mission Statement</div>
        <div style={{fontSize:bp.isMobile?17:22,fontWeight:900,lineHeight:1.3,marginBottom:10}}>
          Glimify exists to help{" "}
          <span style={{color:B.pink}}>small brands</span> and{" "}
          <span style={{color:B.lime}}>big dreamers</span> shine.
        </div>
        <div style={{fontSize:13,color:B.muted,lineHeight:1.7}}>
          Built by a hustler, for hustlers. Every tool, every feature, every font — made with creators in mind.
        </div>
      </div>

      {/* what glimify is */}
      <div style={{display:"grid",gridTemplateColumns:bp.isMobile?"1fr":"repeat(3,1fr)",gap:10,marginBottom:14}}>
        {[
          {icon:"🗓️",title:"Content Calendar",desc:"Plan 30 days of content across all your platforms — organized, trackable, and always ready."},
          {icon:"🔤",title:"Font Studio",desc:"242 Google Fonts, live preview, one-click copy. Your brand deserves to look incredible."},
          {icon:"🖼️",title:"Image Tools",desc:"14 free professional image tools. Edit, convert, compress, mirror — no sign-up ever."},
          {icon:"💡",title:"Tips 2026",desc:"Real, updated strategies for Instagram, Reels, TikTok, Threads, YouTube and more."},
          {icon:"⚡",title:"Brainstorm Engine",desc:"A hook library and content idea bank built specifically for EA and creator brands."},
          {icon:"📊",title:"Analytics & Reports",desc:"Track your content performance with a monthly review system that actually makes sense."},
        ].map((c,i)=>(
          <div key={i} style={{background:B.surface,border:`1px solid ${B.border2}`,
            borderRadius:12,padding:16,position:"relative",overflow:"hidden"}}>
            <div style={{position:"absolute",top:0,left:0,right:0,height:2,
              background:`linear-gradient(90deg,${B.pink},${B.lime})`}}/>
            <div style={{fontSize:24,marginBottom:8}}>{c.icon}</div>
            <div style={{fontSize:13,fontWeight:700,marginBottom:4}}>{c.title}</div>
            <div style={{fontSize:11,color:B.muted,lineHeight:1.55}}>{c.desc}</div>
          </div>
        ))}
      </div>

      {/* why free */}
      <div style={{background:B.surface,border:`1px solid ${B.border2}`,
        borderTop:`2px solid ${B.pink}`,borderRadius:12,padding:20,marginBottom:14}}>
        <div style={{fontSize:11,color:B.pink,fontWeight:700,letterSpacing:2,
          textTransform:"uppercase",marginBottom:8}}>✦ Why is Glimify Free?</div>
        <div style={{fontSize:13,color:B.muted,lineHeight:1.8}}>
          Glimify is free because creativity should have no paywall. We're supported by non-intrusive ads that let us keep the lights on and keep building. When you watch the ad, you're directly helping Athena keep Glimify alive and growing. Thank you for that.
        </div>
      </div>

      {/* contact */}
      <div style={{background:`linear-gradient(135deg,${B.pink}10,${B.lime}06)`,
        border:`1px solid ${B.pink}33`,borderRadius:14,padding:20,marginBottom:14}}>
        <div style={{fontSize:14,fontWeight:800,marginBottom:6}}>✉️ Get in Touch</div>
        <div style={{fontSize:12,color:B.muted,marginBottom:14,lineHeight:1.6}}>
          Have a question, a feature idea, want to advertise on Glimify, or just want to say hi to Athena? We'd genuinely love to hear from you.
        </div>
        <a href="mailto:glimify.io@gmail.com"
          style={{display:"inline-flex",alignItems:"center",gap:10,
            background:B.surface,border:`1px solid ${B.border2}`,borderRadius:10,
            padding:"12px 20px",color:B.text,textDecoration:"none",fontSize:13,
            fontWeight:600,transition:"border-color .2s"}}
          onMouseEnter={e=>e.currentTarget.style.borderColor=B.pink}
          onMouseLeave={e=>e.currentTarget.style.borderColor=B.border2}>
          <span style={{fontSize:18}}>✉️</span>
          <div>
            <div style={{fontWeight:700}}>glimify.io@gmail.com</div>
            <div style={{fontSize:10,color:B.muted,marginTop:1}}>We reply within 24–48 hours</div>
          </div>
        </a>
      </div>

      <BannerAd/>
    </div>
  );

  const TAB_MAP = {
    calendar:<CalendarTab/>,analytics:<AnalyticsTab/>,
    report:<ReportTab/>,tips:<TipsTab/>,
    brainstorm:<BrainstormTab/>,fonts:<FontsTab/>,
    imagetools:<ImageToolsTab/>,about:<AboutTab/>,
  };

  /* ── WORKSPACE LIST ── */
  const WsList=({collapsed=false})=>(
    <>
      {workspaces.map(w=>(
        <div key={w.id} style={{display:"flex",alignItems:"center",gap:4,marginBottom:2}}>
          <button onClick={()=>{setWsId(w.id);setSelDay(null);}}
            style={{flex:1,display:"flex",alignItems:"center",gap:8,
              padding:"7px 10px",borderRadius:8,border:"none",cursor:"pointer",
              background:wsId===w.id?`${w.color}18`:"transparent",
              color:wsId===w.id?w.color:B.muted,
              fontWeight:wsId===w.id?700:400,fontSize:12,
              textAlign:"left",minWidth:0,fontFamily:"'Nunito',sans-serif"}}>
            <span style={{fontSize:13,flexShrink:0}}>{w.emoji}</span>
            {!collapsed&&(
              <span style={{overflow:"hidden",textOverflow:"ellipsis",whiteSpace:"nowrap"}}>
                {w.name}
              </span>
            )}
          </button>
          {!collapsed&&workspaces.length>1&&(
            <button onClick={()=>setDelConfirm(w.id)} title="Delete workspace"
              style={{background:"none",border:"none",color:B.muted,
                cursor:"pointer",padding:"4px 6px",borderRadius:6,
                fontSize:11,flexShrink:0}}
              onMouseEnter={e=>e.currentTarget.style.color=B.red}
              onMouseLeave={e=>e.currentTarget.style.color=B.muted}>✕</button>
          )}
        </div>
      ))}
      {!collapsed&&(
        <>
          <button onClick={()=>setNewWsOpen(true)}
            style={{width:"100%",display:"flex",alignItems:"center",gap:8,
              padding:"6px 10px",borderRadius:8,border:`1px dashed ${B.border2}`,
              cursor:"pointer",background:"transparent",color:B.muted,
              fontSize:12,marginTop:4,fontFamily:"'Nunito',sans-serif"}}>
            <span>+</span><span>New Workspace</span>
          </button>
          {/* privacy note */}
          <div style={{display:"flex",alignItems:"flex-start",gap:5,
            marginTop:8,padding:"6px 8px",
            background:`${B.green}0a`,border:`1px solid ${B.green}22`,
            borderRadius:8}}>
            <span style={{fontSize:11,color:B.green,flexShrink:0}}>🔒</span>
            <span style={{fontSize:9,color:B.muted,lineHeight:1.5}}>
              Your workspaces are private and stored only on your device. No one else can see your content.
            </span>
          </div>
        </>
      )}
    </>
  );

  /* ── FOOTER ── */
  const Footer=()=>(
    <footer id="glimify-support-footer" style={{borderTop:`1px solid ${B.border2}`,
      padding:bp.isMobile?"24px 16px":"36px 36px",
      background:B.surface,marginTop:32}}>
      <div style={{maxWidth:860,margin:"0 auto"}}>

        {/* ── SUPPORT THE CREATOR ── */}
        <div style={{background:`linear-gradient(135deg,${B.pink}14,${B.lime}09,${B.purple}0c)`,
          border:`1.5px solid ${B.pink}33`,borderRadius:16,
          padding:bp.isMobile?"20px 16px":"24px 28px",
          marginBottom:28,position:"relative",overflow:"hidden"}}>
          <div style={{position:"absolute",top:10,right:16,fontSize:28,opacity:.07}}>☕</div>
          <div style={{position:"absolute",bottom:10,right:56,fontSize:18,opacity:.05}}>✦</div>
          <div style={{display:"flex",gap:bp.isMobile?14:20,
            flexWrap:bp.isMobile?"wrap":"nowrap",alignItems:"flex-start"}}>
            {/* left copy */}
            <div style={{flex:1,minWidth:0}}>
              <div style={{display:"inline-flex",alignItems:"center",gap:6,
                background:`${B.pink}22`,border:`1px solid ${B.pink}33`,
                padding:"3px 12px",borderRadius:20,marginBottom:10}}>
                <span style={{fontSize:9,fontWeight:800,letterSpacing:2,
                  textTransform:"uppercase",color:B.pink}}>Support the Creator</span>
              </div>
              <div style={{fontSize:bp.isMobile?15:18,fontWeight:900,
                lineHeight:1.3,marginBottom:10}}>
                ❤️ This tool is{" "}
                <span style={{color:B.lime}}>free to use.</span>
              </div>
              <div style={{fontSize:12,color:B.muted,lineHeight:1.8,marginBottom:14}}>
                Athena built Glimify from scratch — late nights, zero budget, and a lot of love for creators like you. If this tool has saved you time or helped your content, consider supporting its future. Your tip keeps the project alive and improving.
              </div>
              <div style={{fontSize:12,color:B.muted,lineHeight:1.7,
                marginBottom:14,fontStyle:"italic",
                borderLeft:`2px solid ${B.pink}`,paddingLeft:12}}>
                "This tool will always remain free. If it has helped you, a small tip means the world to a solo creator building in the dark."
              </div>
              <div style={{display:"flex",gap:8,flexWrap:"wrap"}}>
                <div style={{display:"flex",alignItems:"center",gap:6,
                  background:B.surface2,border:`1px solid ${B.border2}`,
                  borderRadius:8,padding:"7px 12px",fontSize:11,color:B.text}}>
                  <span>💳</span><span>GCash · Maya · PayPal</span>
                </div>
                <div style={{display:"flex",alignItems:"center",gap:6,
                  background:B.surface2,border:`1px solid ${B.border2}`,
                  borderRadius:8,padding:"7px 12px",fontSize:11,color:B.muted}}>
                  <span>🔒</span><span>100% Voluntary · No pressure</span>
                </div>
              </div>
            </div>

            {/* QR code box */}
            <div style={{flexShrink:0,textAlign:"center",
              width:bp.isMobile?"100%":"auto"}}>
              <div style={{background:B.surface2,border:`1.5px solid ${B.border2}`,
                borderRadius:14,padding:16,display:"inline-block",
                minWidth:140}}>
                {/* QR placeholder — replace with your real QR image */}
                <div style={{width:120,height:120,background:"#fff",
                  borderRadius:8,margin:"0 auto 10px",
                  display:"flex",alignItems:"center",justifyContent:"center",
                  flexDirection:"column",gap:4}}>
                  {/* Pixelated QR art pattern using divs */}
                  <svg width="100" height="100" viewBox="0 0 21 21" style={{imageRendering:"pixelated"}}>
                    {/* QR code corners + placeholder pattern */}
                    <rect width="21" height="21" fill="white"/>
                    {/* top-left corner */}
                    <rect x="1" y="1" width="7" height="7" fill="none" stroke="#000" strokeWidth=".8"/>
                    <rect x="3" y="3" width="3" height="3" fill="#000"/>
                    {/* top-right corner */}
                    <rect x="13" y="1" width="7" height="7" fill="none" stroke="#000" strokeWidth=".8"/>
                    <rect x="15" y="3" width="3" height="3" fill="#000"/>
                    {/* bottom-left corner */}
                    <rect x="1" y="13" width="7" height="7" fill="none" stroke="#000" strokeWidth=".8"/>
                    <rect x="3" y="15" width="3" height="3" fill="#000"/>
                    {/* center data pattern */}
                    {[[9,1],[10,1],[11,1],[9,3],[11,3],[10,5],[9,7],[11,7],
                      [1,9],[3,9],[5,9],[7,9],[9,9],[11,9],[13,9],[15,9],[17,9],[19,9],
                      [9,11],[10,11],[9,13],[11,13],[13,13],[15,13],[13,15],[15,15],[17,15],
                      [13,17],[17,17],[13,19],[14,19],[15,19]].map(([x,y],i)=>(
                      <rect key={i} x={x} y={y} width="1" height="1" fill="#000"/>
                    ))}
                  </svg>
                  <div style={{fontSize:8,color:"#999",letterSpacing:.5}}>
                    Replace with your QR
                  </div>
                </div>
                <div style={{fontSize:11,fontWeight:800,color:B.pink,marginBottom:2}}>
                  ☕ Buy Me a Coffee
                </div>
                <div style={{fontSize:9,color:B.muted,lineHeight:1.4}}>
                  Scan to support Athena<br/>& keep Glimify free
                </div>
              </div>
              <div style={{fontSize:9,color:B.muted,marginTop:8}}>
                GCash · Maya · PayPal · Any amount
              </div>
            </div>
          </div>
        </div>

        {/* ── MAIN FOOTER LINKS ── */}
        <div style={{display:"flex",gap:20,flexWrap:"wrap",
          justifyContent:"space-between",alignItems:"flex-start",marginBottom:20}}>
          {/* brand */}
          <div>
            <div style={{display:"flex",alignItems:"center",gap:10,marginBottom:6}}>
              <Logo size={32}/>
              <div>
                <LogoWord size={17}/>
                <div style={{fontSize:9,color:B.muted,letterSpacing:2,marginTop:2}}>
                  Content OS · Free
                </div>
              </div>
            </div>
            <div style={{fontSize:12,color:B.muted,lineHeight:1.6,maxWidth:220}}>
              Your all-in-one content calendar, font studio, and creator tools. 100% free, supported by ads and lovely humans like you.
            </div>
          </div>

          {/* contact */}
          <div>
            <div style={{fontSize:11,color:B.muted,fontWeight:700,letterSpacing:1,
              textTransform:"uppercase",marginBottom:10}}>Contact</div>
            <a href="mailto:glimify.io@gmail.com"
              style={{display:"flex",alignItems:"center",gap:8,color:B.text,
                textDecoration:"none",background:B.surface2,
                border:`1px solid ${B.border2}`,borderRadius:8,
                padding:"8px 14px",fontSize:12,marginBottom:6,
                transition:"border-color .2s"}}
              onMouseEnter={e=>e.currentTarget.style.borderColor=B.pink}
              onMouseLeave={e=>e.currentTarget.style.borderColor=B.border2}>
              <span>✉️</span><span>glimify.io@gmail.com</span>
            </a>
            <div style={{fontSize:10,color:B.muted,lineHeight:1.6}}>
              Questions, feature ideas, collabs,<br/>or advertising? We'd love to hear from you.
            </div>
          </div>

          {/* nav */}
          <div>
            <div style={{fontSize:11,color:B.muted,fontWeight:700,letterSpacing:1,
              textTransform:"uppercase",marginBottom:10}}>Navigate</div>
            {TABS.map(t=>(
              <button key={t.id} onClick={()=>setTab(t.id)}
                style={{display:"block",background:"none",border:"none",
                  color:B.muted,fontSize:12,cursor:"pointer",
                  padding:"3px 0",fontFamily:"'Nunito',sans-serif",
                  transition:"color .15s"}}
                onMouseEnter={e=>e.currentTarget.style.color=B.pink}
                onMouseLeave={e=>e.currentTarget.style.color=B.muted}>
                {t.icon} {t.label}
              </button>
            ))}
          </div>
        </div>

        {/* bottom bar */}
        <div style={{borderTop:`1px solid ${B.border2}`,paddingTop:14,
          display:"flex",justifyContent:"space-between",
          alignItems:"center",flexWrap:"wrap",gap:8}}>
          <div style={{fontSize:11,color:B.muted}}>
            © {new Date().getFullYear()} Glimify · Built by Athena · All rights reserved
          </div>
          <div style={{fontSize:11,color:B.muted,display:"flex",gap:4,alignItems:"center"}}>
            Made with <span style={{color:B.pink,fontSize:13}}>♥</span> for creators
          </div>
        </div>
      </div>
    </footer>
  );

  /* ── MODALS ── */
  const NewWsModal=()=>(
    <div onClick={()=>setNewWsOpen(false)}
      style={{position:"fixed",inset:0,background:"rgba(0,0,0,.85)",
        zIndex:200,display:"flex",alignItems:"center",justifyContent:"center",padding:20}}>
      <div onClick={e=>e.stopPropagation()}
        style={{background:B.surface,border:`1px solid ${B.border2}`,
          borderRadius:16,padding:24,width:"100%",maxWidth:400}}>
        <div style={{fontSize:16,fontWeight:800,marginBottom:16}}>✦ New Workspace</div>
        <Lbl>WORKSPACE NAME</Lbl>
        <FInput value={newWsName} onChange={e=>setNwName(e.target.value)}
          placeholder="e.g. Client — Brand Name" style={{marginBottom:12}}/>
        <Lbl>EMOJI ICON</Lbl>
        <div style={{display:"flex",gap:6,marginBottom:12,flexWrap:"wrap"}}>
          {["✦","🏢","🎯","💼","🌟","🚀","🎨","💡","📱","🔥"].map(em=>(
            <button key={em} onClick={()=>setNwEmoji(em)}
              style={{background:newWsEmoji===em?`${B.pink}22`:"transparent",
                border:`1px solid ${newWsEmoji===em?B.pink:B.border2}`,
                borderRadius:8,width:36,height:36,fontSize:17,cursor:"pointer"}}>
              {em}
            </button>
          ))}
        </div>
        <Lbl>ACCENT COLOR</Lbl>
        <div style={{display:"flex",gap:8,marginBottom:20}}>
          {[B.lime,B.pink,B.blue,B.purple,B.green,B.orange,B.yellow].map(c=>(
            <button key={c} onClick={()=>setNwColor(c)}
              style={{width:26,height:26,borderRadius:"50%",background:c,
                border:`2px solid ${newWsColor===c?"#fff":"transparent"}`,
                cursor:"pointer"}}/>
          ))}
        </div>
        <div style={{display:"flex",gap:8}}>
          <button onClick={()=>setNewWsOpen(false)}
            style={{flex:1,background:"transparent",border:`1px solid ${B.border2}`,
              color:B.muted,borderRadius:8,padding:"10px",fontSize:12,cursor:"pointer"}}>
            Cancel
          </button>
          <button onClick={addWs} disabled={!newWsName.trim()}
            style={{flex:2,background:`linear-gradient(90deg,${B.pink},${B.lime})`,
              border:"none",color:B.black,fontWeight:800,borderRadius:8,
              padding:"10px",fontSize:13,cursor:"pointer",
              opacity:newWsName.trim()?1:.4,fontFamily:"'Nunito',sans-serif"}}>
            Create Workspace
          </button>
        </div>
      </div>
    </div>
  );

  const DelModal=()=>{
    const t=workspaces.find(w=>w.id===delConfirm);
    if(!t)return null;
    return(
      <div onClick={()=>setDelConfirm(null)}
        style={{position:"fixed",inset:0,background:"rgba(0,0,0,.88)",
          zIndex:300,display:"flex",alignItems:"center",justifyContent:"center",padding:20}}>
        <div onClick={e=>e.stopPropagation()}
          style={{background:B.surface,border:`1px solid ${B.red}44`,
            borderRadius:16,padding:28,width:"100%",maxWidth:380,textAlign:"center"}}>
          <div style={{fontSize:36,marginBottom:12}}>⚠️</div>
          <div style={{fontSize:16,fontWeight:800,marginBottom:8}}>Delete Workspace?</div>
          <div style={{fontSize:13,color:B.muted,marginBottom:24,lineHeight:1.6}}>
            You're about to permanently delete{" "}
            <strong style={{color:B.text}}>{t.emoji} {t.name}</strong> and all{" "}
            <strong style={{color:B.text}}>{t.days?.length} days</strong> of content.
            This cannot be undone.
          </div>
          <div style={{display:"flex",gap:10}}>
            <button onClick={()=>setDelConfirm(null)}
              style={{flex:1,background:"transparent",border:`1px solid ${B.border2}`,
                color:B.muted,borderRadius:8,padding:"11px",fontSize:13,cursor:"pointer"}}>
              Cancel
            </button>
            <button onClick={()=>deleteWs(delConfirm)}
              style={{flex:1,background:B.red,border:"none",color:"#fff",
                fontWeight:800,borderRadius:8,padding:"11px",fontSize:13,cursor:"pointer"}}>
              Delete
            </button>
          </div>
        </div>
      </div>
    );
  };

  /* ── ConnModal removed — integrations coming in future update ── */

  /* ── LAYOUT ── */
  const StatsStrip=()=>(
    <div style={{display:"grid",
      gridTemplateColumns:bp.isMobile?"repeat(2,1fr)":"repeat(4,1fr)",
      gap:8,marginBottom:16}}>
      {[
        {l:"Days in Month",v:ws.days.length,c:B.lime},
        {l:"Published",v:published.length,c:B.pink},
        {l:"Avg Engagement",v:`${avgEng}%`,c:B.purple},
        {l:"Top Reach",v:topReach>0?`${(topReach/1000).toFixed(1)}K`:"—",c:B.blue},
      ].map(s=>(
        <div key={s.l} style={{background:B.surface,border:`1px solid ${B.border}`,
          borderTop:`2px solid ${s.c}`,borderRadius:10,
          padding:bp.isMobile?"10px 12px":"12px 14px"}}>
          <div style={{fontSize:bp.isMobile?18:20,fontWeight:800,color:s.c,lineHeight:1}}>
            {s.v}
          </div>
          <div style={{fontSize:10,color:B.muted,marginTop:3}}>{s.l}</div>
        </div>
      ))}
    </div>
  );

  const Sidebar=()=>(
    <div style={{width:220,flexShrink:0,display:"flex",flexDirection:"column",
      background:B.surface,borderRight:`1px solid ${B.border2}`,
      height:"100vh",position:"sticky",top:0,overflowY:"auto"}}>
      <div style={{padding:"18px 16px 12px",borderBottom:`2px solid ${B.pink}`,
        display:"flex",alignItems:"center",gap:10}}>
        <Logo size={34}/>
        <div>
          <LogoWord size={17}/>
          <div style={{fontSize:9,color:B.muted,letterSpacing:2,marginTop:2}}>Content OS</div>
        </div>
      </div>
      <nav style={{padding:"8px 8px 0"}}>
        {TABS.map(t=>(
          <button key={t.id} onClick={()=>setTab(t.id)}
            style={{width:"100%",display:"flex",alignItems:"center",gap:10,
              padding:"9px 10px",borderRadius:8,border:"none",cursor:"pointer",
              marginBottom:2,
              background:tab===t.id?`${ws.color||B.lime}18`:"transparent",
              color:tab===t.id?ws.color||B.lime:B.muted,
              fontWeight:tab===t.id?700:400,fontSize:13,textAlign:"left",
              fontFamily:"'Nunito',sans-serif"}}>
            <span style={{fontSize:14}}>{t.icon}</span>
            <span>{t.label}</span>
          </button>
        ))}
      </nav>
      <div style={{padding:"12px 8px 4px",marginTop:8,borderTop:`1px solid ${B.border2}`}}>
        <div style={{fontSize:9,color:B.muted,fontWeight:700,letterSpacing:1,
          padding:"0 6px",marginBottom:6}}>WORKSPACES</div>
        <WsList/>
      </div>
      <div style={{padding:"12px 8px",borderTop:`1px solid ${B.border2}`}}>
        <div style={{fontSize:9,color:B.muted,fontWeight:700,letterSpacing:1,
          padding:"0 6px",marginBottom:8}}>INTEGRATIONS</div>
        <div style={{background:`${B.lime}0a`,border:`1px dashed ${B.lime}33`,
          borderRadius:10,padding:"10px 12px",textAlign:"center"}}>
          <div style={{fontSize:16,marginBottom:4}}>🔗</div>
          <div style={{fontSize:11,fontWeight:700,color:B.lime,marginBottom:2}}>Coming Soon</div>
          <div style={{fontSize:9,color:B.muted,lineHeight:1.5}}>
            Meta & Google Analytics integration launching in a future update
          </div>
        </div>
      </div>
      <SidebarAd/>
      <div style={{padding:"10px 12px 14px",borderTop:`1px solid ${B.border2}`,marginTop:"auto"}}>
        <a href="mailto:glimify.io@gmail.com"
          style={{display:"flex",alignItems:"center",gap:7,
            color:B.muted,textDecoration:"none",fontSize:10}}>
          <span>✉️</span><span>glimify.io@gmail.com</span>
        </a>
      </div>
    </div>
  );

  const BottomNav=()=>(
    <div style={{position:"fixed",bottom:0,left:0,right:0,zIndex:100,
      background:B.surface,borderTop:`2px solid ${B.pink}`,
      display:"flex",padding:"4px 0 6px",
      backdropFilter:"blur(12px)"}}>
      {TABS.map(t=>(
        <button key={t.id} onClick={()=>setTab(t.id)}
          style={{display:"flex",flexDirection:"column",alignItems:"center",
            gap:1,padding:"4px",background:"none",border:"none",
            cursor:"pointer",color:tab===t.id?ws.color||B.lime:B.muted,
            flex:1,minWidth:0}}>
          <span style={{fontSize:bp.isMobile?15:17}}>{t.icon}</span>
          <span style={{fontSize:bp.isMobile?7:9,fontWeight:tab===t.id?700:400,
            whiteSpace:"nowrap",overflow:"hidden",
            textOverflow:"ellipsis",maxWidth:"100%",
            padding:"0 2px"}}>
            {t.label}
          </span>
        </button>
      ))}
    </div>
  );

  const TabletBar=()=>(
    <div style={{position:"sticky",top:0,zIndex:90,background:B.bg,
      borderBottom:`2px solid ${B.pink}`,backdropFilter:"blur(10px)"}}>
      <div style={{display:"flex",alignItems:"center",gap:12,
        padding:"11px 20px 0",flexWrap:"wrap"}}>
        <div style={{display:"flex",alignItems:"center",gap:8,flexShrink:0}}>
          <Logo size={30}/><LogoWord size={14}/>
        </div>
        <div style={{display:"flex",gap:5,overflowX:"auto",flex:1}}>
          {workspaces.map(w=>(
            <div key={w.id} style={{display:"flex",alignItems:"center",gap:2,flexShrink:0}}>
              <button onClick={()=>{setWsId(w.id);setSelDay(null);}}
                style={{background:wsId===w.id?`${w.color}22`:"transparent",
                  border:`1px solid ${wsId===w.id?w.color:B.border2}`,
                  color:wsId===w.id?w.color:B.muted,fontSize:11,
                  fontWeight:wsId===w.id?700:400,padding:"4px 11px",
                  borderRadius:20,cursor:"pointer",whiteSpace:"nowrap",
                  fontFamily:"'Nunito',sans-serif"}}>
                {w.emoji} {w.name}
              </button>
              {workspaces.length>1&&(
                <button onClick={()=>setDelConfirm(w.id)}
                  style={{background:"none",border:"none",color:B.muted,
                    cursor:"pointer",fontSize:10,padding:"2px"}}
                  onMouseEnter={e=>e.currentTarget.style.color=B.red}
                  onMouseLeave={e=>e.currentTarget.style.color=B.muted}>✕</button>
              )}
            </div>
          ))}
          <button onClick={()=>setNewWsOpen(true)}
            style={{background:"transparent",border:`1px dashed ${B.border2}`,
              color:B.muted,fontSize:11,padding:"4px 10px",borderRadius:20,
              cursor:"pointer",whiteSpace:"nowrap",flexShrink:0,
              fontFamily:"'Nunito',sans-serif"}}>+ New</button>
        </div>
        {/* integrations coming soon pill */}
        <div style={{display:"flex",gap:5,flexShrink:0}}>
          <div style={{background:`${B.lime}18`,border:`1px solid ${B.lime}33`,
            color:B.lime,fontSize:10,fontWeight:700,padding:"4px 10px",
            borderRadius:20,display:"flex",alignItems:"center",gap:4}}>
            <span>🔗</span><span>Integrations — Soon</span>
          </div>
        </div>
      </div>
      <div style={{display:"flex",overflowX:"auto",padding:"0 14px"}}>
        {TABS.map(t=>(
          <button key={t.id} onClick={()=>setTab(t.id)}
            style={{background:"none",border:"none",
              color:tab===t.id?ws.color||B.lime:B.muted,
              fontWeight:tab===t.id?700:400,fontSize:12,
              padding:"8px 12px",cursor:"pointer",
              borderBottom:tab===t.id?`2px solid ${ws.color||B.lime}`:"2px solid transparent",
              whiteSpace:"nowrap",fontFamily:"'Nunito',sans-serif"}}>
            {t.icon} {t.label}
          </button>
        ))}
      </div>
    </div>
  );

  const MobileBar=()=>(
    <div style={{position:"sticky",top:0,zIndex:90,background:B.bg,
      borderBottom:`2px solid ${B.pink}`,
      padding:"10px 14px",display:"flex",alignItems:"center",gap:8}}>
      <Logo size={28}/>
      <div style={{flex:1,minWidth:0}}>
        <LogoWord size={14}/>
        <div style={{fontSize:9,color:B.muted,whiteSpace:"nowrap",
          overflow:"hidden",textOverflow:"ellipsis"}}>
          {ws.emoji} {ws.name} · {MONTH_NAMES[ws.month]}
        </div>
      </div>
      {/* user avatar or cloud save */}
      {user ? (
        <button onClick={()=>setShowProfile(true)}
          style={{background:"none",border:"none",cursor:"pointer",padding:0,flexShrink:0}}>
          {user.user_metadata?.avatar_url
            ? <img src={user.user_metadata.avatar_url} width={28} height={28}
                style={{borderRadius:"50%",objectFit:"cover",
                  border:`2px solid ${B.lime}`}} alt=""/>
            : <div style={{width:28,height:28,borderRadius:"50%",
                background:`linear-gradient(135deg,${B.pink},${B.lime})`,
                display:"flex",alignItems:"center",justifyContent:"center",
                fontSize:11,fontWeight:900,color:B.black}}>
                {(user.user_metadata?.full_name||user.email||"G")[0].toUpperCase()}
              </div>
          }
        </button>
      ):(
        <button onClick={()=>setShowSignIn(true)}
          style={{background:`${B.lime}18`,border:`1px solid ${B.lime}33`,
            color:B.lime,fontSize:9,fontWeight:800,padding:"4px 9px",
            borderRadius:20,cursor:"pointer",flexShrink:0,letterSpacing:.5}}>
          ☁️ Save
        </button>
      )}
      <select value={wsId}
        onChange={e=>{
          if(e.target.value==="__new__")setNewWsOpen(true);
          else{setWsId(e.target.value);setSelDay(null);}
        }}
        style={{background:B.surface2,border:`1px solid ${B.border2}`,
          color:B.text,borderRadius:8,padding:"5px 8px",fontSize:10,
          outline:"none",cursor:"pointer",maxWidth:110}}>
        {workspaces.map(w=>(
          <option key={w.id} value={w.id} style={{background:B.surface2}}>
            {w.emoji} {w.name}
          </option>
        ))}
        <option value="__new__" style={{background:B.surface2}}>+ New</option>
      </select>
    </div>
  );

  /* ── AD GATE ── */
  if(!adDone && !showSignIn) return <AdGate onComplete={()=>setAdDone(true)}/>;

  /* ── floating support button ── */
  const SupportBtn = () => (
    <a href="#support-footer"
      onClick={e=>{e.preventDefault();document.getElementById("glimify-support-footer")?.scrollIntoView({behavior:"smooth"});}}
      title="Support Glimify"
      style={{position:"fixed",bottom:bp.isMobile?72:24,left:16,zIndex:99,
        background:`linear-gradient(135deg,${B.pink},${B.purple})`,
        border:"none",color:"#fff",fontWeight:800,fontSize:11,
        padding:"8px 14px",borderRadius:30,cursor:"pointer",
        textDecoration:"none",display:"flex",alignItems:"center",gap:5,
        boxShadow:`0 4px 20px ${B.pink}55`,
        transition:"transform .2s"}}
      onMouseEnter={e=>e.currentTarget.style.transform="scale(1.05)"}
      onMouseLeave={e=>e.currentTarget.style.transform="scale(1)"}>
      <span>☕</span><span>Support</span>
    </a>
  );

  /* ══ MAIN RENDER ══ */
  return(
    <div style={{fontFamily:"'Nunito',system-ui,sans-serif",
      background:B.bg,color:B.text,minHeight:"100vh"}}>
      <style>{`
        @keyframes glimToast {
          from { transform: translateY(20px); opacity: 0; }
          to   { transform: none; opacity: 1; }
        }
        @keyframes glimSparkle {
          0%,100% { opacity:1; transform:scale(1) rotate(0deg); }
          25%      { opacity:.6; transform:scale(1.3) rotate(15deg); }
          50%      { opacity:1; transform:scale(.85) rotate(-10deg); }
          75%      { opacity:.7; transform:scale(1.2) rotate(8deg); }
        }
        @keyframes glimHoloPulse {
          0%,100% { filter:drop-shadow(0 0 4px #FF3EA5aa) drop-shadow(0 0 8px #D9FB6055); }
          33%     { filter:drop-shadow(0 0 6px #A78BFAaa) drop-shadow(0 0 12px #60A5FA55); }
          66%     { filter:drop-shadow(0 0 5px #D9FB60aa) drop-shadow(0 0 10px #FF3EA555); }
        }
        .glim-logo-wrap { animation: glimHoloPulse 3s ease-in-out infinite; }
        .glim-star-1    { animation: glimSparkle 2.2s ease-in-out infinite; transform-origin: center; }
        .glim-star-2    { animation: glimSparkle 1.8s ease-in-out infinite .4s; transform-origin: center; }
        .glim-star-3    { animation: glimSparkle 2.6s ease-in-out infinite .8s; transform-origin: center; }

        /* ── CUSTOM CURSOR ── */
        *, *::before, *::after { box-sizing: border-box; }
        html, body {
          cursor: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='32' height='32' viewBox='0 0 32 32'%3E%3Cdefs%3E%3ClinearGradient id='cg' x1='0%25' y1='0%25' x2='100%25' y2='100%25'%3E%3Cstop offset='0%25' stop-color='%23FF3EA5'/%3E%3Cstop offset='50%25' stop-color='%23D9FB60'/%3E%3Cstop offset='100%25' stop-color='%23A78BFA'/%3E%3C/linearGradient%3E%3C/defs%3E%3Cpath d='M6 2 L10 22 L14 14 L22 10 Z' fill='url(%23cg)' stroke='%23000' stroke-width='1.5'/%3E%3Cpath d='M22 8 L23 11 L26 12 L23 13 L22 16 L21 13 L18 12 L21 11Z' fill='%23D9FB60' opacity='.9'/%3E%3Cpath d='M26 2 L26.5 4 L28.5 4.5 L26.5 5 L26 7 L25.5 5 L23.5 4.5 L25.5 4Z' fill='%23FF3EA5' opacity='.8'/%3E%3C/svg%3E") 6 2, auto !important;
        }
        button, a, select, input, textarea, [role="button"] {
          cursor: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='32' height='32' viewBox='0 0 32 32'%3E%3Cdefs%3E%3ClinearGradient id='cg2' x1='0%25' y1='0%25' x2='100%25' y2='100%25'%3E%3Cstop offset='0%25' stop-color='%23FF3EA5'/%3E%3Cstop offset='50%25' stop-color='%23D9FB60'/%3E%3Cstop offset='100%25' stop-color='%23A78BFA'/%3E%3C/linearGradient%3E%3C/defs%3E%3Cpath d='M6 2 L10 22 L14 14 L22 10 Z' fill='url(%23cg2)' stroke='%23000' stroke-width='1.5'/%3E%3Ccircle cx='20' cy='20' r='5' fill='none' stroke='%23D9FB60' stroke-width='1.5' opacity='.8'/%3E%3Cpath d='M22 8 L23 11 L26 12 L23 13 L22 16 L21 13 L18 12 L21 11Z' fill='%23D9FB60' opacity='.9'/%3E%3C/svg%3E") 6 2, pointer !important;
        }

        ::-webkit-scrollbar { width: 4px; height: 4px; }
        ::-webkit-scrollbar-track { background: transparent; }
        ::-webkit-scrollbar-thumb { background: #2a2a2a; border-radius: 10px; }
      `}</style>
      <Toast msg={toast}/>
      <SupportBtn/>

      {/* DESKTOP */}
      {bp.isDesktop&&(
        <div style={{display:"flex",minHeight:"100vh"}}>
          <Sidebar/>
          <div style={{flex:1,minWidth:0,display:"flex",flexDirection:"column"}}>
            <div style={{position:"sticky",top:0,zIndex:90,background:B.bg,
              borderBottom:`1px solid ${B.border2}`,padding:"13px 28px",
              display:"flex",alignItems:"center",justifyContent:"space-between",
              backdropFilter:"blur(10px)"}}>
              <div>
                <div style={{fontSize:15,fontWeight:700}}>
                  {TABS.find(t=>t.id===tab)?.icon} {TABS.find(t=>t.id===tab)?.label}
                </div>
                <div style={{fontSize:11,color:B.muted}}>
                  {ws.emoji} {ws.name} · {MONTH_NAMES[ws.month]} {ws.year}
                </div>
              </div>
              <div style={{display:"flex",gap:8,alignItems:"center"}}>
                {user ? (
                  <button onClick={()=>setShowProfile(true)}
                    style={{display:"flex",alignItems:"center",gap:8,
                      background:B.surface2,border:`1px solid ${B.border2}`,
                      borderRadius:30,padding:"5px 14px 5px 5px",cursor:"pointer"}}>
                    {user.user_metadata?.avatar_url
                      ? <img src={user.user_metadata.avatar_url} width={26} height={26}
                          style={{borderRadius:"50%",objectFit:"cover"}} alt=""/>
                      : <div style={{width:26,height:26,borderRadius:"50%",
                          background:`linear-gradient(135deg,${B.pink},${B.lime})`,
                          display:"flex",alignItems:"center",justifyContent:"center",
                          fontSize:12,fontWeight:900,color:B.black}}>
                          {(user.user_metadata?.full_name||user.email||"G")[0].toUpperCase()}
                        </div>
                    }
                    <span style={{fontSize:12,fontWeight:600,color:B.text}}>
                      {user.user_metadata?.full_name?.split(" ")[0]||"Account"}
                    </span>
                    <div style={{width:7,height:7,borderRadius:"50%",background:B.lime}}/>
                  </button>
                ):(
                  <button onClick={()=>setShowSignIn(true)}
                    style={{background:`${B.lime}22`,border:`1px solid ${B.lime}44`,
                      color:B.lime,fontSize:12,fontWeight:700,padding:"8px 14px",
                      borderRadius:8,cursor:"pointer",fontFamily:"'Nunito',sans-serif",
                      display:"flex",alignItems:"center",gap:5}}>
                    <span>☁️</span><span>Save My Data</span>
                  </button>
                )}
                <button onClick={()=>setNewWsOpen(true)}
                  style={{background:`${B.pink}18`,border:`1px solid ${B.pink}33`,
                    color:B.pink,fontSize:12,fontWeight:700,padding:"8px 14px",
                    borderRadius:8,cursor:"pointer",fontFamily:"'Nunito',sans-serif"}}>
                  + Workspace
                </button>
              </div>
            </div>
            <div style={{flex:1,overflowY:"auto"}}>
              <div style={{padding:"20px 28px",maxWidth:860}}>
                <StatsStrip/>
                {TAB_MAP[tab]}
              </div>
              <Footer/>
            </div>
          </div>
        </div>
      )}

      {/* TABLET */}
      {bp.isTablet&&(
        <div>
          <TabletBar/>
          <div style={{padding:"16px 20px 90px"}}>
            <StatsStrip/>{TAB_MAP[tab]}
          </div>
          <Footer/>
          <BottomNav/>
        </div>
      )}

      {/* MOBILE */}
      {bp.isMobile&&(
        <div>
          <MobileBar/>
          <div style={{padding:"12px 14px 90px"}}>
            <StatsStrip/>{TAB_MAP[tab]}
          </div>
          <Footer/>
          <BottomNav/>
        </div>
      )}

      {newWsOpen&&<NewWsModal/>}
      {delConfirm&&<DelModal/>}

      {/* Sign In Screen */}
      {showSignIn&&(
        <div style={{position:"fixed",inset:0,zIndex:600}}>
          <SignInScreen onSkip={()=>setShowSignIn(false)}/>
        </div>
      )}

      {/* Profile Modal */}
      {showProfile&&(
        <ProfilePage
          user={user}
          workspaces={workspaces}
          onSignOut={handleSignOut}
          onClose={()=>setShowProfile(false)}
          bp={bp}
        />
      )}
    </div>
  );
}

const _r=ReactDOM.createRoot(document.getElementById('root'));
_r.render(React.createElement(GlimifyApp));
</script>
</body>
</html>

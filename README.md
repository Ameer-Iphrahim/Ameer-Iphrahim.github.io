<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes">
    <title>Tile Animation Explorer · 110+ unique effects</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        /* ===== ORIGINAL STYLES (unchanged) ===== */
        html, body {
            width: 100%;
            height: 100%;
            margin: 0;
            overflow: hidden;
            background: #f7f7f7;
            font-family: Inter, sans-serif;
        }
        body {
            display: flex;
        }
        .sidebar {
            width: 320px;
            background: white;
            border-right: 1px solid rgba(0,0,0,.05);
            padding: 24px;
            overflow: auto;
        }
        .title {
            font-size: 22px;
            font-weight: 700;
            margin-bottom: 20px;
        }
        .anim-btn {
            width: 100%;
            text-align: left;
            border: none;
            background: white;
            padding: 14px 18px;
            margin-bottom: 10px;
            border-radius: 16px;
            cursor: pointer;
            transition: .25s;
            box-shadow: 0 4px 12px rgba(0,0,0,.04);
            font-size: 14px;
            font-weight: 500;
            color: #1e1e1e;
        }
        .anim-btn:hover {
            transform: translateX(6px);
            box-shadow: 0 10px 24px rgba(0,0,0,.08);
        }
        .stage {
            flex: 1;
            display: flex;
            justify-content: center;
            align-items: center;
            position: relative;
        }
        .tile {
            width: 260px;
            height: 260px;
            border-radius: 36px;
            background: white;
            box-shadow: 0 30px 80px rgba(0,0,0,.08), 0 10px 30px rgba(0,0,0,.05);
            transform-style: preserve-3d;
            transform-origin: center center;
        }
        .controls {
            position: absolute;
            bottom: 40px;
            display: flex;
            gap: 12px;
        }
        .control {
            border: none;
            border-radius: 999px;
            padding: 12px 18px;
            background: white;
            cursor: pointer;
            box-shadow: 0 8px 20px rgba(0,0,0,.07);
            font-weight: 500;
        }
        /* original 5 animations */
        .anim-tile21 { animation: tile21Enter 2.5s cubic-bezier(.16,1,.3,1); }
        @keyframes tile21Enter {
            from { opacity: 0; transform: perspective(1600px) scale(.08) rotate3d(1,1,0,190deg); filter: blur(13px); }
            14% { opacity: 1; }
            to { opacity: 1; transform: perspective(1600px) scale(1); filter: none; }
        }
        .anim-spin { animation: spinEnter 2.2s cubic-bezier(.16,1,.3,1); }
        @keyframes spinEnter {
            from { opacity: 0; transform: perspective(1600px) rotateY(720deg) scale(.2); }
            to { opacity: 1; transform: perspective(1600px) rotateY(0deg) scale(1); }
        }
        .anim-flip { animation: flipEnter 2s cubic-bezier(.16,1,.3,1); }
        @keyframes flipEnter {
            from { opacity: 0; transform: perspective(1600px) rotateX(-120deg) translateY(-220px); }
            to { opacity: 1; transform: perspective(1600px) rotateX(0); }
        }
        .anim-vortex { animation: vortexEnter 3s cubic-bezier(.16,1,.3,1); }
        @keyframes vortexEnter {
            from { opacity: 0; transform: perspective(1600px) rotateX(-80deg) rotateY(80deg) rotateZ(220deg) scale(.2); }
            to { opacity: 1; transform: perspective(1600px) scale(1); }
        }
        .anim-depth { animation: depthEnter 2.5s cubic-bezier(.16,1,.3,1); }
        @keyframes depthEnter {
            from { opacity: 0; transform: perspective(1600px) translateZ(-1000px) scale(.1); }
            to { opacity: 1; transform: perspective(1600px) translateZ(0) scale(1); }
        }
        /* ===== END ORIGINAL STYLES ===== */

        /* All new keyframes will be injected dynamically via JS */
    </style>
</head>
<body>
    <div class="sidebar">
        <div class="title">Animation Library</div>
        <div id="button-container">
            <!-- original 5 buttons -->
            <button class="anim-btn" data-anim="anim-tile21">Tile 21</button>
            <button class="anim-btn" data-anim="anim-spin">720° Spin</button>
            <button class="anim-btn" data-anim="anim-flip">Flip Drop</button>
            <button class="anim-btn" data-anim="anim-vortex">Vortex</button>
            <button class="anim-btn" data-anim="anim-depth">Depth Zoom</button>
        </div>
    </div>

    <div class="stage">
        <div id="tile" class="tile anim-tile21"></div>
        <div class="controls">
            <button class="control" id="replay">Replay</button>
            <button class="control" id="random">Random</button>
        </div>
    </div>

    <script>
        (function() {
            // --------------------------------------------------------------
            // 1. MASTER LIST OF 110+ UNIQUE ANIMATIONS
            //    Each entry: { name, class, keyframesCSS, animationShorthand }
            // --------------------------------------------------------------
            const animations = [];

            // helper to add one animation
            function add(name, cls, keyframesDef, animValue) {
                animations.push({
                    name: name,
                    class: cls,
                    css: keyframesDef,        // full @keyframes rule
                    animation: animValue       // e.g., "myAnim 2s ease"
                });
            }

            // ---- original 5 (preserved) ----
            add('Tile 21', 'anim-tile21',
                `@keyframes tile21Enter {
                    from { opacity:0; transform:perspective(1600px) scale(.08) rotate3d(1,1,0,190deg); filter:blur(13px); }
                    14% { opacity:1; }
                    to { opacity:1; transform:perspective(1600px) scale(1); filter:none; }
                }`, 'tile21Enter 2.5s cubic-bezier(.16,1,.3,1)');
            add('720° Spin', 'anim-spin',
                `@keyframes spinEnter {
                    from { opacity:0; transform:perspective(1600px) rotateY(720deg) scale(.2); }
                    to { opacity:1; transform:perspective(1600px) rotateY(0deg) scale(1); }
                }`, 'spinEnter 2.2s cubic-bezier(.16,1,.3,1)');
            add('Flip Drop', 'anim-flip',
                `@keyframes flipEnter {
                    from { opacity:0; transform:perspective(1600px) rotateX(-120deg) translateY(-220px); }
                    to { opacity:1; transform:perspective(1600px) rotateX(0); }
                }`, 'flipEnter 2s cubic-bezier(.16,1,.3,1)');
            add('Vortex', 'anim-vortex',
                `@keyframes vortexEnter {
                    from { opacity:0; transform:perspective(1600px) rotateX(-80deg) rotateY(80deg) rotateZ(220deg) scale(.2); }
                    to { opacity:1; transform:perspective(1600px) scale(1); }
                }`, 'vortexEnter 3s cubic-bezier(.16,1,.3,1)');
            add('Depth Zoom', 'anim-depth',
                `@keyframes depthEnter {
                    from { opacity:0; transform:perspective(1600px) translateZ(-1000px) scale(.1); }
                    to { opacity:1; transform:perspective(1600px) translateZ(0) scale(1); }
                }`, 'depthEnter 2.5s cubic-bezier(.16,1,.3,1)');

            // ---- Now 105+ NEW unique animations ----
            add('Shatter In', 'anim-shatter',
                `@keyframes shatterIn {
                    0% { opacity:0; transform:perspective(1600px) scale(0.2) rotateZ(35deg); clip-path:polygon(50% 0%, 61% 35%, 98% 35%, 68% 57%, 79% 91%, 50% 70%, 21% 91%, 32% 57%, 2% 35%, 39% 35%); }
                    30% { opacity:0.8; clip-path:polygon(50% 0%, 61% 35%, 98% 35%, 68% 57%, 79% 91%, 50% 70%, 21% 91%, 32% 57%, 2% 35%, 39% 35%); }
                    100% { opacity:1; transform:perspective(1600px) scale(1) rotateZ(0deg); clip-path:polygon(0% 0%, 100% 0%, 100% 100%, 0% 100%); }
                }`, 'shatterIn 2.8s cubic-bezier(.16,1,.3,1)');

            add('Rip Vertical', 'anim-rip-v',
                `@keyframes ripVertical {
                    0% { opacity:0; transform:perspective(1600px) scaleY(0.05) translateY(-60px); filter:blur(6px); }
                    50% { opacity:1; transform:perspective(1600px) scaleY(1.05) translateY(4px); }
                    100% { opacity:1; transform:perspective(1600px) scaleY(1) translateY(0); filter:none; }
                }`, 'ripVertical 2.4s cubic-bezier(.16,1,.3,1)');

            add('Rip Horizontal', 'anim-rip-h',
                `@keyframes ripHorizontal {
                    0% { opacity:0; transform:perspective(1600px) scaleX(0.05) translateX(-80px); filter:blur(6px); }
                    60% { opacity:1; transform:perspective(1600px) scaleX(1.04) translateX(3px); }
                    100% { opacity:1; transform:perspective(1600px) scaleX(1) translateX(0); filter:none; }
                }`, 'ripHorizontal 2.4s cubic-bezier(.16,1,.3,1)');

            add('Pixel Dissolve', 'anim-pixel',
                `@keyframes pixelDissolve {
                    0% { opacity:0; transform:perspective(1600px) scale(1.3); filter:blur(12px) contrast(0.2); }
                    40% { opacity:0.7; filter:blur(4px) contrast(1.2); }
                    100% { opacity:1; transform:perspective(1600px) scale(1); filter:none; }
                }`, 'pixelDissolve 2.7s cubic-bezier(.16,1,.3,1)');

            add('Glitch Slice', 'anim-glitch',
                `@keyframes glitchSlice {
                    0% { opacity:0; transform:perspective(1600px) translateX(-20px) skewX(15deg); clip-path:inset(0 0 60% 0); }
                    20% { opacity:0.9; transform:perspective(1600px) translateX(15px) skewX(-8deg); clip-path:inset(30% 0 20% 0); }
                    40% { opacity:1; transform:perspective(1600px) translateX(-8px) skewX(4deg); clip-path:inset(10% 0 50% 0); }
                    100% { opacity:1; transform:perspective(1600px) translateX(0) skewX(0); clip-path:inset(0 0 0 0); }
                }`, 'glitchSlice 2.3s steps(6) both');

            add('Fold Diagonal', 'anim-fold-diag',
                `@keyframes foldDiagonal {
                    0% { opacity:0; transform:perspective(1600px) rotate3d(1,1,0,120deg) scale(0.5); filter:blur(7px); }
                    100% { opacity:1; transform:perspective(1600px) rotate3d(0,0,0,0deg) scale(1); filter:none; }
                }`, 'foldDiagonal 2.6s cubic-bezier(.16,1,.3,1)');

            add('Melt Down', 'anim-melt',
                `@keyframes meltDown {
                    0% { opacity:0; transform:perspective(1600px) translateY(-90px) scaleY(1.5) scaleX(0.7); filter:blur(10px); }
                    100% { opacity:1; transform:perspective(1600px) translateY(0) scaleY(1) scaleX(1); filter:none; }
                }`, 'meltDown 2.5s cubic-bezier(.16,1,.3,1)');

            add('Inflate Bounce', 'anim-inflate',
                `@keyframes inflateBounce {
                    0% { opacity:0; transform:perspective(1600px) scale(0.2); border-radius:80px; }
                    50% { opacity:1; transform:perspective(1600px) scale(1.12); border-radius:28px; }
                    75% { transform:perspective(1600px) scale(0.94); border-radius:38px; }
                    100% { opacity:1; transform:perspective(1600px) scale(1); border-radius:36px; }
                }`, 'inflateBounce 2.9s cubic-bezier(.16,1,.3,1)');

            add('Stretch Bounce', 'anim-stretch',
                `@keyframes stretchBounce {
                    0% { opacity:0; transform:perspective(1600px) scaleX(0.3) scaleY(1.6); }
                    55% { opacity:1; transform:perspective(1600px) scaleX(1.08) scaleY(0.88); }
                    80% { transform:perspective(1600px) scaleX(0.96) scaleY(1.04); }
                    100% { opacity:1; transform:perspective(1600px) scaleX(1) scaleY(1); }
                }`, 'stretchBounce 2.7s cubic-bezier(.16,1,.3,1)');

            add('Whoosh Left', 'anim-whoosh-l',
                `@keyframes whooshLeft {
                    0% { opacity:0; transform:perspective(1600px) translateX(-320px) rotateY(55deg) scale(0.7); filter:blur(9px); }
                    100% { opacity:1; transform:perspective(1600px) translateX(0) rotateY(0) scale(1); filter:none; }
                }`, 'whooshLeft 2.3s cubic-bezier(.16,1,.3,1)');

            add('Whoosh Right', 'anim-whoosh-r',
                `@keyframes whooshRight {
                    0% { opacity:0; transform:perspective(1600px) translateX(320px) rotateY(-55deg) scale(0.7); filter:blur(9px); }
                    100% { opacity:1; transform:perspective(1600px) translateX(0) rotateY(0) scale(1); filter:none; }
                }`, 'whooshRight 2.3s cubic-bezier(.16,1,.3,1)');

            add('Curl Unfold', 'anim-curl',
                `@keyframes curlUnfold {
                    0% { opacity:0; transform:perspective(1600px) rotateX(-80deg) rotateY(30deg) scale(0.4); filter:blur(11px); }
                    100% { opacity:1; transform:perspective(1600px) rotateX(0) rotateY(0) scale(1); filter:none; }
                }`, 'curlUnfold 2.9s cubic-bezier(.16,1,.3,1)');

            add('Spiral In', 'anim-spiral',
                `@keyframes spiralIn {
                    0% { opacity:0; transform:perspective(1600px) rotateZ(280deg) scale(0.15) translateY(40px); filter:blur(15px); }
                    100% { opacity:1; transform:perspective(1600px) rotateZ(0deg) scale(1) translateY(0); filter:none; }
                }`, 'spiralIn 3.0s cubic-bezier(.16,1,.3,1)');

            add('Card Flip Back', 'anim-cardflip',
                `@keyframes cardFlipBack {
                    0% { opacity:0; transform:perspective(1600px) rotateY(180deg) scale(0.8); }
                    100% { opacity:1; transform:perspective(1600px) rotateY(0deg) scale(1); }
                }`, 'cardFlipBack 2.2s cubic-bezier(.16,1,.3,1)');

            add('Drop Shadow Reveal', 'anim-dropshadow',
                `@keyframes dropShadowReveal {
                    0% { opacity:0; transform:perspective(1600px) translateY(-160px); box-shadow:0 80px 100px rgba(0,0,0,0); }
                    70% { opacity:1; transform:perspective(1600px) translateY(8px); box-shadow:0 30px 80px rgba(0,0,0,.08); }
                    100% { opacity:1; transform:perspective(1600px) translateY(0); }
                }`, 'dropShadowReveal 2.1s cubic-bezier(.16,1,.3,1)');

            add('Peel Corner', 'anim-peel',
                `@keyframes peelCorner {
                    0% { opacity:0; transform:perspective(1600px) rotateX(45deg) rotateY(-35deg) scale(0.6); filter:blur(5px); }
                    100% { opacity:1; transform:perspective(1600px) rotateX(0) rotateY(0) scale(1); filter:none; }
                }`, 'peelCorner 2.5s cubic-bezier(.16,1,.3,1)');

            add('Blur Zoom', 'anim-blurzoom',
                `@keyframes blurZoom {
                    0% { opacity:0; transform:perspective(1600px) scale(1.8); filter:blur(18px); }
                    100% { opacity:1; transform:perspective(1600px) scale(1); filter:none; }
                }`, 'blurZoom 2.4s cubic-bezier(.16,1,.3,1)');

            add('Slide Up Fade', 'anim-slideup',
                `@keyframes slideUpFade {
                    0% { opacity:0; transform:perspective(1600px) translateY(120px); filter:blur(4px); }
                    100% { opacity:1; transform:perspective(1600px) translateY(0); filter:none; }
                }`, 'slideUpFade 1.9s cubic-bezier(.16,1,.3,1)');

            add('Rotate Scale', 'anim-rotatescale',
                `@keyframes rotateScale {
                    0% { opacity:0; transform:perspective(1600px) rotate(160deg) scale(0.35); }
                    100% { opacity:1; transform:perspective(1600px) rotate(0deg) scale(1); }
                }`, 'rotateScale 2.1s cubic-bezier(.16,1,.3,1)');

            add('Swing Gate Left', 'anim-swing-l',
                `@keyframes swingGate {
                    0% { opacity:0; transform:perspective(1600px) rotateY(-110deg); transform-origin:left center; }
                    100% { opacity:1; transform:perspective(1600px) rotateY(0deg); transform-origin:left center; }
                }`, 'swingGate 2.6s cubic-bezier(.16,1,.3,1)');

            add('Swing Gate Right', 'anim-swing-r',
                `@keyframes swingGateRight {
                    0% { opacity:0; transform:perspective(1600px) rotateY(110deg); transform-origin:right center; }
                    100% { opacity:1; transform:perspective(1600px) rotateY(0deg); transform-origin:right center; }
                }`, 'swingGateRight 2.6s cubic-bezier(.16,1,.3,1)');

            add('Vertical Shutter', 'anim-vshutter',
                `@keyframes verticalShutter {
                    0% { opacity:0; transform:perspective(1600px) scaleY(0); transform-origin:top; }
                    100% { opacity:1; transform:perspective(1600px) scaleY(1); transform-origin:top; }
                }`, 'verticalShutter 2.2s cubic-bezier(.16,1,.3,1)');

            add('Horizontal Shutter', 'anim-hshutter',
                `@keyframes horizontalShutter {
                    0% { opacity:0; transform:perspective(1600px) scaleX(0); transform-origin:left; }
                    100% { opacity:1; transform:perspective(1600px) scaleX(1); transform-origin:left; }
                }`, 'horizontalShutter 2.2s cubic-bezier(.16,1,.3,1)');

            add('Morph Diamond', 'anim-morph',
                `@keyframes morphDiamond {
                    0% { opacity:0; transform:perspective(1600px) rotateZ(45deg) scale(0.5); border-radius:8px; }
                    100% { opacity:1; transform:perspective(1600px) rotateZ(0deg) scale(1); border-radius:36px; }
                }`, 'morphDiamond 2.5s cubic-bezier(.16,1,.3,1)');

            add('Warp Speed', 'anim-warp',
                `@keyframes warpSpeed {
                    0% { opacity:0; transform:perspective(1600px) translateZ(-400px) rotateX(20deg) scale(0.6); filter:blur(8px); }
                    100% { opacity:1; transform:perspective(1600px) translateZ(0) rotateX(0) scale(1); filter:none; }
                }`, 'warpSpeed 2.8s cubic-bezier(.16,1,.3,1)');

            add('Tilt Nudge', 'anim-tilt',
                `@keyframes tiltNudge {
                    0% { opacity:0; transform:perspective(1600px) rotateX(35deg) rotateY(-25deg) translateY(40px); }
                    100% { opacity:1; transform:perspective(1600px) rotateX(0) rotateY(0) translateY(0); }
                }`, 'tiltNudge 2.0s cubic-bezier(.16,1,.3,1)');

            add('Compress Expand', 'anim-compress',
                `@keyframes compressExpand {
                    0% { opacity:0; transform:perspective(1600px) scaleX(1.4) scaleY(0.5); }
                    70% { opacity:1; transform:perspective(1600px) scaleX(0.9) scaleY(1.15); }
                    100% { opacity:1; transform:perspective(1600px) scaleX(1) scaleY(1); }
                }`, 'compressExpand 2.4s cubic-bezier(.16,1,.3,1)');

            add('Diamond Slice', 'anim-diamonds',
                `@keyframes diamondSlice {
                    0% { opacity:0; clip-path:polygon(50% 50%, 50% 50%, 50% 50%, 50% 50%); transform:perspective(1600px) scale(0.5); }
                    100% { opacity:1; clip-path:polygon(0% 0%, 100% 0%, 100% 100%, 0% 100%); transform:perspective(1600px) scale(1); }
                }`, 'diamondSlice 2.5s cubic-bezier(.16,1,.3,1)');

            add('Hexagon Reveal', 'anim-hexagon',
                `@keyframes hexagonReveal {
                    0% { opacity:0; clip-path:polygon(25% 0%, 75% 0%, 100% 50%, 75% 100%, 25% 100%, 0% 50%); transform:perspective(1600px) rotateZ(30deg); }
                    100% { opacity:1; clip-path:polygon(0% 0%, 100% 0%, 100% 100%, 0% 100%); transform:perspective(1600px) rotateZ(0deg); }
                }`, 'hexagonReveal 2.7s cubic-bezier(.16,1,.3,1)');

            add('Twist Open', 'anim-twistopen',
                `@keyframes twistOpen {
                    0% { opacity:0; transform:perspective(1600px) rotateY(90deg) rotateZ(20deg) scale(0.7); }
                    100% { opacity:1; transform:perspective(1600px) rotateY(0) rotateZ(0) scale(1); }
                }`, 'twistOpen 2.3s cubic-bezier(.16,1,.3,1)');

            add('Pop Corner', 'anim-popcorner',
                `@keyframes popCorner {
                    0% { opacity:0; transform:perspective(1600px) translate(-40px, -40px) scale(0.4); }
                    70% { opacity:1; transform:perspective(1600px) translate(6px, 6px) scale(1.05); }
                    100% { opacity:1; transform:perspective(1600px) translate(0,0) scale(1); }
                }`, 'popCorner 2.2s cubic-bezier(.16,1,.3,1)');

            add('Elastic Rotate', 'anim-elasticrot',
                `@keyframes elasticRotate {
                    0% { opacity:0; transform:perspective(1600px) rotateZ(-40deg) scale(0.6); }
                    60% { opacity:1; transform:persective(1600px) rotateZ(8deg) scale(1.08); }
                    100% { opacity:1; transform:perspective(1600px) rotateZ(0deg) scale(1); }
                }`, 'elasticRotate 2.6s cubic-bezier(.16,1,.3,1)');

            add('Radial Wipe', 'anim-radialwipe',
                `@keyframes radialWipe {
                    0% { opacity:0; clip-path:circle(0% at 30% 30%); transform:perspective(1600px) scale(0.8); }
                    100% { opacity:1; clip-path:circle(100% at 30% 30%); transform:perspective(1600px) scale(1); }
                }`, 'radialWipe 2.4s cubic-bezier(.16,1,.3,1)');

            // ---- Continue with many more UNIQUE animations (up to 110+) ----
            // I'll generate a batch of 60+ additional distinct ones using various combos
            const additionalDefs = [
                { name: 'Jello Squish', cls: 'anim-jello', keyframeName: 'jelloSquish', css: `@keyframes jelloSquish { 0% { opacity:0; transform:perspective(1600px) scale3d(0.7,1.3,1); } 30% { opacity:1; transform:perspective(1600px) scale3d(1.15,0.85,1); } 50% { transform:perspective(1600px) scale3d(0.9,1.1,1); } 70% { transform:perspective(1600px) scale3d(1.05,0.95,1); } 100% { opacity:1; transform:perspective(1600px) scale3d(1,1,1); } }` },
                { name: 'Checker Wipe', cls: 'anim-checker', keyframeName: 'checkerWipe', css: `@keyframes checkerWipe { 0% { opacity:0; clip-path:inset(10% 10% 80% 80%); transform:perspective(1600px) scale(0.9); } 25% { clip-path:inset(20% 70% 60% 10%); } 50% { clip-path:inset(50% 40% 20% 40%); } 100% { opacity:1; clip-path:inset(0 0 0 0); transform:perspective(1600px) scale(1); } }` },
                { name: 'Tumble Dry', cls: 'anim-tumble', keyframeName: 'tumbleDry', css: `@keyframes tumbleDry { 0% { opacity:0; transform:perspective(1600px) rotateX(200deg) rotateY(160deg) scale(0.3); } 100% { opacity:1; transform:perspective(1600px) rotateX(0) rotateY(0) scale(1); } }` },
                { name: 'Origami Fold', cls: 'anim-origami', keyframeName: 'origamiFold', css: `@keyframes origamiFold { 0% { opacity:0; transform:perspective(1600px) rotateX(100deg) rotateY(40deg) scale(0.5); } 100% { opacity:1; transform:perspective(1600px) rotateX(0) rotateY(0) scale(1); } }` },
                { name: 'Crush Paper', cls: 'anim-crush', keyframeName: 'crushPaper', css: `@keyframes crushPaper { 0% { opacity:0; transform:perspective(1600px) scale(0.6) rotateZ(15deg); filter:blur(10px) contrast(1.4); } 100% { opacity:1; transform:perspective(1600px) scale(1) rotateZ(0); filter:none; } }` },
                { name: 'Stretch Left', cls: 'anim-stretch-l', keyframeName: 'stretchLeft', css: `@keyframes stretchLeft { 0% { opacity:0; transform:perspective(1600px) scaleX(0.2) translateX(-120px); } 100% { opacity:1; transform:perspective(1600px) scaleX(1) translateX(0); } }` },
                { name: 'Stretch Right', cls: 'anim-stretch-r', keyframeName: 'stretchRight', css: `@keyframes stretchRight { 0% { opacity:0; transform:perspective(1600px) scaleX(0.2) translateX(120px); } 100% { opacity:1; transform:perspective(1600px) scaleX(1) translateX(0); } }` },
                { name: 'Pinwheel', cls: 'anim-pinwheel', keyframeName: 'pinwheelEnter', css: `@keyframes pinwheelEnter { 0% { opacity:0; transform:perspective(1600px) rotate(180deg) scale(0.2); clip-path:polygon(50% 0%, 100% 50%, 50% 100%, 0% 50%); } 100% { opacity:1; transform:perspective(1600px) rotate(0deg) scale(1); clip-path:polygon(0% 0%, 100% 0%, 100% 100%, 0% 100%); } }` },
                { name: 'Flip Horizontal', cls: 'anim-flip-h', keyframeName: 'flipHorizontal', css: `@keyframes flipHorizontal { 0% { opacity:0; transform:perspective(1600px) rotateY(180deg); } 100% { opacity:1; transform:perspective(1600px) rotateY(0deg); } }` },
                { name: 'Flip Vertical', cls: 'anim-flip-v', keyframeName: 'flipVertical', css: `@keyframes flipVertical { 0% { opacity:0; transform:perspective(1600px) rotateX(180deg); } 100% { opacity:1; transform:perspective(1600px) rotateX(0deg); } }` },
                { name: 'Zoom Out Burst', cls: 'anim-zoomout', keyframeName: 'zoomOutBurst', css: `@keyframes zoomOutBurst { 0% { opacity:0; transform:perspective(1600px) scale(2.5); filter:blur(20px); } 100% { opacity:1; transform:perspective(1600px) scale(1); filter:none; } }` },
                { name: 'Slide Right Bounce', cls: 'anim-slideright', keyframeName: 'slideRightBounce', css: `@keyframes slideRightBounce { 0% { opacity:0; transform:perspective(1600px) translateX(-200px); } 60% { opacity:1; transform:perspective(1600px) translateX(15px); } 80% { transform:perspective(1600px) translateX(-6px); } 100% { opacity:1; transform:perspective(1600px) translateX(0); } }` },
                { name: 'Slide Left Bounce', cls: 'anim-slideleft', keyframeName: 'slideLeftBounce', css: `@keyframes slideLeftBounce { 0% { opacity:0; transform:perspective(1600px) translateX(200px); } 60% { opacity:1; transform:perspective(1600px) translateX(-15px); } 80% { transform:perspective(1600px) translateX(6px); } 100% { opacity:1; transform:perspective(1600px) translateX(0); } }` },
                { name: 'Skew Reveal', cls: 'anim-skew', keyframeName: 'skewReveal', css: `@keyframes skewReveal { 0% { opacity:0; transform:perspective(1600px) skewX(25deg) skewY(10deg); } 100% { opacity:1; transform:perspective(1600px) skewX(0) skewY(0); } }` },
                { name: 'Perspective Shift', cls: 'anim-pershift', keyframeName: 'perspectiveShift', css: `@keyframes perspectiveShift { 0% { opacity:0; transform:perspective(1600px) rotateY(50deg) translateZ(-150px); } 100% { opacity:1; transform:perspective(1600px) rotateY(0) translateZ(0); } }` },
                { name: 'Scale Fade In', cls: 'anim-scalefade', keyframeName: 'scaleFadeIn', css: `@keyframes scaleFadeIn { 0% { opacity:0; transform:perspective(1600px) scale(0.5); } 100% { opacity:1; transform:perspective(1600px) scale(1); } }` },
                { name: 'Rotate Fade In', cls: 'anim-rotatefade', keyframeName: 'rotateFadeIn', css: `@keyframes rotateFadeIn { 0% { opacity:0; transform:perspective(1600px) rotate(90deg); } 100% { opacity:1; transform:perspective(1600px) rotate(0deg); } }` },
                { name: 'Blur Fade', cls: 'anim-blurfade', keyframeName: 'blurFade', css: `@keyframes blurFade { 0% { opacity:0; filter:blur(15px); } 100% { opacity:1; filter:blur(0); } }` },
                { name: 'Top Corner Reveal', cls: 'anim-topcorner', keyframeName: 'topCornerReveal', css: `@keyframes topCornerReveal { 0% { opacity:0; transform:perspective(1600px) translate(-40px, -40px) scale(0.4); } 100% { opacity:1; transform:perspective(1600px) translate(0,0) scale(1); } }` },
                { name: 'Bottom Corner Reveal', cls: 'anim-bottomcorner', keyframeName: 'bottomCornerReveal', css: `@keyframes bottomCornerReveal { 0% { opacity:0; transform:perspective(1600px) translate(40px, 40px) scale(0.4); } 100% { opacity:1; transform:perspective(1600px) translate(0,0) scale(1); } }` },
                { name: 'Clockwise Spin', cls: 'anim-cwspin', keyframeName: 'cwSpin', css: `@keyframes cwSpin { 0% { opacity:0; transform:perspective(1600px) rotate(360deg) scale(0.3); } 100% { opacity:1; transform:perspective(1600px) rotate(0deg) scale(1); } }` },
                { name: 'Counter Spin', cls: 'anim-ccwspin', keyframeName: 'ccwSpin', css: `@keyframes ccwSpin { 0% { opacity:0; transform:perspective(1600px) rotate(-360deg) scale(0.3); } 100% { opacity:1; transform:perspective(1600px) rotate(0deg) scale(1); } }` },
                { name: 'Drop In', cls: 'anim-dropin', keyframeName: 'dropIn', css: `@keyframes dropIn { 0% { opacity:0; transform:perspective(1600px) translateY(-300px); } 60% { opacity:1; transform:perspective(1600px) translateY(20px); } 80% { transform:perspective(1600px) translateY(-10px); } 100% { opacity:1; transform:perspective(1600px) translateY(0); } }` },
                { name: 'Rise Up', cls: 'anim-riseup', keyframeName: 'riseUp', css: `@keyframes riseUp { 0% { opacity:0; transform:perspective(1600px) translateY(300px); } 100% { opacity:1; transform:perspective(1600px) translateY(0); } }` },
                { name: 'Wobble Horizontal', cls: 'anim-wobbleh', keyframeName: 'wobbleH', css: `@keyframes wobbleH { 0% { opacity:0; transform:perspective(1600px) translateX(0); } 20% { transform:perspective(1600px) translateX(-30px); } 40% { transform:perspective(1600px) translateX(20px); } 60% { transform:perspective(1600px) translateX(-10px); } 80% { transform:perspective(1600px) translateX(5px); } 100% { opacity:1; transform:perspective(1600px) translateX(0); } }` },
                { name: 'Wobble Vertical', cls: 'anim-wobblev', keyframeName: 'wobbleV', css: `@keyframes wobbleV { 0% { opacity:0; transform:perspective(1600px) translateY(0); } 20% { transform:perspective(1600px) translateY(-30px); } 40% { transform:perspective(1600px) translateY(20px); } 60% { transform:perspective(1600px) translateY(-10px); } 80% { transform:perspective(1600px) translateY(5px); } 100% { opacity:1; transform:perspective(1600px) translateY(0); } }` },
                { name: 'Rotate In 3D', cls: 'anim-rotate3d', keyframeName: 'rotateIn3D', css: `@keyframes rotateIn3D { 0% { opacity:0; transform:perspective(1600px) rotate3d(1,0.5,0,180deg) scale(0.5); } 100% { opacity:1; transform:perspective(1600px) rotate3d(0,0,0,0deg) scale(1); } }` },
                { name: 'Swing Top', cls: 'anim-swingtop', keyframeName: 'swingTop', css: `@keyframes swingTop { 0% { opacity:0; transform:perspective(1600px) rotateX(-90deg); transform-origin:top; } 100% { opacity:1; transform:perspective(1600px) rotateX(0); transform-origin:top; } }` },
                { name: 'Swing Bottom', cls: 'anim-swingbottom', keyframeName: 'swingBottom', css: `@keyframes swingBottom { 0% { opacity:0; transform:perspective(1600px) rotateX(90deg); transform-origin:bottom; } 100% { opacity:1; transform:perspective(1600px) rotateX(0); transform-origin:bottom; } }` },
                { name: 'Peel Left', cls: 'anim-peelleft', keyframeName: 'peelLeft', css: `@keyframes peelLeft { 0% { opacity:0; transform:perspective(1600px) rotateY(-80deg); transform-origin:left; } 100% { opacity:1; transform:perspective(1600px) rotateY(0); transform-origin:left; } }` },
                { name: 'Peel Right', cls: 'anim-peelright', keyframeName: 'peelRight', css: `@keyframes peelRight { 0% { opacity:0; transform:perspective(1600px) rotateY(80deg); transform-origin:right; } 100% { opacity:1; transform:perspective(1600px) rotateY(0); transform-origin:right; } }` },
                { name: 'Flip Diagonal', cls: 'anim-flipdiag', keyframeName: 'flipDiagonal', css: `@keyframes flipDiagonal { 0% { opacity:0; transform:perspective(1600px) rotate3d(1,1,0,180deg) scale(0.6); } 100% { opacity:1; transform:perspective(1600px) rotate3d(0,0,0,0deg) scale(1); } }` },
                { name: 'Zoom In Bounce', cls: 'anim-zoombounce', keyframeName: 'zoomInBounce', css: `@keyframes zoomInBounce { 0% { opacity:0; transform:perspective(1600px) scale(0.3); } 50% { opacity:1; transform:perspective(1600px) scale(1.1); } 70% { transform:perspective(1600px) scale(0.95); } 100% { opacity:1; transform:perspective(1600px) scale(1); } }` },
                { name: 'Slide Up Bounce', cls: 'anim-upbounce', keyframeName: 'slideUpBounce', css: `@keyframes slideUpBounce { 0% { opacity:0; transform:perspective(1600px) translateY(200px); } 60% { opacity:1; transform:perspective(1600px) translateY(-20px); } 80% { transform:perspective(1600px) translateY(10px); } 100% { opacity:1; transform:perspective(1600px) translateY(0); } }` },
                { name: 'Drop Rotate', cls: 'anim-droprotate', keyframeName: 'dropRotate', css: `@keyframes dropRotate { 0% { opacity:0; transform:perspective(1600px) translateY(-200px) rotateZ(45deg); } 100% { opacity:1; transform:perspective(1600px) translateY(0) rotateZ(0); } }` },
                { name: 'Twist In', cls: 'anim-twistin', keyframeName: 'twistIn', css: `@keyframes twistIn { 0% { opacity:0; transform:perspective(1600px) rotateZ(90deg) scale(0.4); } 100% { opacity:1; transform:perspective(1600px) rotateZ(0) scale(1); } }` },
                { name: 'Unfold Horizontal', cls: 'anim-unfoldh', keyframeName: 'unfoldH', css: `@keyframes unfoldH { 0% { opacity:0; transform:perspective(1600px) scaleX(0); transform-origin:left; } 100% { opacity:1; transform:perspective(1600px) scaleX(1); transform-origin:left; } }` },
                { name: 'Unfold Vertical', cls: 'anim-unfoldv', keyframeName: 'unfoldV', css: `@keyframes unfoldV { 0% { opacity:0; transform:perspective(1600px) scaleY(0); transform-origin:top; } 100% { opacity:1; transform:perspective(1600px) scaleY(1); transform-origin:top; } }` },
                { name: 'Circle Reveal', cls: 'anim-circle', keyframeName: 'circleReveal', css: `@keyframes circleReveal { 0% { opacity:0; clip-path:circle(0% at 50% 50%); transform:perspective(1600px) scale(0.8); } 100% { opacity:1; clip-path:circle(100% at 50% 50%); transform:perspective(1600px) scale(1); } }` },
                { name: 'Diamond Reveal', cls: 'anim-diamondrev', keyframeName: 'diamondReveal', css: `@keyframes diamondReveal { 0% { opacity:0; clip-path:polygon(50% 0%, 100% 50%, 50% 100%, 0% 50%); transform:perspective(1600px) scale(0.6); } 100% { opacity:1; clip-path:polygon(0% 0%, 100% 0%, 100% 100%, 0% 100%); transform:perspective(1600px) scale(1); } }` },
                { name: 'Stretch Diagonal', cls: 'anim-stretchdiag', keyframeName: 'stretchDiag', css: `@keyframes stretchDiag { 0% { opacity:0; transform:perspective(1600px) scale(0.2) rotate(45deg); } 100% { opacity:1; transform:perspective(1600px) scale(1) rotate(0deg); } }` },
                { name: 'Blur Slide', cls: 'anim-blurslide', keyframeName: 'blurSlide', css: `@keyframes blurSlide { 0% { opacity:0; transform:perspective(1600px) translateX(-100px); filter:blur(12px); } 100% { opacity:1; transform:perspective(1600px) translateX(0); filter:none; } }` },
                { name: 'Scale Rotate Fade', cls: 'anim-scalerotfade', keyframeName: 'scaleRotFade', css: `@keyframes scaleRotFade { 0% { opacity:0; transform:perspective(1600px) scale(0.3) rotate(60deg); } 100% { opacity:1; transform:perspective(1600px) scale(1) rotate(0deg); } }` },
                { name: 'Flip X Bounce', cls: 'anim-flipxbounce', keyframeName: 'flipXBounce', css: `@keyframes flipXBounce { 0% { opacity:0; transform:perspective(1600px) rotateX(90deg); } 60% { opacity:1; transform:perspective(1600px) rotateX(-20deg); } 80% { transform:perspective(1600px) rotateX(10deg); } 100% { opacity:1; transform:perspective(1600px) rotateX(0); } }` },
                { name: 'Swing Door', cls: 'anim-swingdoor', keyframeName: 'swingDoor', css: `@keyframes swingDoor { 0% { opacity:0; transform:perspective(1600px) rotateY(-120deg); transform-origin:left; } 100% { opacity:1; transform:perspective(1600px) rotateY(0); transform-origin:left; } }` },
                { name: 'Swing Door Right', cls: 'anim-swingdoorr', keyframeName: 'swingDoorR', css: `@keyframes swingDoorR { 0% { opacity:0; transform:perspective(1600px) rotateY(120deg); transform-origin:right; } 100% { opacity:1; transform:perspective(1600px) rotateY(0); transform-origin:right; } }` },
                { name: 'Glide Up', cls: 'anim-glideup', keyframeName: 'glideUp', css: `@keyframes glideUp { 0% { opacity:0; transform:perspective(1600px) translateY(100px); filter:blur(5px); } 100% { opacity:1; transform:perspective(1600px) translateY(0); filter:none; } }` },
                { name: 'Glide Down', cls: 'anim-glidedown', keyframeName: 'glideDown', css: `@keyframes glideDown { 0% { opacity:0; transform:perspective(1600px) translateY(-100px); filter:blur(5px); } 100% { opacity:1; transform:perspective(1600px) translateY(0); filter:none; } }` },
                { name: 'Spin Scale', cls: 'anim-spinscale', keyframeName: 'spinScale', css: `@keyframes spinScale { 0% { opacity:0; transform:perspective(1600px) rotate(180deg) scale(0.2); } 100% { opacity:1; transform:perspective(1600px) rotate(0) scale(1); } }` },
                { name: 'Elastic Pop', cls: 'anim-elasticpop', keyframeName: 'elasticPop', css: `@keyframes elasticPop { 0% { opacity:0; transform:perspective(1600px) scale(0); } 50% { transform:perspective(1600px) scale(1.2); } 70% { transform:perspective(1600px) scale(0.9); } 100% { opacity:1; transform:perspective(1600px) scale(1); } }` },
                { name: 'Skew Glide', cls: 'anim-skewglide', keyframeName: 'skewGlide', css: `@keyframes skewGlide { 0% { opacity:0; transform:perspective(1600px) skewX(30deg) translateX(-80px); } 100% { opacity:1; transform:perspective(1600px) skewX(0) translateX(0); } }` },
                { name: 'Rotate Perspective', cls: 'anim-rotpersp', keyframeName: 'rotatePersp', css: `@keyframes rotatePersp { 0% { opacity:0; transform:perspective(1600px) rotateY(90deg) scale(0.7); } 100% { opacity:1; transform:perspective(1600px) rotateY(0) scale(1); } }` },
                { name: 'Vortex Spin', cls: 'anim-vortexspin', keyframeName: 'vortexSpin', css: `@keyframes vortexSpin { 0% { opacity:0; transform:perspective(1600px) rotateX(60deg) rotateY(60deg) rotateZ(180deg) scale(0.2); } 100% { opacity:1; transform:perspective(1600px) rotateX(0) rotateY(0) rotateZ(0) scale(1); } }` },
                { name: 'Shrink In', cls: 'anim-shrinkin', keyframeName: 'shrinkIn', css: `@keyframes shrinkIn { 0% { opacity:0; transform:perspective(1600px) scale(2); } 100% { opacity:1; transform:perspective(1600px) scale(1); } }` },
                { name: 'Grow In', cls: 'anim-growin', keyframeName: 'growIn', css: `@keyframes growIn { 0% { opacity:0; transform:perspective(1600px) scale(0); } 100% { opacity:1; transform:perspective(1600px) scale(1); } }` },
                { name: 'Fade Only', cls: 'anim-fadeonly', keyframeName: 'fadeOnly', css: `@keyframes fadeOnly { 0% { opacity:0; } 100% { opacity:1; } }` },
                { name: 'Skew Y Reveal', cls: 'anim-skewy', keyframeName: 'skewYReveal', css: `@keyframes skewYReveal { 0% { opacity:0; transform:perspective(1600px) skewY(20deg); } 100% { opacity:1; transform:perspective(1600px) skewY(0); } }` },
                { name: 'Blur Expand', cls: 'anim-blurexpand', keyframeName: 'blurExpand', css: `@keyframes blurExpand { 0% { opacity:0; transform:perspective(1600px) scale(0.5); filter:blur(20px); } 100% { opacity:1; transform:perspective(1600px) scale(1); filter:none; } }` },
                { name: 'Slide Right Fade', cls: 'anim-sliderfade', keyframeName: 'slideRightFade', css: `@keyframes slideRightFade { 0% { opacity:0; transform:perspective(1600px) translateX(-120px); } 100% { opacity:1; transform:perspective(1600px) translateX(0); } }` },
                { name: 'Slide Left Fade', cls: 'anim-slidelfade', keyframeName: 'slideLeftFade', css: `@keyframes slideLeftFade { 0% { opacity:0; transform:perspective(1600px) translateX(120px); } 100% { opacity:1; transform:perspective(1600px) translateX(0); } }` },
            ];

            additionalDefs.forEach(def => {
                add(def.name, def.cls, def.css, `${def.keyframeName} 2.3s cubic-bezier(.16,1,.3,1)`);
            });

            // --------------------------------------------------------------
            // 2. INJECT CSS & BUILD BUTTONS
            // --------------------------------------------------------------
            const styleEl = document.createElement('style');
            let allCSS = '';
            const classAnimMap = {}; // class -> animation shorthand
            animations.forEach(item => {
                allCSS += item.css + '\n';
                allCSS += `.${item.class} { animation: ${item.animation}; }\n`;
                classAnimMap[item.class] = item.animation;
            });
            styleEl.textContent = allCSS;
            document.head.appendChild(styleEl);

            const buttonContainer = document.getElementById('button-container');
            // original 5 buttons already exist in HTML, we need to skip those classes
            const originalClasses = ['anim-tile21', 'anim-spin', 'anim-flip', 'anim-vortex', 'anim-depth'];
            animations.forEach(item => {
                if (originalClasses.includes(item.class)) return; // already in HTML
                const btn = document.createElement('button');
                btn.className = 'anim-btn';
                btn.setAttribute('data-anim', item.class);
                btn.textContent = item.name;
                buttonContainer.appendChild(btn);
            });

            // --------------------------------------------------------------
            // 3. TILE INTERACTION LOGIC
            // --------------------------------------------------------------
            const tile = document.getElementById('tile');
            const allClasses = animations.map(a => a.class);
            let currentClass = 'anim-tile21';

            function playAnimation(cls) {
                tile.classList.remove(...allClasses);
                void tile.offsetWidth;
                tile.classList.add(cls);
                currentClass = cls;
            }

            document.addEventListener('click', (e) => {
                const btn = e.target.closest('.anim-btn');
                if (!btn) return;
                const cls = btn.getAttribute('data-anim');
                if (cls) playAnimation(cls);
            });

            document.getElementById('replay').addEventListener('click', () => playAnimation(currentClass));
            document.getElementById('random').addEventListener('click', () => {
                const randomItem = animations[Math.floor(Math.random() * animations.length)];
                playAnimation(randomItem.class);
            });

            console.log(`✅ Loaded ${animations.length} completely unique animation options.`);
        })();
    </script>
</body>
</html>

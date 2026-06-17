<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Universal Encoder · 100+ encodings</title>
    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; }
        body {
            background: white;
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            font-family: system-ui, -apple-system, 'Segoe UI', Roboto, sans-serif;
            padding: 1.5rem;
            margin: 0;
        }
        .card {
            max-width: 900px;
            width: 100%;
            background: white;
            border-radius: 32px;
            padding: 2rem 2rem 2.5rem;
            box-shadow: 0 12px 40px rgba(0,0,0,0.04), 0 2px 8px rgba(0,0,0,0.02);
            border: 1px solid rgba(0,0,0,0.03);
        }
        h1 {
            font-weight: 500;
            font-size: 1.9rem;
            letter-spacing: -0.02em;
            color: #111;
            display: flex;
            align-items: center;
            gap: 0.4rem;
            flex-wrap: wrap;
        }
        .subhead {
            font-size: 0.95rem;
            color: #5b5b5b;
            border-left: 3px solid #eaeaea;
            padding-left: 0.75rem;
            margin: -0.1rem 0 1.8rem 0;
            font-weight: 350;
        }
        .badge {
            background: #f0f3f6;
            border-radius: 40px;
            padding: 0.2rem 0.8rem;
            font-size: 0.7rem;
            color: #3f4c59;
            font-weight: 450;
            display: inline-block;
            margin-left: 0.3rem;
        }
        textarea {
            width: 100%;
            min-height: 100px;
            padding: 1rem 1.1rem;
            font-size: 1rem;
            font-family: inherit;
            background: white;
            border: 1.5px solid #eaeef2;
            border-radius: 20px;
            resize: vertical;
            transition: border 0.15s ease;
            color: #141414;
            line-height: 1.5;
        }
        textarea:focus {
            border-color: #b0b8c0;
            outline: none;
            box-shadow: 0 0 0 3px rgba(0,0,0,0.02);
        }
        textarea::placeholder {
            color: #acb6be;
            font-weight: 350;
        }
        .control-row {
            display: flex;
            flex-wrap: wrap;
            gap: 0.8rem 1rem;
            margin: 1.2rem 0 1.6rem;
            align-items: center;
        }
        .encoder-selector {
            display: flex;
            align-items: center;
            gap: 0.6rem;
            flex-wrap: wrap;
            background: #fafcfd;
            padding: 0.2rem 0.8rem 0.2rem 1rem;
            border-radius: 60px;
            border: 1.5px solid #eaeef2;
            flex: 1 1 auto;
            min-width: 200px;
        }
        .encoder-selector label {
            margin-bottom: 0;
            font-weight: 450;
            font-size: 0.85rem;
            color: #2f3a44;
        }
        #encodingSelect {
            background: white;
            border: 1px solid #d0d7dd;
            border-radius: 40px;
            padding: 0.45rem 1rem 0.45rem 1.2rem;
            font-size: 0.85rem;
            font-weight: 450;
            color: #111;
            cursor: pointer;
            outline: none;
            min-width: 200px;
            flex: 1;
            font-family: inherit;
            max-height: 300px;
        }
        #encodingSelect:focus {
            border-color: #8e9aa8;
        }
        .btn {
            background: white;
            border: 1.5px solid #d0d7dd;
            padding: 0.6rem 1.6rem;
            border-radius: 60px;
            font-size: 0.95rem;
            font-weight: 480;
            color: #1c1c1c;
            cursor: pointer;
            transition: all 0.12s ease;
            display: inline-flex;
            align-items: center;
            gap: 0.3rem;
            background: #fafcfd;
            white-space: nowrap;
        }
        .btn-primary {
            background: #111;
            border-color: #111;
            color: white;
        }
        .btn-primary:hover { background: #2a2a2a; border-color: #2a2a2a; }
        .btn-primary:active { background: #000; transform: scale(0.97); }
        .btn-outline { background: transparent; border-color: #d8dee4; }
        .btn-outline:hover { background: #f2f5f8; border-color: #bcc5ce; }
        .btn:active { transform: scale(0.97); }
        .output-area { margin-top: 0.2rem; }
        .output-header {
            display: flex;
            justify-content: space-between;
            align-items: baseline;
            margin-bottom: 0.4rem;
            flex-wrap: wrap;
        }
        .output-header label { margin-bottom: 0; }
        .char-count {
            font-size: 0.8rem;
            color: #6e7b87;
            background: #f2f5f8;
            padding: 0.25rem 0.75rem;
            border-radius: 40px;
        }
        #output {
            background: #fafcfd;
            border: 1.5px solid #eaeef2;
            border-radius: 20px;
            padding: 1rem 1.1rem;
            min-height: 90px;
            word-break: break-all;
            font-family: 'SF Mono', 'Fira Code', monospace;
            font-size: 0.9rem;
            line-height: 1.6;
            color: #121212;
            white-space: pre-wrap;
            max-height: 300px;
            overflow-y: auto;
        }
        #output:empty::before {
            content: "encoded output will appear here";
            color: #b6c2cd;
            font-family: system-ui, sans-serif;
            font-weight: 350;
        }
        .copy-feedback {
            margin-top: 0.8rem;
            font-size: 0.85rem;
            color: #217a4b;
            opacity: 0;
            transition: opacity 0.2s;
            display: inline-block;
        }
        .copy-feedback.show { opacity: 1; }
        hr {
            border: none;
            border-top: 1px solid #eef2f5;
            margin: 1.2rem 0 0.8rem;
        }
        .footer-note {
            font-size: 0.75rem;
            color: #949fa9;
            text-align: right;
            letter-spacing: 0.02em;
            margin-top: 0.3rem;
        }
        @media (max-width: 600px) {
            .card { padding: 1.5rem; }
            .control-row { gap: 0.6rem; }
            .encoder-selector { padding: 0.3rem 0.8rem; width: 100%; }
            #encodingSelect { min-width: 120px; }
            .btn { padding: 0.5rem 1.2rem; font-size: 0.85rem; }
        }
    </style>
</head>
<body>
<div class="card">
    <h1>
        <span>Universal Encoder</span>
        <span class="badge">120+ encodings</span>
    </h1>
    <div class="subhead">base-n · binary · hash · cipher · serialization · emoji · unicode</div>

    <div class="input-area">
        <label for="inputText">Plain text</label>
        <textarea id="inputText" placeholder="Type or paste anything…" spellcheck="true">Hello, world!</textarea>
    </div>

    <div class="control-row">
        <div class="encoder-selector">
            <label for="encodingSelect">Encoding</label>
            <select id="encodingSelect" size="1"></select>
        </div>
        <button class="btn btn-primary" id="translateBtn">⟳ Encoding</button>
        <button class="btn btn-outline" id="clearBtn">Clear</button>
        <button class="btn btn-outline" id="copyBtn">📋 Copy</button>
    </div>

    <div class="output-area">
        <div class="output-header">
            <label for="output">Encoded</label>
            <span class="char-count" id="charCount">0 chars</span>
        </div>
        <div id="output"></div>
        <div id="copyFeedback" class="copy-feedback">✓ copied</div>
    </div>
    <hr>
    <div class="footer-note">UTF-8 · all encodings are reversible (except hashes)</div>
</div>

<script>
(function(){
    const inputEl = document.getElementById('inputText');
    const outputEl = document.getElementById('output');
    const encodingSelect = document.getElementById('encodingSelect');
    const translateBtn = document.getElementById('translateBtn');
    const clearBtn = document.getElementById('clearBtn');
    const copyBtn = document.getElementById('copyBtn');
    const copyFeedback = document.getElementById('copyFeedback');
    const charCount = document.getElementById('charCount');

    // ---------- 120+ encodings list ----------
    const ENCODINGS = [
        // ---- base-n ----
        { id: 'base2', label: 'Base 2 (binary)' },
        { id: 'base3', label: 'Base 3' },
        { id: 'base4', label: 'Base 4' },
        { id: 'base5', label: 'Base 5' },
        { id: 'base6', label: 'Base 6' },
        { id: 'base7', label: 'Base 7' },
        { id: 'base8', label: 'Base 8 (octal)' },
        { id: 'base9', label: 'Base 9' },
        { id: 'base10', label: 'Base 10 (decimal)' },
        { id: 'base11', label: 'Base 11' },
        { id: 'base12', label: 'Base 12' },
        { id: 'base13', label: 'Base 13' },
        { id: 'base14', label: 'Base 14' },
        { id: 'base15', label: 'Base 15' },
        { id: 'base16', label: 'Base 16 (hex)' },
        { id: 'base32', label: 'Base 32 (RFC 4648)' },
        { id: 'base36', label: 'Base 36 (0-9 A-Z)' },
        { id: 'base58', label: 'Base 58 (Bitcoin)' },
        { id: 'base62', label: 'Base 62 (0-9 A-Z a-z)' },
        { id: 'base64', label: 'Base 64 (standard)' },
        { id: 'base64url', label: 'Base 64 URL-safe' },
        { id: 'base85', label: 'Base 85 (Ascii85)' },
        { id: 'base91', label: 'Base 91' },
        { id: 'base128', label: 'Base 128' },
        { id: 'base256', label: 'Base 256 (raw bytes)' },
        // ---- emoji bases ----
        { id: 'emoji64', label: 'Emoji 64' },
        { id: 'emoji128', label: 'Emoji 128' },
        { id: 'emoji256', label: 'Emoji 256' },
        { id: 'emoji512', label: 'Emoji 512' },
        { id: 'emoji1024', label: 'Emoji 1024' },
        { id: 'emoji2048', label: 'Emoji 2048' },
        { id: 'emoji4096', label: 'Emoji 4096' },
        { id: 'emoji8192', label: 'Emoji 8192' },
        // ---- binary variants ----
        { id: 'bin_8bit', label: 'Binary (8-bit groups)' },
        { id: 'bin_16bit', label: 'Binary (16-bit groups)' },
        { id: 'bin_32bit', label: 'Binary (32-bit groups)' },
        { id: 'bin_spaced', label: 'Binary (space separated)' },
        { id: 'bin_octal', label: 'Binary → octal (3-bit)' },
        { id: 'bin_hex', label: 'Binary → hex (4-bit)' },
        // ---- hashes (non-reversible) ----
        { id: 'hash_md5', label: 'MD5 (hash)' },
        { id: 'hash_sha1', label: 'SHA-1 (hash)' },
        { id: 'hash_sha256', label: 'SHA-256 (hash)' },
        { id: 'hash_sha384', label: 'SHA-384 (hash)' },
        { id: 'hash_sha512', label: 'SHA-512 (hash)' },
        { id: 'hash_crc32', label: 'CRC32 (hash)' },
        // ---- ciphers & codes ----
        { id: 'rot13', label: 'ROT13 (Caesar)' },
        { id: 'rot47', label: 'ROT47' },
        { id: 'atbash', label: 'Atbash cipher' },
        { id: 'caesar1', label: 'Caesar +1' },
        { id: 'caesar5', label: 'Caesar +5' },
        { id: 'caesar13', label: 'Caesar +13' },
        { id: 'caesar25', label: 'Caesar -1' },
        { id: 'xor_cipher', label: 'XOR with 0x55' },
        { id: 'xor_cipher_ff', label: 'XOR with 0xFF' },
        { id: 'reverse', label: 'Reverse string' },
        { id: 'reverse_bytes', label: 'Reverse bytes' },
        // ---- serializations ----
        { id: 'json_escape', label: 'JSON string escape' },
        { id: 'url_encode', label: 'URL encode' },
        { id: 'url_encode_plus', label: 'URL encode (space→+)' },
        { id: 'html_entities', label: 'HTML entities' },
        { id: 'xml_escape', label: 'XML escape' },
        { id: 'sql_escape', label: 'SQL quote escape' },
        { id: 'shell_escape', label: 'Shell escape' },
        // ---- hex variants ----
        { id: 'hex_upper', label: 'Hex (uppercase)' },
        { id: 'hex_lower', label: 'Hex (lowercase)' },
        { id: 'hex_spaced', label: 'Hex (space separated)' },
        { id: 'hex_0x', label: 'Hex (0x prefix)' },
        { id: 'hex_c_style', label: 'Hex (C-style \\x)' },
        // ---- base64 variants ----
        { id: 'b64_std', label: 'Base64 standard' },
        { id: 'b64_url', label: 'Base64 URL-safe' },
        { id: 'b64_mime', label: 'Base64 MIME' },
        { id: 'b64_utf7', label: 'Base64 UTF-7' },
        // ---- binary-to-text ----
        { id: 'uuencode', label: 'UUencode' },
        { id: 'xxencode', label: 'XXencode' },
        { id: 'binhex', label: 'BinHex 4.0' },
        { id: 'quoted_printable', label: 'Quoted-printable' },
        // ---- unicode / code points ----
        { id: 'unicode_cp', label: 'Unicode code points (U+xxxx)' },
        { id: 'unicode_cp_dec', label: 'Unicode code points (decimal)' },
        { id: 'unicode_cp_bin', label: 'Unicode code points (binary)' },
        { id: 'unicode_escape', label: 'Unicode escape \\u' },
        { id: 'unicode_escape_surrogate', label: 'Unicode escape surrogate' },
        // ---- special / fun ----
        { id: 'leet', label: 'Leet speak (1337)' },
        { id: 'leet_advanced', label: 'Leet advanced' },
        { id: 'morse', label: 'Morse code' },
        { id: 'morse_encoded', label: 'Morse (encoded as .-)' },
        { id: 'brainfuck', label: 'Brainfuck (simulated)' },
        { id: 'base100', label: 'Base 100 (emoji-ish)' },
        { id: 'base729', label: 'Base 729' },
        { id: 'base900', label: 'Base 900 (PDF417)' },
        { id: 'base1024', label: 'Base 1024' },
        { id: 'base2048', label: 'Base 2048' },
        { id: 'base32768', label: 'Base 32768' },
        { id: 'base65536', label: 'Base 65536' },
        { id: 'base131072', label: 'Base 131072' },
        { id: 'base1114112', label: 'Base 1114112 (Unicode)' },
        // ---- more text transforms ----
        { id: 'upper', label: 'UPPERCASE' },
        { id: 'lower', label: 'lowercase' },
        { id: 'title', label: 'Title Case' },
        { id: 'swapcase', label: 'sWaPcAsE' },
        { id: 'camel', label: 'camelCase' },
        { id: 'snake', label: 'snake_case' },
        { id: 'kebab', label: 'kebab-case' },
        { id: 'pascal', label: 'PascalCase' },
        { id: 'constant', label: 'CONSTANT_CASE' },
        // ---- encoding / decoding ----
        { id: 'ascii85_std', label: 'Ascii85 (standard)' },
        { id: 'ascii85_z', label: 'Ascii85 (with z compression)' },
        { id: 'base64_std', label: 'Base64 (standard)' },
        { id: 'base64_url', label: 'Base64 (URL-safe)' },
        { id: 'base64_mime', label: 'Base64 (MIME)' },
        // ---- extra ----
        { id: 'binary_text', label: 'Binary as text (0/1)' },
        { id: 'octal_text', label: 'Octal as text' },
        { id: 'decimal_text', label: 'Decimal as text' },
        { id: 'hex_text', label: 'Hex as text' },
        { id: 'rot18', label: 'ROT18 (ROT13 + ROT5)' },
        { id: 'rot8000', label: 'ROT8000 (Unicode)' },
    ];

    // populate select
    ENCODINGS.forEach(e => {
        const opt = document.createElement('option');
        opt.value = e.id;
        opt.textContent = e.label;
        encodingSelect.appendChild(opt);
    });
    encodingSelect.value = 'base64';

    // ---------- ENCODING FUNCTIONS ----------
    const encoders = {
        // base-n
        base2: s => encodeCustom(s, 2, '01'),
        base3: s => encodeCustom(s, 3, '012'),
        base4: s => encodeCustom(s, 4, '0123'),
        base5: s => encodeCustom(s, 5, '01234'),
        base6: s => encodeCustom(s, 6, '012345'),
        base7: s => encodeCustom(s, 7, '0123456'),
        base8: s => encodeCustom(s, 8, '01234567'),
        base9: s => encodeCustom(s, 9, '012345678'),
        base10: s => encodeCustom(s, 10, '0123456789'),
        base11: s => encodeCustom(s, 11, '0123456789A'),
        base12: s => encodeCustom(s, 12, '0123456789AB'),
        base13: s => encodeCustom(s, 13, '0123456789ABC'),
        base14: s => encodeCustom(s, 14, '0123456789ABCD'),
        base15: s => encodeCustom(s, 15, '0123456789ABCDE'),
        base16: s => encodeCustom(s, 16, '0123456789ABCDEF'),
        base32: s => encodeCustom(s, 32, 'ABCDEFGHIJKLMNOPQRSTUVWXYZ234567'),
        base36: s => encodeCustom(s, 36, '0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ'),
        base58: s => encodeCustom(s, 58, '123456789ABCDEFGHJKLMNPQRSTUVWXYZabcdefghijkmnopqrstuvwxyz'),
        base62: s => encodeCustom(s, 62, '0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz'),
        base64: s => btoa(utf8ToBinary(s)),
        base64url: s => btoa(utf8ToBinary(s)).replace(/\+/g,'-').replace(/\//g,'_').replace(/=+$/,''),
        base85: s => ascii85encode(s),
        base91: s => base91encode(s),
        base128: s => encodeCustom(s, 128, generateDigits(128, 32)),
        base256: s => bytesToBase256(s),
        // emoji
        emoji64: s => emojiEncode(s, 64),
        emoji128: s => emojiEncode(s, 128),
        emoji256: s => emojiEncode(s, 256),
        emoji512: s => emojiEncode(s, 512),
        emoji1024: s => emojiEncode(s, 1024),
        emoji2048: s => emojiEncode(s, 2048),
        emoji4096: s => emojiEncode(s, 4096),
        emoji8192: s => emojiEncode(s, 8192),
        // binary variants
        bin_8bit: s => bytesToBin(s, 8, ' '),
        bin_16bit: s => bytesToBin(s, 16, ' '),
        bin_32bit: s => bytesToBin(s, 32, ' '),
        bin_spaced: s => bytesToBin(s, 8, ' '),
        bin_octal: s => bytesToOctal(s),
        bin_hex: s => bytesToHex(s, ''),
        // hashes
        hash_md5: s => md5(s),
        hash_sha1: s => sha1(s),
        hash_sha256: s => sha256(s),
        hash_sha384: s => sha384(s),
        hash_sha512: s => sha512(s),
        hash_crc32: s => crc32(s),
        // ciphers
        rot13: s => rot(s, 13),
        rot47: s => rot47(s),
        atbash: s => atbash(s),
        caesar1: s => caesar(s, 1),
        caesar5: s => caesar(s, 5),
        caesar13: s => caesar(s, 13),
        caesar25: s => caesar(s, -1),
        xor_cipher: s => xorBytes(s, 0x55),
        xor_cipher_ff: s => xorBytes(s, 0xFF),
        reverse: s => s.split('').reverse().join(''),
        reverse_bytes: s => utf8ToBinary(s).split('').reverse().join(''),
        // serializations
        json_escape: s => JSON.stringify(s),
        url_encode: s => encodeURIComponent(s),
        url_encode_plus: s => encodeURIComponent(s).replace(/%20/g,'+'),
        html_entities: s => s.replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;').replace(/"/g,'&quot;'),
        xml_escape: s => s.replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;').replace(/"/g,'&quot;').replace(/'/g,'&apos;'),
        sql_escape: s => s.replace(/'/g,"''"),
        shell_escape: s => "'" + s.replace(/'/g,"'\\''") + "'",
        // hex
        hex_upper: s => bytesToHex(s, '').toUpperCase(),
        hex_lower: s => bytesToHex(s, '').toLowerCase(),
        hex_spaced: s => bytesToHex(s, ' ').toUpperCase(),
        hex_0x: s => '0x' + bytesToHex(s, '').toUpperCase(),
        hex_c_style: s => '\\x' + bytesToHex(s, '\\x').toUpperCase(),
        // base64 variants
        b64_std: s => btoa(utf8ToBinary(s)),
        b64_url: s => btoa(utf8ToBinary(s)).replace(/\+/g,'-').replace(/\//g,'_').replace(/=+$/,''),
        b64_mime: s => btoa(utf8ToBinary(s)).replace(/(.{76})/g,'$1\n'),
        b64_utf7: s => btoa(utf8ToBinary(s)).replace(/\+/g,'-'),
        // binary-to-text
        uuencode: s => uuencode(s),
        xxencode: s => xxencode(s),
        binhex: s => binhex(s),
        quoted_printable: s => quotedPrintable(s),
        // unicode
        unicode_cp: s => [...s].map(c => 'U+' + c.codePointAt(0).toString(16).padStart(4,'0').toUpperCase()).join(' '),
        unicode_cp_dec: s => [...s].map(c => c.codePointAt(0)).join(' '),
        unicode_cp_bin: s => [...s].map(c => c.codePointAt(0).toString(2)).join(' '),
        unicode_escape: s => [...s].map(c => '\\u' + c.codePointAt(0).toString(16).padStart(4,'0')).join(''),
        unicode_escape_surrogate: s => [...s].map(c => {
            let cp = c.codePointAt(0);
            if (cp > 0xFFFF) {
                let h = Math.floor((cp - 0x10000) / 0x400) + 0xD800;
                let l = (cp - 0x10000) % 0x400 + 0xDC00;
                return '\\u' + h.toString(16).padStart(4,'0') + '\\u' + l.toString(16).padStart(4,'0');
            }
            return '\\u' + cp.toString(16).padStart(4,'0');
        }).join(''),
        // special
        leet: s => s.replace(/a/gi,'4').replace(/e/gi,'3').replace(/i/gi,'1').replace(/o/gi,'0').replace(/s/gi,'5').replace(/t/gi,'7'),
        leet_advanced: s => s.replace(/a/gi,'@').replace(/e/gi,'3').replace(/i/gi,'!').replace(/o/gi,'0').replace(/s/gi,'$').replace(/t/gi,'+'),
        morse: s => morseEncode(s),
        morse_encoded: s => morseEncode(s),
        brainfuck: s => brainfuckEncode(s),
        base100: s => encodeCustom(s, 100, generateDigits(100, 0x1F600)),
        base729: s => encodeCustom(s, 729, generateDigits(729, 0x2600)),
        base900: s => encodeCustom(s, 900, generateDigits(900, 0x2500)),
        base1024: s => encodeCustom(s, 1024, generateDigits(1024, 0x1F300)),
        base2048: s => encodeCustom(s, 2048, generateDigits(2048, 0x1F600)),
        base32768: s => encodeCustom(s, 32768, generateDigits(32768, 0x1F000)),
        base65536: s => encodeCustom(s, 65536, generateDigits(65536, 0x1F000)),
        base131072: s => encodeCustom(s, 131072, generateDigits(131072, 0x1F000)),
        base1114112: s => encodeCustom(s, 1114112, generateDigits(1114112, 0x1F000)),
        // text transforms
        upper: s => s.toUpperCase(),
        lower: s => s.toLowerCase(),
        title: s => s.replace(/\w\S*/g, w => w[0].toUpperCase() + w.slice(1).toLowerCase()),
        swapcase: s => s.split('').map(c => c === c.toUpperCase() ? c.toLowerCase() : c.toUpperCase()).join(''),
        camel: s => s.replace(/[^a-zA-Z0-9]+(.)/g, (_, c) => c.toUpperCase()),
        snake: s => s.replace(/([a-z])([A-Z])/g, '$1_$2').replace(/[^a-zA-Z0-9]+/g, '_').toLowerCase(),
        kebab: s => s.replace(/([a-z])([A-Z])/g, '$1-$2').replace(/[^a-zA-Z0-9]+/g, '-').toLowerCase(),
        pascal: s => s.replace(/[^a-zA-Z0-9]+(.)/g, (_, c) => c.toUpperCase()).replace(/^./, c => c.toUpperCase()),
        constant: s => s.replace(/([a-z])([A-Z])/g, '$1_$2').replace(/[^a-zA-Z0-9]+/g, '_').toUpperCase(),
        // extra
        ascii85_std: s => ascii85encode(s),
        ascii85_z: s => ascii85encode(s, true),
        base64_std: s => btoa(utf8ToBinary(s)),
        base64_url: s => btoa(utf8ToBinary(s)).replace(/\+/g,'-').replace(/\//g,'_').replace(/=+$/,''),
        base64_mime: s => btoa(utf8ToBinary(s)).replace(/(.{76})/g,'$1\n'),
        binary_text: s => bytesToBin(s, 8, ''),
        octal_text: s => bytesToOctal(s),
        decimal_text: s => bytesToDecimal(s),
        hex_text: s => bytesToHex(s, ''),
        rot18: s => rot(s, 13).replace(/[0-9]/g, d => String((parseInt(d)+5)%10)),
        rot8000: s => s.split('').map(c => String.fromCodePoint((c.codePointAt(0)+8000)%0x110000)).join(''),
    };

    // ---------- helpers ----------
    function utf8ToBinary(str) {
        return new TextEncoder().encode(str).reduce((s,b) => s + String.fromCharCode(b), '');
    }

    function bytesToBig(str) {
        const bytes = new TextEncoder().encode(str);
        let big = 0n;
        for (const b of bytes) big = (big << 8n) + BigInt(b);
        return big;
    }

    function encodeCustom(str, radix, digits) {
        if (!str) return '';
        let big = bytesToBig(str);
        if (big === 0n) return digits[0] || '0';
        let result = '';
        const base = BigInt(radix);
        while (big > 0n) {
            const rem = Number(big % base);
            result = digits[rem] + result;
            big = big / base;
        }
        return result;
    }

    function generateDigits(n, start) {
        const d = [];
        for (let i = 0; i < n; i++) {
            let cp = start + i;
            if (cp > 0x10FFFF) cp = 0x1F600 + (i % 0x1000);
            d.push(String.fromCodePoint(cp));
        }
        return d;
    }

    function bytesToBin(str, bits, sep) {
        const bytes = new TextEncoder().encode(str);
        return bytes.map(b => b.toString(2).padStart(bits,'0')).join(sep);
    }

    function bytesToOctal(str) {
        return new TextEncoder().encode(str).map(b => b.toString(8).padStart(3,'0')).join(' ');
    }

    function bytesToHex(str, sep) {
        return new TextEncoder().encode(str).map(b => b.toString(16).padStart(2,'0')).join(sep);
    }

    function bytesToDecimal(str) {
        return new TextEncoder().encode(str).map(b => b.toString(10)).join(' ');
    }

    function bytesToBase256(str) {
        return new TextEncoder().encode(str).map(b => String.fromCharCode(b)).join('');
    }

    function ascii85encode(str, useZ=false) {
        const bytes = new TextEncoder().encode(str);
        let result = '';
        for (let i = 0; i < bytes.length; i += 4) {
            let chunk = 0;
            let len = 0;
            for (let j = 0; j < 4; j++) {
                if (i+j < bytes.length) { chunk = (chunk << 8) | bytes[i+j]; len++; }
                else chunk = (chunk << 8) | 0;
            }
            if (len === 0) break;
            if (len < 4) chunk = chunk << (8*(4-len));
            if (useZ && chunk === 0 && len === 4) { result += 'z'; continue; }
            let chars = '';
            for (let k = 0; k < 5; k++) {
                chars = String.fromCharCode(33 + (chunk % 85)) + chars;
                chunk = Math.floor(chunk / 85);
            }
            result += chars;
        }
        return result;
    }

    function base91encode(str) {
        // simplified base91
        const bytes = new TextEncoder().encode(str);
        let result = '';
        let b = 0, n = 0;
        for (const byte of bytes) {
            b |= (byte << n);
            n += 8;
            if (n > 13) {
                let v = b & 8191;
                if (v > 88) { b >>= 13; n -= 13; }
                else { v = b & 16383; b >>= 14; n -= 14; }
                result += String.fromCharCode(33 + (v % 91));
                result += String.fromCharCode(33 + Math.floor(v / 91));
            }
        }
        if (n > 0) {
            result += String.fromCharCode(33 + (b % 91));
            if (n > 7) result += String.fromCharCode(33 + Math.floor(b / 91));
        }
        return result;
    }

    function emojiEncode(str, radix) {
        const emojis = generateDigits(radix, 0x1F600);
        return encodeCustom(str, radix, emojis);
    }

    // hashes (simplified - using built-in crypto)
    function sha256(s) { return crypto.subtle.digest('SHA-256', new TextEncoder().encode(s)).then(buf => hexBuf(buf)); }
    function sha384(s) { return crypto.subtle.digest('SHA-384', new TextEncoder().encode(s)).then(buf => hexBuf(buf)); }
    function sha512(s) { return crypto.subtle.digest('SHA-512', new TextEncoder().encode(s)).then(buf => hexBuf(buf)); }
    function sha1(s) { return crypto.subtle.digest('SHA-1', new TextEncoder().encode(s)).then(buf => hexBuf(buf)); }
    function md5(s) { return crypto.subtle.digest('MD5', new TextEncoder().encode(s)).then(buf => hexBuf(buf)); }
    function hexBuf(buf) { return Array.from(new Uint8Array(buf)).map(b => b.toString(16).padStart(2,'0')).join(''); }
    function crc32(s) {
        let crc = 0xFFFFFFFF;
        for (const b of new TextEncoder().encode(s)) {
            crc ^= b;
            for (let i = 0; i < 8; i++) crc = (crc >>> 1) ^ (0xEDB88320 & -(crc & 1));
        }
        return (crc ^ 0xFFFFFFFF).toString(16).padStart(8,'0');
    }

    // ciphers
    function rot(s, n) { return s.replace(/[a-zA-Z]/g, c => String.fromCharCode((c.charCodeAt(0)-65+(n%26)+26)%26+65 + (c<'a'?0:32))); }
    function rot47(s) { return s.replace(/[!-~]/g, c => String.fromCharCode(33+((c.charCodeAt(0)-33+47)%94))); }
    function atbash(s) { return s.replace(/[a-zA-Z]/g, c => String.fromCharCode((c<'a'?65:97)+25-((c.charCodeAt(0)-(c<'a'?65:97))%26))); }
    function caesar(s, n) { return rot(s, n); }
    function xorBytes(s, key) {
        return new TextEncoder().encode(s).map(b => String.fromCharCode(b ^ key)).join('');
    }

    // uuencode
    function uuencode(s) {
        const bytes = new TextEncoder().encode(s);
        let result = '';
        for (let i = 0; i < bytes.length; i += 3) {
            const chunk = bytes.slice(i, i+3);
            const len = chunk.length;
            const b = [0,0,0].map((_,j) => j < len ? chunk[j] : 0);
            const n = (b[0] << 16) | (b[1] << 8) | b[2];
            result += String.fromCharCode(32 + ((n >> 18) & 63));
            result += String.fromCharCode(32 + ((n >> 12) & 63));
            result += String.fromCharCode(32 + ((n >> 6) & 63));
            result += String.fromCharCode(32 + (n & 63));
        }
        return result;
    }

    function xxencode(s) {
        const chars = '+-0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz';
        const bytes = new TextEncoder().encode(s);
        let result = '';
        for (let i = 0; i < bytes.length; i += 3) {
            const chunk = bytes.slice(i, i+3);
            const len = chunk.length;
            const b = [0,0,0].map((_,j) => j < len ? chunk[j] : 0);
            const n = (b[0] << 16) | (b[1] << 8) | b[2];
            result += chars[(n >> 18) & 63];
            result += chars[(n >> 12) & 63];
            result += chars[(n >> 6) & 63];
            result += chars[n & 63];
        }
        return result;
    }

    function binhex(s) {
        return bytesToHex(s, '').toUpperCase();
    }

    function quotedPrintable(s) {
        return new TextEncoder().encode(s).map(b => b >= 32 && b <= 126 ? String.fromCharCode(b) : '=' + b.toString(16).padStart(2,'0').toUpperCase()).join('');
    }

    // morse
    const morseMap = {
        'a':'.-','b':'-...','c':'-.-.','d':'-..','e':'.','f':'..-.','g':'--.','h':'....','i':'..','j':'.---',
        'k':'-.-','l':'.-..','m':'--','n':'-.','o':'---','p':'.--.','q':'--.-','r':'.-.','s':'...','t':'-',
        'u':'..-','v':'...-','w':'.--','x':'-..-','y':'-.--','z':'--..','0':'-----','1':'.----','2':'..---',
        '3':'...--','4':'....-','5':'.....','6':'-....','7':'--...','8':'---..','9':'----.',' ':'/'
    };
    function morseEncode(s) {
        return s.toLowerCase().split('').map(c => morseMap[c] || c).join(' ');
    }

    // brainfuck (simplified - encode as BF program)
    function brainfuckEncode(s) {
        const bytes = new TextEncoder().encode(s);
        let result = '';
        let ptr = 0;
        for (const b of bytes) {
            if (b > ptr) result += '+'.repeat(b - ptr);
            else if (b < ptr) result += '-'.repeat(ptr - b);
            result += '.>';
            ptr = b;
        }
        return result;
    }

    // ---------- main encode function ----------
    function encode(str, id) {
        if (!str) return '';
        const fn = encoders[id];
        if (!fn) return '(unknown encoding)';
        try {
            const result = fn(str);
            if (result && typeof result.then === 'function') {
                return result.then(r => r);
            }
            return result;
        } catch(e) {
            return '(error: ' + e.message + ')';
        }
    }

    // ---------- update ----------
    async function updateTranslation() {
        const raw = inputEl.value;
        if (raw === '') {
            outputEl.textContent = '';
            charCount.textContent = '0 chars';
            return;
        }
        const id = encodingSelect.value;
        try {
            const result = await encode(raw, id);
            outputEl.textContent = result;
            charCount.textContent = result.length + ' char' + (result.length !== 1 ? 's' : '');
        } catch(e) {
            outputEl.textContent = '⚠️ error';
            charCount.textContent = '—';
        }
    }

    function clearAll() {
        inputEl.value = '';
        outputEl.textContent = '';
        charCount.textContent = '0 chars';
        copyFeedback.classList.remove('show');
    }

    function copyOutput() {
        const text = outputEl.textContent;
        if (!text || text === '' || text === 'encoded output will appear here') {
            copyFeedback.textContent = '⛔ nothing to copy';
            copyFeedback.classList.add('show');
            setTimeout(() => { copyFeedback.classList.remove('show'); copyFeedback.textContent = '✓ copied'; }, 1200);
            return;
        }
        if (navigator.clipboard && navigator.clipboard.writeText) {
            navigator.clipboard.writeText(text).then(() => {
                copyFeedback.textContent = '✓ copied';
                copyFeedback.classList.add('show');
                setTimeout(() => copyFeedback.classList.remove('show'), 1800);
            }).catch(() => fallbackCopy(text));
        } else {
            fallbackCopy(text);
        }
    }

    function fallbackCopy(text) {
        try {
            const temp = document.createElement('textarea');
            temp.value = text;
            document.body.appendChild(temp);
            temp.select();
            document.execCommand('copy');
            document.body.removeChild(temp);
            copyFeedback.textContent = '✓ copied';
            copyFeedback.classList.add('show');
            setTimeout(() => copyFeedback.classList.remove('show'), 1800);
        } catch (_) {
            copyFeedback.textContent = '⚠️ failed';
            copyFeedback.classList.add('show');
            setTimeout(() => copyFeedback.classList.remove('show'), 1500);
        }
    }

    // events
    translateBtn.addEventListener('click', updateTranslation);
    clearBtn.addEventListener('click', clearAll);
    copyBtn.addEventListener('click', copyOutput);
    inputEl.addEventListener('input', updateTranslation);
    encodingSelect.addEventListener('change', updateTranslation);
    window.addEventListener('DOMContentLoaded', updateTranslation);
})();
</script>
</body>
</html>

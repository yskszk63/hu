# ahe

Alphabet to hieroglyph encode.

# Example

```bash
$ cat cli.ts
const { stdin, stdout } = Deno;
const rbuf = new Uint8Array(1024 * 8);
const wbuf = new Uint8Array(rbuf.length * 2);
const enc = new TextEncoder();

while (true) {
    const n = await stdin.read(rbuf);
    if (n === null) {
        break;
    }

    let p = 0;
    for (const c of rbuf) {
        const s = encode(c);
        if (s !== null) {
            const a = enc.encode(s);
            wbuf.set(a, p);
            p += a.length;
        } else {
            wbuf.set([c], p);
            p += 1;
        }
    }

    let r = p;
    while (r) {
        r -= await stdout.write(wbuf.slice(p - r, p));
    }
}
...
$ cat cli.ts | deno run https://deno.land/x/ahe@v0.0.3/cli.ts
𓎡𓍯𓈖𓋴𓏏 { 𓋴𓏏𓂧𓇋𓈖, 𓋴𓏏𓂧𓍯𓅱𓏏 } = 𓂧𓇋𓈖𓍯;
𓎡𓍯𓈖𓋴𓏏 𓂋𓃀𓅱𓆑 = 𓈖𓇋𓅱 𓅱𓇋𓈖𓏏8𓄿𓂋𓂋𓄿𓇋(1024 * 8);
𓎡𓍯𓈖𓋴𓏏 𓅱𓃀𓅱𓆑 = 𓈖𓇋𓅱 𓅱𓇋𓈖𓏏8𓄿𓂋𓂋𓄿𓇋(𓂋𓃀𓅱𓆑.𓃭𓇋𓈖𓎼𓏏𓎛 * 2);
𓎡𓍯𓈖𓋴𓏏 𓇋𓈖𓎡 = 𓈖𓇋𓅱 𓏏𓇋𓎡𓋴𓏏𓇋𓈖𓎡𓍯𓂧𓇋𓂋();

𓅱𓎛𓇋𓃭𓇋 (𓏏𓂋𓅱𓇋) {
    𓎡𓍯𓈖𓋴𓏏 𓈖 = 𓄿𓅱𓄿𓇋𓏏 𓋴𓏏𓂧𓇋𓈖.𓂋𓇋𓄿𓂧(𓂋𓃀𓅱𓆑);
    𓇋𓆑 (𓈖 === 𓈖𓅱𓃭𓃭) {
        𓃀𓂋𓇋𓄿𓎡;
    }

    𓃭𓇋𓏏 𓏤 = 0;
    𓆑𓍯𓂋 (𓎡𓍯𓈖𓋴𓏏 𓎡 𓍯𓆑 𓂋𓃀𓅱𓆑) {
        𓎡𓍯𓈖𓋴𓏏 𓋴 = 𓇋𓈖𓎡𓍯𓂧𓇋(𓎡);
        𓇋𓆑 (𓋴 !== 𓈖𓅱𓃭𓃭) {
            𓎡𓍯𓈖𓋴𓏏 𓄿 = 𓇋𓈖𓎡.𓇋𓈖𓎡𓍯𓂧𓇋(𓋴);
            𓅱𓃀𓅱𓆑.𓋴𓇋𓏏(𓄿, 𓏤);
            𓏤 += 𓄿.𓃭𓇋𓈖𓎼𓏏𓎛;
        } 𓇋𓃭𓋴𓇋 {
            𓅱𓃀𓅱𓆑.𓋴𓇋𓏏([𓎡], 𓏤);
            𓏤 += 1;
        }
    }

    𓃭𓇋𓏏 𓂋 = 𓏤;
    𓅱𓎛𓇋𓃭𓇋 (𓂋) {
        𓂋 -= 𓄿𓅱𓄿𓇋𓏏 𓋴𓏏𓂧𓍯𓅱𓏏.𓅱𓂋𓇋𓏏𓇋(𓅱𓃀𓅱𓆑.𓋴𓃭𓇋𓎡𓇋(𓏤 - 𓂋, 𓏤));
    }
}
...
```

# License

MIT
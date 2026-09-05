# cma_public

Veřejná data pro aplikaci **Crypto Market Analysis** (CMA).

Repozitář neobsahuje žádný kód aplikace — jen datový soubor, který si
aplikace stahuje, a dokumenty, na které musí být veřejný odkaz.

## `snapshot.json`

Předpočítané metriky ke kryptoměnám obchodovaným na Binance. Generuje se
automaticky **jednou za hodinu** z veřejných zdrojů:

| Zdroj | Co z něj je |
|---|---|
| CoinGecko | market cap, supply, ATH/ATL, počet lidí s coinem v portfoliu, sentiment |
| GitHub | commity, poslední push, hvězdy, počet contributorů |
| DeFiLlama | TVL řetězce |
| Binance | dlouhodobý růst od listingu, korelace s BTC, volatilita, trend objemu |

**Aktuální ceny ve snapshotu nejsou.** Ty si aplikace bere živě z Binance,
protože hodinu stará cena je k ničemu.

### Proč to takhle

Limity CoinGecka a GitHub API se počítají na IP adresu, případně na token.
Ani jedno se neškáluje na desetitisíce uživatelů — a sdílený token vložený
do aplikace by byl dokonce horší než žádný, protože jeho limit platí
dohromady pro všechny, kdežto anonymní limit má každý svůj. Jediné, co se
škáluje, je jeden server, který data stáhne jednou a rozdá je hotová.

### Formát

```jsonc
{
  "generatedAt": "2026-08-30T12:07:00.000Z",  // UTC
  "version": 1,                                // verze formátu
  "coins": [ /* … */ ]
}
```

Klient odmítne snapshot s vyšší `version`, než na jakou je stavěný, a spadne
zpět na přímé volání API.

## Dokumenty

- [privacy.md](privacy.md) — zásady ochrany osobních údajů

# Trading Workspace History

> Journal chronologique des sessions de trading et décisions importantes.
> Le plus récent en haut. Mis à jour via `/review` ou `/update`, pas à la main.

---

## Format d'une entrée de session

```
## AAAA-MM-JJ — Session [matin/après-midi/week-end]

**Contexte :** paires suivies, état d'esprit, conditions de marché.
**Trades pris :** [vide si aucun, c'est valide]
**Trades refusés (et pourquoi) :** ce que j'ai vu et écarté, et la raison.
**Erreurs / patterns du jour :** ce qui revient.
**Décision / règle ajoutée :** s'il y a lieu.
```

## Format d'une entrée de trade

```
### Trade — AAAA-MM-JJ HH:MM — [Paire] [Long/Short]

- **Timeframe d'entrée :** [60 / 240 / D]
- **Contexte HTF :** [haussier / baissier / range, BOS/CHoCH récent]
- **POI utilisé :** [OB / FVG / BPR / Breaker, niveau]
- **Liquidité prise avant entrée :** [EQH / EQL / Asian H / PDH...]
- **Killzone :** [London / NY / hors zone]
- **Entrée :** prix
- **SL :** prix (raison du placement)
- **TP :** prix (raison du placement)
- **RR visé :** [1:2 / 1:3]
- **Résultat :** [TP / SL / BE / partial / en cours]
- **Erreur ou bonne décision :** ce qu'il faut retenir.
```

---

## 2026-06-21 — Choix des sources d'exchange pour la watchlist

**Contexte :** validation des sources de données TradingView pour les 3 symboles de la watchlist. Le rules.json initial proposait Binance (USDT) par défaut, choix non discuté.

**Décisions :**
- BTC : `BITSTAMP:BTCUSD` (exchange régulé EU, paire USD réelle).
- ETH : `BITSTAMP:ETHUSD` (idem).
- SOL : `COINBASE:SOLUSD` (Coinbase régulé US, paire USD réelle).
- Refus explicite de Binance/USDT : exposition réglementaire FR/AMF, stablecoin moins propre pour analyse SMC long terme.

**Conséquences :**
- Les structures de marché lues seront légèrement différentes de celles d'analyses SMC communautaires (qui utilisent souvent Binance). Décalage de volume et parfois de niveaux de quelques pips.
- Avantage : alignement avec un environnement réglementé, plus cohérent si bascule un jour en réel sur Kraken/Bitstamp/Coinbase.

**Prochaine action :** ouvrir TradingView Desktop, vérifier que les 3 symboles sont chargeables et que les bougies 4H/1H/Daily sont disponibles en Basic.

---

## 2026-06-21 — Setup du workspace + alerte broker

**Contexte :** finalisation de l'archi à 4 fichiers du workspace trading. Décision d'utiliser le MCP server de Kasper (`claudeverstradingview`) pour l'intégration TradingView Desktop. Plan TradingView : Basic. Mode : démo uniquement.

**Décisions :**
- Architecture validée : workspace de posture (CLAUDE/SOUL/CONTEXT/HISTORY) séparé du repo MCP de Kasper.
- Watchlist initiale : BTCUSDT, ETHUSDT, SOLUSDT (par défaut Kasper, validée).
- Timeframes : 1H / 4H / Daily. Pas de scalp.
- Règles dures : RR 1:2 min, max 2 positions, stop session après 3 SL d'affilée, 1h d'attente après un SL.
- Priorité absolue Ascensia : aucune session trading n'empiète sur les créneaux commerciaux du matin (lundi-vendredi 8h-12h FR).

**Changements de contexte :**
- `CONTEXT.md` créé avec profil complet + glossaire SMC/ICT version Kasper.
- `rules.json` créé pour le `morning_brief`, mode DEMO_ONLY.

**Alerte broker (à traiter sérieusement avant tout passage en réel) :**
- Le broker envisagé `app.liquid.trade` n'a **pas** été vérifié officiellement.
- Plusieurs entités utilisent le nom "Liquid" dans le crypto/trading. L'une d'elles (`liquidbrokers.com`, Liquid Markets Pty Ltd, Australie) présente des **signaux d'alerte sérieux** :
  - Licence ASIC en mode "Appointed Representative" hors du périmètre retail autorisé par le principal (Pulse Markets).
  - Classée "scam broker" par BrokersView en 2026.
  - Trustpilot 3 étoiles avec plaintes répétées de chasse aux stops et retraits bloqués.
  - Entité enregistrée fin 2023, domaine racheté en 2024, opérationnelle depuis décembre 2024.
- **Action requise avant tout dépôt réel** : vérifier l'identité exacte de `app.liquid.trade`, son enregistrement légal, et comparer à des alternatives propres (Bitstamp, Kraken EU, courtier régulé MiFID II en France).
- Pour l'instant : **analyse uniquement, zéro exécution sur Liquid Trade**.

**Décision / règle ajoutée :**
- Une "Priorité du moment" est inscrite dans CONTEXT.md : valider en démo sur plusieurs week-ends que la méthode produit des résultats reproductibles avant tout passage en réel.

---

[Les prochaines entrées s'ajoutent au-dessus de cette ligne, plus récent en haut.]

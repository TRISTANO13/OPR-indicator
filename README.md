# 📊 Stratégie de 15h30 — Pine Script v5

Un indicateur **TradingView** conçu pour le trading intraday, centré sur la bougie clé de **15h30** (configurable).
Il combine :

* 📍 **Repères visuels** du range de la bougie cible (Haut, Bas, Milieu) sur **M15**
* 📈 **EMA 20 & EMA 50** calculées sur **M5** et affichées sur tous les timeframes
* 🛡️ **Supertrend** calculé sur un **timeframe supérieur** (H1 par défaut) pour filtrer la tendance

---

## 🚀 Fonctionnalités

* **Lignes 15h30** :

  * Ligne **haute** = plus haut + offset en ticks
  * Ligne **basse** = plus bas + offset en ticks
  * Ligne **médiane** = moyenne des deux
  * Traçage uniquement sur graphique **M15**
* **Moyennes mobiles** :

  * EMA 20 (M5)
  * EMA 50 (M5)
* **Supertrend HTF** :

  * Paramétrable : période ATR, multiplicateur, source ATR ou SMA(TR)
  * Timeframe configurable (par défaut H1)

---

## ⚙️ Paramètres

| Paramètre                           | Type        | Description                                           |
| ----------------------------------- | ----------- | ----------------------------------------------------- |
| `Heure cible` (`inputHour`)         | `int`       | Heure de la bougie clé (par défaut 15)                |
| `Minute cible` (`inputMinute`)      | `int`       | Minute de la bougie clé (par défaut 30)               |
| `Décalage vertical` (`offsetTick`)  | `float`     | Décalage vertical des lignes en ticks                 |
| `Longueur ligne` (`extendLength`)   | `int`       | Nombre de bougies sur lesquelles prolonger les lignes |
| `ATR Period` (`Periods`)            | `int`       | Période de l’ATR pour le Supertrend                   |
| `ATR Multiplier` (`Multiplier`)     | `float`     | Multiplicateur ATR pour le Supertrend                 |
| `Use ATR or SMA(TR)?` (`changeATR`) | `bool`      | Utiliser ATR brut ou SMA(TR)                          |
| `Timeframe du Supertrend` (`tf`)    | `timeframe` | Timeframe sur lequel calculer le Supertrend           |

---

## 📷 Aperçu visuel

*(Insérer ici un screenshot TradingView avec les lignes, EMA et Supertrend)*

---

## 🧠 Logique

1. **Détection de la bougie cible**

   ```pinescript
   isTargetBar = (hour == targetHour and minute == inputMinute)
   ```

   * `targetHour` = `inputHour - 2` (décalage pratique si votre flux est en UTC)

2. **Traçage du range de la bougie clé (M15)**

   * Ligne haute, ligne basse, ligne médiane pointillée

3. **Ajout des EMA (M5)**

   * Via `request.security()` pour injecter les données M5 dans n’importe quel TF

4. **Calcul Supertrend (HTF)**

   * Fonction interne `supertrendFunc()`
   * Données récupérées sur `tf` via `request.security()`
   * Affichage bande haute (vert) ou basse (rouge) selon tendance

---

## 📦 Installation

1. Ouvrir **TradingView**
2. Aller dans **Pine Editor**
3. Coller le contenu du fichier `.pine`
4. Cliquer sur **Add to chart**
5. Ajuster les paramètres selon vos besoins

---

👤 **Auteur** : *TRISTANO13*

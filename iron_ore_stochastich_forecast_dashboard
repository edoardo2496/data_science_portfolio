# 🏗️ Iron Ore Stochastic Forecast Dashboard

Questo progetto utilizza il calcolo stocastico per prevedere l'andamento del prezzo del ferro grezzo, fornendo uno strumento decisionale per l'ottimizzazione degli acquisti di materie prime (tondino ferroso).

## 🧠 Il Modello Matematico
Il motore della previsione si basa sul processo di **Ornstein-Uhlenbeck (Mean Reversion)**. A differenza dei modelli standard, questo riconosce che le commodity tendono a tornare verso un costo medio di produzione nel lungo periodo.

L'evoluzione del prezzo $S_t$ è descritta dalla seguente Equazione Differenziale Stocastica (SDE):

$$dS_t = \theta(\mu - S_t)dt + \sigma dW_t$$

Grazie al **Lemma di Itô**, abbiamo derivato la soluzione analitica utilizzata nella dashboard per proiettare il valore atteso e il "cono di incertezza" (intervallo di confidenza) a 3, 6 e 12 mesi.

## 🛠️ Tecnologia e Struttura
- **Python (Scikit-learn/Pandas):** Utilizzato per la calibrazione dei parametri ($\theta, \mu, \sigma$) sui dati storici della World Bank (post-2010).
- **JavaScript (Plotly.js):** Gestisce la parte interattiva della dashboard lato client.
- **GitHub Pages:** Hosting della dashboard statica.

## 📈 Come usare la Dashboard
La dashboard è pensata per acquirenti industriali. Inserendo l'orizzonte temporale, il modello calcola se il prezzo attuale è statisticamente "caro" o "conveniente" rispetto alla sua dinamica stocastica, suggerendo se procedere con l'acquisto o attendere un riallineamento verso la media.

---
*Progetto sviluppato per analisi predittiva e supporto alle decisioni aziendali.*

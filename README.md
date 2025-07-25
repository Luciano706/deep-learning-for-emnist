# Riconoscimento di Caratteri Manoscritti (EMNIST) - Un Confronto tra Modelli

Questo repository contiene il codice e l'analisi di un progetto di Machine Learning finalizzato al riconoscimento di caratteri manoscritti utilizzando il dataset **EMNIST (Extended MNIST)**. L'obiettivo principale è confrontare le performance, l'efficienza e le caratteristiche di diversi approcci di modellazione, spaziando da modelli classici a reti neurali profonde.

## 📋 Indice
1. [Introduzione e Obiettivi](#1-introduzione-e-obiettivi)
2. [Dataset](#2-dataset)
3. [Approcci di Modellazione](#3-approcci-di-modellazione)
    - [Modello 1: Rete Neurale Convoluzionale (CNN) da Zero](#modello-1-rete-neurale-convoluzionale-cnn-da-zero)
    - [Modello 2: Transfer Learning con Fine-Tuning (MobileNetV2)](#modello-2-transfer-learning-con-fine-tuning-mobilenetv2)
    - [Modello 3: Classificatore Random Forest (Baseline Non-Deep)](#modello-3-classificatore-random-forest-baseline-non-deep)
4. [Riepilogo dei Risultati](#4-riepilogo-dei-risultati)
5. [Come Eseguire il Progetto](#5-come-eseguire-il-progetto)
    - [Prerequisiti](#prerequisiti)
    - [Installazione](#installazione)
    - [Utilizzo](#utilizzo)
6. [Conclusioni e Lezioni Apprese](#6-conclusioni-e-lezioni-apprese)

---

## 1. Introduzione e Obiettivi

Il progetto esplora il campo del Riconoscimento Ottico dei Caratteri (OCR) applicato a un dataset complesso e bilanciato. L'analisi non si limita a trovare il modello più performante, ma si concentra sul **confronto metodologico** per comprendere i punti di forza e i limiti di ogni approccio.

**Obiettivi principali:**
- Implementare e addestrare una CNN su misura per il problema.
- Sfruttare la potenza del Transfer Learning utilizzando un modello pre-addestrato (MobileNetV2) e la tecnica del Fine-Tuning.
- Stabilire un solido benchmark utilizzando un modello di machine learning classico (Random Forest).
- Analizzare e confrontare i risultati in termini di accuratezza, efficienza computazionale e capacità di generalizzazione.

---

## 2. Dataset

È stato utilizzato il dataset **EMNIST (Extended MNIST)** nella sua versione **Balanced**.
- **Contenuto:** 131.600 immagini in scala di grigi di 28x28 pixel.
- **Classi:** 47 classi bilanciate, che includono 10 cifre, 26 lettere maiuscole e 11 lettere minuscole.
- **Accesso:** Il dataset è disponibile su [Kaggle](https://www.kaggle.com/datasets/crawford/emnist).

---

## 3. Approcci di Modellazione

Sono stati sviluppati e analizzati tre modelli distinti.

### Modello 1: Rete Neurale Convoluzionale (CNN) da Zero

- **Architettura:** Una CNN sequenziale con due blocchi convoluzionali (Conv2D + MaxPooling2D), seguiti da strati densi per la classificazione. Include regolarizzazione tramite Dropout per prevenire l'overfitting.
- **Logica:** Questo modello serve come baseline "deep learning" di alta qualità, apprendendo le feature visive direttamente e unicamente dai dati EMNIST.
- **Risultato Chiave:** Ha raggiunto un'accuratezza eccellente (~89%), dimostrando l'efficacia di un'architettura su misura.

### Modello 2: Transfer Learning con Fine-Tuning (MobileNetV2)

- **Architettura:** Utilizza il modello **MobileNetV2**, pre-addestrato su ImageNet, come base per l'estrazione di feature. La tecnica di fine-tuning è stata applicata per adattare il modello al dominio EMNIST.
- **Logica:** Questo approccio testa se la conoscenza pre-esistente di un modello complesso può essere trasferita a un nuovo problema, superando la sfida del *domain mismatch* (immagini fotorealistiche vs. caratteri astratti).
- **Risultato Chiave:** Ha raggiunto un'accuratezza molto buona (~87.4%), ma leggermente inferiore alla CNN da zero. I grafici di addestramento mostrano un classico "trauma da adattamento" all'inizio del fine-tuning, seguito da una rapida convergenza.

### Modello 3: Classificatore Random Forest (Baseline Non-Deep)

- **Architettura:** Un modello d'insieme basato su alberi decisionali, implementato con Scikit-learn.
- **Logica:** Serve come benchmark per i modelli classici. Tratta ogni immagine come un vettore "piatto" di 784 pixel, ignorando la struttura spaziale 2D.
- **Risultato Chiave:** Ha raggiunto un'accuratezza rispettabile (~82%), quantificando il limite di un approccio che non "vede" la struttura dell'immagine e mettendo in prospettiva il guadagno ottenuto dalle CNN.

---

## 4. Riepilogo dei Risultati

| Modello | Accuratezza Test Set | Tempo di Training | Punti di Forza |
| :--- | :--- | :--- | :--- |
| **CNN da Zero** | **~89%** | Medio | **Migliori performance**, architettura ottimizzata. |
| **Fine-Tuning (MobileNetV2)** | ~87.4% | Medio-Lungo | Ottima capacità di adattamento, sfrutta conoscenza pregressa. |
| **Random Forest** | ~82% | **Molto Veloce** | Ottimo baseline, efficiente e semplice da implementare. |

---

## 5. Conclusioni e Lezioni Apprese

La lezione più importante di questo progetto è che **la soluzione più complessa non è sempre la migliore**. Nonostante la potenza del Transfer Learning, il forte disallineamento di dominio tra ImageNet e EMNIST ha fatto sì che una CNN più semplice, ma progettata su misura, ottenesse le performance migliori.

Il progetto dimostra con successo:
- L'efficacia delle CNN nell'apprendere gerarchie di feature spaziali.
- La potenza ma anche i limiti del Transfer Learning.
- L'importanza di stabilire baseline solidi con modelli classici per contestualizzare i risultati.

Questo lavoro fornisce una panoramica completa e pratica su come affrontare un problema di classificazione di immagini, confrontando metodologie diverse e analizzandone i compromessi.

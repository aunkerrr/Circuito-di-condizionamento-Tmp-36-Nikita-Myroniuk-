# Circuito-di-condizionamento-Tmp-36-Nikita-Myroniuk-
This project made for demonstration of mine basic electrical competence

Fatto da Nikita Myroniuk
======================================================================== REPORT TECNICO: CONDIZIONAMENTO SEGNALE SENSORE TMP36 (-10C/+40C)
OBIETTIVO DEL PROGETTO

Trasformare l'uscita del sensore TMP36 in un segnale lineare 0-5V. Dati di partenza:
Temperatura -10 C = Uscita sensore 0.4V
Temperatura +40 C = Uscita sensore 0.9V
Obiettivo finale: -10 C (0.4V) -> 0V | +40 C (0.9V) -> 5V
Logica matematica applicata:
OFFSET: Sottrarre 0.4V per azzerare il punto di partenza.
GUADAGNO (GAIN): Moltiplicare x10 la differenza (0.5V x 10 = 5V). Formula: Vout = 10 * (V_sensor - 0.4V).
ARCHITETTURA DEL CIRCUITO (STRUTTURA A 3 STADI)

Il circuito utilizza tre amplificatori operazionali 741:
A. STADIO DI INGRESSO (BUFFER / SEGUITORI):
Utilizzati per isolare il sensore e il partitore di tensione dal resto del circuito.
Evitano che il carico delle resistenze successive faccia "crollare" la tensione del segnale originale.
B. STADIO DI RIFERIMENTO (PARTITORE):
Le resistenze sono collegate a +5V e GND crea la tensione di riferimento di 0.4V.
Questa tensione viene stabilizzata da uno dei buffer prima di entrare nel calcolatore.
C. STADIO DI CALCOLO (DIFFERENZIALE):
L'ultimo operazionale esegue la sottrazione e l'amplificazione simultaneamente.
CONNESSIONI DETTAGLIATE DEI PIN (UA741)

Per tutti i tre operazionali 741:
PIN 7: Alimentazione Positiva (+12V)
PIN 4: Alimentazione Negativa (-12V)
PIN 6: Uscita del segnale
CONFIGURAZIONE SPECIFICA:
OPERAZIONALE 1 (Buffer Sensore):
Pin 3 (+): Ingresso segnale dal pin centrale del TMP36.
Pin 2 (-): Collegato direttamente al Pin 6 (Feedback totale).
OPERAZIONALE 2 (Buffer Riferimento/Partitore):
Pin 3 (+): Ingresso dal cursore centrale del partitore (0.4V).
Pin 2 (-): Collegato direttamente al Pin 6 (Feedback totale).
OPERAZIONALE 3 (Amplificatore Differenziale):
Pin 3 (+): Riceve il segnale dal Buffer Sensore tramite resistenza 10k.
Pin 3 (+): Collegato a GND tramite resistenza 100k.
Pin 2 (-): Riceve i 0.4V dal Buffer Riferimento tramite resistenza 10k.
Pin 2 (-): Collegato al Pin 6 tramite resistenza 100k (Feedback per Gain 10).
ANALISI DEI COMPONENTI E TERMINOLOGIA

PARTITORE: Circuito a resistenze che riduce i 5V a 0.4V. L'uso delle resistenze permette di correggere le tolleranze delle resistenze per avere uno zero perfetto.
BUFFER: Agisce come un "muscolo". Ha un'altissima impedenza in ingresso (non assorbe corrente dal sensore) e bassissima in uscita (può pilotare le resistenze del differenziale senza distorsioni).
-12V (ALIMENTAZIONE NEGATIVA): Necessaria perché il 741 non è "Rail-to-Rail". Senza il voltaggio negativo, l'operazionale non riuscirebbe fisicamente a scendere a 0.00V, fermandosi a circa 1.5V-2V.
RISOLUZIONE DEI PROBLEMI DURANTE LA COSTRUZIONE

Durante lo sviluppo, le sfide principali sono state risolte come segue:
ERRORE DI CARICO: Inizialmente collegando il sensore direttamente alle resistenze, il tensione cade. SOLUZIONE: Inserimento dei Buffer per isolare i segnali.
IMPOSSIBILITA' DI RAGGIUNGERE 0V: L'uscita rimaneva alta anche a -10C. SOLUZIONE: Collegamento del Pin 4 alla linea dei -12V invece che a GND.
IMPRECISIONE DELLO ZERO: Le resistenze fisse non davano esattamente 0.4V. SOLUZIONE: Utilizzo delle resistenze per una taratura fine del riferimento di offset.
GUADAGNO SCORRETTO: Il rapporto tra le resistenze di feedback e ingresso deve essere esattamente 10 (100k / 10k). SOLUZIONE: Verifica dei codici colore dei resistori sulla breadboard.
======================================================================== FINE REPORT - CIRCUITO PRONTO PER ACQUISIZIONE ARDUINO (ADC 0-5V)
Fatto da Nikita Myroniuk




Tutti i link necessari:
https://www.tinkercad.com/things/giDzrVvdgzD-circuito-di-condizionamento-tmp-36-nikita-myroniuk?sharecode=VcHktzstXJ2wWLT5jurK-uSyVZyG5gdduJfMteM3Q8Q
Anche ci sono i file allegati.
Scopri di più su:
https://github.com/aunkerrr/Circuito-di-condizionamento-Tmp-36-Nikita-Myroniuk-

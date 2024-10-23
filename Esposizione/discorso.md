# Discorso
### intro
Buongiorno, in questo con questa tesi si vuole analizzare il problema di trovare il flusso massimo instradabile in un network. Ripercorreremo alcuni degli algoritmi più importanti, fino ad arrivare a quello di nostro maggior interesse: L'algoritmo di Orlin.

È fondamentale l'analisi di ogni algoritmo intermedio per capire l'algortimo successivo, in quanto questi sono tra loro strettamente legati. 
Iniziamo dal contesto:

### preliminari
Al giorno d'oggi, le reti di connessioni come le strade o come internet sono presenti ormai su vasta scala e noi vi facciamo grande affidamento. 

Prendiamo d'esempio una rete internet, parliamo di una rete formata da migliaia e migliaia di dispositivi connessi tra loro:
Queste connessioni variano di prestazione come i dispositivi che la popolano. 
Nella teoria dei grafi rappresentiamo il **network** come un particolare grafo semplice diretto in cui due nodi in particolare sono in risalto: la sorgente $s$ e il pozzo $t$. 
Ogni arco (i,j) ha associata una capacità che rappresenta il massimo flusso che può passare da i a j.
Per convenzione si suppone che, se esiste l'arco (i,j) allora esiste anche (j,i), ognuno con la propria capacità. 

Un flow, o flusso, è qualisasi cosa possa passare attraverso la capacità residua degli archi nel network. Per definirsi feasible, cioè compatibile, con il network, deve rispettare i **vincoli di capacità** e di **conservazione del flusso**.

La capacità di un arco si misura quando questo non è attraversato da nessun flow, né in un verso né in un altro.
Solo quando un arco è attraversto dal flusso, possiamo parlare di capacità residua.

Dato che l'intento è diramare il flusso attraverso tutta la rete, tenere traccia delle capacità residue ci permette di delineare il grafo residuo. Quando nel grafo residuo non esiste più un percorso da s a t, il flow che lo attraversa ha raggiunto il suo massimo valore. 

Trovare il max flow di un network è importante per sfuttarne al massimo le potenzialità senza sovraccaricarlo.
Data la forte dinamicità delle reti moderne, è molto importante trovare questo limite in fretta.

### primi algoritmi
Il primo algoritmo usato per calcolare il flusso massimo è il Ford-Fulkerson pubblicato nel 1956, un algoritmo che incrementa il flusso su un percorso qualsiasi da s a t finche ne esiste uno.
Un'idea tanto semplice quanto inefficiente poiché il costo computazionale dipende dal flusso massimo che può passare nella rete. 

L'algoritmo di Edmonds-Karp seguì nel 1972, e svincolò il costo computazionale dalla portata della rete ottenendo costo $O(nm^2)$. 

Il principio di tale miglioramento stava nel trovare il percorso più corto da $s$ a $t$ e incrementare il flusso su quel percorso invece che su uno qualsiasi. Saturando almeno un arco per ogni incremento, si lega il costo al numero di archi invece che al flusso massimo.

### dinitz
Fu nello stesso periodo però che, indipendentemente, Yefim Dinitz elaborò una strategia molto simile ma che manteneva un costo computazionale sensibilmente minore: $O(n^2m)$. 

Anche questo algoritmo utilizza una BFS per trovare le distanze di tutti i nodi da t, ma invece di incrementare il flusso solo sullo shortest path, si cerca un flusso bloccante nell'admissible graph.

Per flusso bloccante si intende un flusso che satura almeno un arco in tutti i percorsi da $s$ a $t$.
L'admissible graph è una restrizione della rete in cui tutti i percorsi da s a t sono della stessa lunghezza.
In questo modo ogni volta che un flusso bloccante viene trovato, la distanza tra s e t aumenta di sicuro legando così il numero di fasi non più a numero di archi ma a quello di nodi *(la massima distanza che puo esistere tra s e t è uguale al numero di nodi)*.

### Goldberg citato
Siamo ancora lontani dal costo $O(nm)$, ma ad accorciare le distanze arrivano nel 1998 Andrew V. Goldberg e Satish Rao che pubblicano un algoritmo che risolve il problema in 
\[O(\min\{m^{1/2}, n^{2/3}\}m\log(n^2/m)\log U)\]

Una complessità definita weakly polynomial. 
Infatti abbiamo ancora una dipendenza dalla capacità dell'arco più capiente.  
*Nella tesi è presente un'analisi completa dell'algoritmo. Sono mostrate chiaramente le scelte procedurali dell'algoritmo,le criticità che queste potrebbero comportare e le dimostrazioni di come sono state gestite.*

### Orlin
La strada che porta all'algoritmo in $O(nm)$ è ora ad un bivio. 
Se il network di cui cerchiamo il flusso massimo fosse abbastanza denso si potrebbe usare l'algoritmo di King Rao e Tarjan del 1992.
L'algoritmo sviluppa una soluzione in $O(nm)$ per grafi in cui il rapporto tra nodi e archi è almeno $m/n = \Omega(n^\varepsilon)$ per qualche $\varepsilon > 0$
 
Ma, se il numero di archi non fosse abbastanza elevato da coprire gli altri costi di quest'algoritmo, nel 2013 James B. Orlin pubblica una soluzione che in tempo $O(nm)$ calcola il flusso massimo per grafi in cui $m = O(n^{1+\varepsilon})$. 

Le idee che guidano le scelte di questa soluzione partono dall'osservazione che
se si hanno abbastanza archi rispetto alla massima capacità, l'algoritmo di Goldberg-Rao ha già costo strettamente polinomiale
In oltre dato che cerchiamo la soluzione per un grafo sparso, possiamo notare che la soluzione può avere costo $O(nm)$

Lo scopo di Orlin è quindi quello di eseguire tutte le fasi del Golberg-Rao su dun grrafo adeguato. 
Per farlo possiamo modificare il network originale e far si che il numero di nodi sia legato agli archi e alla massima capacità dell'arco originale.

Chiameremo questi nodi $\Delta$-critici. Una condizione necessaria per ottenere costo $O(nm)$ è quella che esistano durante tutte le fasi al massimo O(m) nodi $\Delta$-critici.
Per garantire ciò il natwork originale viene modificato in due passaggi, contrazione e compattazione.
Nella contrazione si fissa un valore $\Delta$ che fa da upper bound al flusso e si contraggono tutti i cicli composti da archi con capacità residua abbondante.

Possiamo contrarre gliarchi abbondanti uscenti da s o entranti in t, possiamo contrarre due nodi connessi da archi abbondanti e in generale qualsiasi altro set di nodi connesso da un ciclo abbondante.

La compattazione invece avviene in due fasi:
- nella prima vengono eliminati i nodi connessi solo ad archi abbondanti e vengono ridirezionati gli archi ad essi connessi 
- nella seconda viene trasferita la capacità residua da alcuni perscorsi specifici a dei nuovi pseudoarchi.
    
È possibile dimostrare che nessuna di queste operazioni influisce sul flusso massimo calcolabile nel grafo residuo. La seguente invece si:

Infatti al temrine della compattazione alcune capacità residue ritenute troppo piccole vengono scartate dunque il flusso massimo instradabile potrebbe avere un valore inferiore all'originale.
Nonostante ciò è possibile dimostrare che la capacità residua persa è al massimo $\Delta/16m$ per ogni fase di incremento *mentre noi cerchiamo un flusso $\Delta/8m$-ottimale quindi questo non è un problema.*

Vediamo dunque come funziona la procedura di incremento del flusso dell'algoritmo di orlin.
Si fissa un valore per delta;
Si contano i nodi $\Delta$-critici;
- Se sono almeno $m^{9/16}$ allora il grafo originale è abbastanza sparso e si può eseguire il Goldberg-Rao per trovare un flusso $\Delta/8m$-ottimale
- Se sono tra gli $m^{9/16}$ e gli $m^{1/3}$ nodi allora si contrae il grafo per renderlo sparso a sufficienza e si cerca il flusso $\Delta/8m$ ottimale nel grafo compatto.
- Se invece i nodi delta critici fossero meno di $m^{1/3}$ allora non non si può ancora contrarre il grafo in quanto si otterrebbe un incremento troppo piccolo che non fa crescere il valore del flusso abbastanza in fretta. In questa situazione però è possibile scegliere un valore $\Gamma$ più piccolo di $\Delta$ per aumentare abbastanza numero di nodi $\Gamma$-critici.

Avendo i due bottlenek di adattare il flusso dal grafo compatto all'originale e di mantenere la chiusura transitiva dei nodi che sono connessi da archi abbondanti, otteniamo il costo finale di \[O(nm + m^{31/16}\log^2n)\]

Dunque abbiamo ottenuto una soluzione che per i grafi sparsi trova il flusso massimo in tempo strettamente polinomiale $O(nm)$
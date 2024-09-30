# Max flow in un network
I miei [appunti](latex/appuntiTesi.pdf) sul problema del max flow in un network

## To Do
- [x] Algoritmo di Dinic
- [x] Algoritmo di Goldberg-Rao 
    - [x] presentazione nozioni
    - [x] dimostrazione della correttezza 
    - [x] dimostrazione del tempo computazionale
- [ ] Algoritmo di Prim 
    - [x] presentazione nozioni    
    - [x] $\Gamma$-compact network
    - [ ] dimostrazioni di correttezza e costo

- [ ] Dynamics Trees
    - [x] definizione BST
    - [x] slplay tree / tango tree
    - [ ] link cut tree 


    
## Dubbi
- nell'algoritmo finale nel caso $c < m^{1/3}$ credo che gamma vada calcolato per fare in modo che $c<2m^{1/3}$  
- credevo così perché così era riportato nel vecchio paper. comunque Quello che credo si intenda è 
    - abbassando il valore di $\Gamma$ i nodi $\Gamma$-critici aumentano, quindi il voglio il più piccolo valore di delta per fare in modo che i nodi $\Gamma$-critici tendano da sinistra a $m^{1/3}$ in modo da assicurarmi di averne almeno $O(m^{1/3})$
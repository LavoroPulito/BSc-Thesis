# Perché T = O($m^{3/2}log^2n$)?
sono ormai piuttosto convinto che venga da Glodberg-Rao. Il costo di Goldberg-Rao è :\[O(\Lambda m \log(n^2/m)\log mU)  \]


ricordando che ogni improvement phase prende in input un $(S,T)$-cut e ne restituisce uno con un $1/8m$ della capacità residua possiamo concordare che il numero di improvement phase saranno al massimo $\log _{8m}mU \le 1+\log U$ ottenendo così $O(\log U)$ fasi

Per quanto riguarda $m^{3/2}$ credo che venga da $\Lambda = m^{1/2} \rightarrow \Lambda m = m^{3/2}$

possiamo notare che se \[\log U < m^{7/16} \implies \tilde{O}(m^{3/2}m^{7/16}) = \tilde{O}(m^{31/16})\] 
*(The $\tilde O$ notation ignores log factors of $m$ and $n$).*

Possiamo eseguire il goldberg rao in un grafo compattato con Al massimo $C$ nodi e $O(C^2)$ archi con 
\[C = \frac{m}{\log U}\]
*da dimostrare*
L'idea di fondo è proprio calcolare questi C nodi e poi 
The time to run the Goldberg-Rao **scaling phase** on a network with at most C nodes and $O(C^2)$ arcs is $\tilde{O}(C^{7/3})$ time. 
eppure
\[min \{m^{1/2}, n^{2/3}\} = m^{1/2} = C \]
e quindi 
\[O(C\cdot C^2\cdot \log(C^2/C^2))\]

NOTA: credo di star facendo un errore ma non so dove

In conclusione si afferma che se $\log U \ge m^{7/16}$ posso approssimare il flusso nel grafo contratto in cui se il costo di una scaling phase è $\tilde O (C^{7/3}*\log) U$ allora 
\[\tilde O (C^{7/3} \log U) = \tilde O ((\frac{m}{\log U})^{7/3} \log U) = \tilde O(m^{7/3}\cdot \log^{-4/3} U)\]

In alcuni contesti (specialmente nei risultati approssimati o negli algoritmi per il flusso massimo), si può arrivare a una semplificazione del tipo:
\[log⁡^{−4/3}U ∼ m^{−ϵ}\]


per un certo piccolo $ϵ$, che dipende dall'algoritmo o dal contesto specifico.

Di conseguenza, sostituendo $log⁡^{−4/3}U$ con $m^{−ϵ}$, l'espressione diventa:
\[\tilde O(m^{7/3}log⁡^{−4/3}U) ∼ \tilde O(m^{(7/3)−ϵ}) =\tilde O (m^{31/16})\]


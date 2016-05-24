# 23. - DFT/FFT (radix-2)

> vlastnosti a výpočetní složitost, linearní a kruhová konvoluce, rychlý
výpočet lineární konvoluce pomocí FFT (metoda overlap-add, overlap-save).

##DFT a FFT
- Rychlá Fourierova Transformace (Fast Fourier Transform)
je skupina algoritmů umožňující výpočetně optimalizovaný
výpočet DFT a IDFT
- DFT se používá pro transformaci konečné (periodické) řady
čísel na konečný (periodický) vektor frekvenčních komponent
- Výpočetní náročnost DFT vypočtené podle deﬁnice je ![O(N^{2})](https://latex.codecogs.com/svg.latex?O%28N%5E%7B2%7D%29) aritmetických operací
	- FFT je schopna spočítat stejný výsledek v ![O(N \cdot log(N))](https://latex.codecogs.com/svg.latex?O%28N%20%5Ccdot%20log%28N%29%29)operacích

**Radix-2 Cooley-Tukey FFT** 

- je algoritmus určený pro sekvence délky ![N = 2^{k} , k \in Z](https://latex.codecogs.com/svg.latex?N%20%3D%202%5E%7Bk%7D%20%2C%20k%20%5Cin%20Z)
- Výpočetních úspor je dosaženo díky periodicitě komplexních exponenciál a možnosti vypočítat N-bodovou DFT pomocí dvou N/2-bodových DFT

##Lineární a kruhová konvoluce
###Lineární konvoluce

![y[n] = x[n] * h[n] = \sum_{k=0}^{N-1}x[k]\cdot h[n-k]](https://latex.codecogs.com/svg.latex?y%5Bn%5D%20%3D%20x%5Bn%5D%20*%20h%5Bn%5D%20%3D%20%5Csum_%7Bk%3D0%7D%5E%7BN-1%7Dx%5Bk%5D%5Ccdot%20h%5Bn-k%5D)

- možné výpočty:
	- Posuvné pásky
	- Násobení polynomů
	- Kompozice posunutých impulzních odezev
- **Vlastnosti konvoluce**:
	- Komutativita: (Commutative property)
		-	x[n] ∗h[n] = h[n] ∗x[n]
	- Asociativita: (Associative property)
		- {x[n] ∗h1[n]}∗h2[n] = x[n] ∗{h1[n] ∗h2[n]}
		- Sériové zapojení systémů h1[n],h2[n] lze nahradit systémem s impulsní odezvou heq = h1[n] ∗h2[n]
	- Distributivita: (Distributive property)
		- x[n] ∗{h1[n] + h2[n]}= x[n] ∗h1[n] + x[n] ∗h2[n]
		- Paralelní zapojení systémů h1[n],h2[n] lze nahradit systémem s impulsní odezvou heq = h1[n] + h2[n]
###Kruhová konvoluce
- Jsou-li x[n] a h[n] dvě konečné sekvence s N-bodovou DFT X[k] a H[k]
- pak sekvence s DFT rovnou Y [k] = H[k]X[k] je dána vztahem
- ![](http://s33.postimg.org/dyxv7dgsf/kruh_konv.png)
- Jedná se tedy o konvoluci h[n] s periodicky prodlouženým signálem x[n] vyhodnocenou na jedné periodě o délce N
- Kruhová konvoluce obecně NEMÁ stejnou hodnotu jako lineární  konvoluce
- Při vhodném doplnění nulami se však používá právě pro rychlý výpočet lineární konvoluce (výstup z FIR ﬁltru) pomocí DFT

##Rychlý výpočet lineární konvoluce pomocí FFT
- Výpočet DFT je možné provést efektivně pomocí Rychlé  Fourierovy Transformace (FFT)
- Tento postup je nevhodný pro dlouhé sekvence x[n]
	- Při vyhodnocování konv. sumy získáváme výsledek po vzorcích
	- Při výpočtu DFT výsledek celý najednou - zpoždění
	- Toto negativum se v praxi obchází blokovým výpočtem konvoluce
###Overlap-Add (Bloková konvoluce)
- Overlap-Add (OA,OLA) poskytuje efektivní postup pro vyhodnocení konvoluce dlouhého signálu x[n] s impulsní odezvou FIR ﬁltru h[n] (délka L)
![](http://s33.postimg.org/s1thkqudb/overlap_add.png)
###Overlap-Save (Bloková konvoluce)
![](http://s33.postimg.org/wp0x8mwjj/ovelap_save.png)
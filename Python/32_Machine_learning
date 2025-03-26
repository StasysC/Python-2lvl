# Tiesinė regresija
## Dėmesio!
Statistikos ir matematikos čia neaptarinėsime, tik patį modelio veikimo principą, labai paviršutiniškai. Šios paskaitos yra orientuotos į rezultatą, o ne teoriją. Kam įdomu, pasistudijuokite savarankiškai.

## Mašininis mokymąsis
Mašininis mokymasis (Machine Learning) yra dirbtinio intelekto atšaka, automatizuojanti analitinio modelio kūrimą. Jis naudoja neuroninius tinklus, statistinius, fizikos metodus, siekdamas duomenyse atrasti paslėptas įžvalgas, kai tiksliai negalima pasakyti, kur ieškoti ar ką daryti. Nuo įprasto programavimo skiriasi tuo, kad kad žmogus paduoda duomenis, atsakymus ir gauna taisykles, kurios vėliau gali būti naudojamos naujiems duomenims apdoroti. Kai tuo tarpu klasikiniame programavime, žmogus paduoda ir taisykles ir duomenis.

![](https://github.com/StasysC/Python-2lvl/blob/master/Python/residuals.png)

Tiesinės regresijos veikimo principas - mūsų modelis stengsis nubrėžti tarp taškų liniją taip, kad iki jų būtų mažiausia įmanoma atstumų kvadratų suma. Vėliau, prognozuojant naujas reikšmes, jis remsis ta linija. Žinoma, esant daugiau negu dviems kintamiesiems, kaip šiuo atveju, x ir y, procesai pasidaro sudėtingi ir painūs, todėl turėkite omenyje, kad tai tik labai primityvus pavyzdys.

Pradėkime nuo bibliotekų importavimo:

```python
import pandas as pd
import seaborn as sns
```

Dirbsime su tuo pačiu automobilių DF, mėginsime apmokyti modelį, kuris atspės automobilio degalų suvartojimą

```python
mpg = sns.load_dataset('mpg')
print(mpg.to_string())

	mpg	cylinders	displacement	horsepower	weight	acceleration	model_year	origin	name
0	18.0	8	307.0	130.0	3504	12.0	70	usa	chevrolet chevelle malibu
1	15.0	8	350.0	165.0	3693	11.5	70	usa	buick skylark 320
2	18.0	8	318.0	150.0	3436	11.0	70	usa	plymouth satellite
3	16.0	8	304.0	150.0	3433	12.0	70	usa	amc rebel sst
4	17.0	8	302.0	140.0	3449	10.5	70	usa	ford torino
5	15.0	8	429.0	198.0	4341	10.0	70	usa	ford galaxie 500
6	14.0	8	454.0	220.0	4354	9.0	70	usa	chevrolet impala
7	14.0	8	440.0	215.0	4312	8.5	70	usa	plymouth fury iii
8	14.0	8	455.0	225.0	4425	10.0	70	usa	pontiac catalina
9	15.0	8	390.0	190.0	3850	8.5	70	usa	amc ambassador dpl
10	15.0	8	383.0	170.0	3563	10.0	70	usa	dodge challenger se
....


```
## Duomenų sutvarkymas
Patikrinkime, ar nėra tuščių reikšmių:
```python
mpg.info()
```

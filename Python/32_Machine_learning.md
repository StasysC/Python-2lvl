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
```
## Duomenų sutvarkymas
Patikrinkime, ar nėra tuščių reikšmių:
```python
mpg.info()
```
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 398 entries, 0 to 397
Data columns (total 9 columns):
 #   Column        Non-Null Count  Dtype  
---  ------        --------------  -----  
 0   mpg           398 non-null    float64
 1   cylinders     398 non-null    int64  
 2   displacement  398 non-null    float64
 3   horsepower    392 non-null    float64
 4   weight        398 non-null    int64  
 5   acceleration  398 non-null    float64
 6   model_year    398 non-null    int64  
 7   origin        398 non-null    object 
 8   name          398 non-null    object 
dtypes: float64(4), int64(3), object(2)
memory usage: 28.1+ KB

matome, kad yra problemų su horsepower stulpeliu.
```python
print(mpg[mpg['horsepower'].isnull()])
```


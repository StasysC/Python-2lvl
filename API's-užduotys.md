# 1
Sukurkite programą, kuri duoda įvestos valiutų poros dabartinį kursą. Naudokitės https://api.frankfurter.app/. 
Dokumentaciją rasite [Čia](https://www.frankfurter.app/docs/). Rezultatas galėtų atrodyti taip:
```python
get_rate('EUR', 'GBP')
# EUR-GBP:	0.84828

get_rate('ZZZ', 'GBP')
# Neteisingai suvestos valiutos. Galimų variantų sąrašas:
# ['AUD', 'BGN', 'BRL', 'CAD', 'CHF', 'CNY', 'CZK', 'DKK', 'EUR', 'GBP', 'HKD', 'HRK', 'HUF', 'IDR', 'ILS', 'INR', 'ISK', 'JPY', 'KRW', 'MXN', 'MYR', 'NOK', 'NZD', 'PHP', 'PLN', 'RON', 'RUB', 'SEK', 'SGD', 'THB', 'TRY', 'USD', 'ZAR']
```
# 2
Sukurkite programą, kuri atspausdintų jūsų rytdienos horoskopą, naudokite šį [resursą](https://aztro.readthedocs.io/en/latest//).

# 3
Naudodami tą pačią Frankfurter API (kaip ir pirmoje užduotyje), sukurkite programą, kuri pagal parametruose pateiktas valiutų poras, 
periodo pradžios ir pabaigos datą surastų dienas kai kursas buvo aukščiausias ir kai kursas buvo žemiausias
Maždaug taip:

```python
currency_pair_analysis('EUR', 'GBP', '2019-01-01', '2019-12-31')

    # Valiutų poroje EUR-GBP, periode nuo 2019-01-01 iki 2019-12-31:
    # Žemiausias kursas buvo 2019-12-09 - 0.84116
    # Aukščiausias kursas buvo 2019-08-12 - 0.92203
```





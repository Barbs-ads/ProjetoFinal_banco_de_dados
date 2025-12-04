# 😸 Sistema de Clínica Veterinária Gatices

Este repositório contém a documentação e os scripts SQL para a Clínica Veterinária **Gatices**, um sistema desenvolvido para um ambiente *Cat Friendly* (exclusivo para felinos).

---

## 1. Cenário

### 1.1 Descrição
A **Gatices** é uma clínica veterinária exclusiva para gatos, com selo *Cat Friendly*, oferecendo ambiente livre de estresse, sem latidos ou cheiro de cães.

### 1.2 O Problema
A gestão de dados atual é precária e baseada em papéis, gerando riscos:
* **Identificação:** Confusão entre gatos com nomes e pelagens semelhantes.
* **Controle de Vacinas:** Perda de prazos para reforços (V3, V4, V5, FIV/FELV), deixando os animais vulneráveis.
* **Contato:** O cadastro atual limita-se a um único telefone, dificultando o contato em emergências quando o tutor viaja.

### 1.3 A Necessidade
O sistema visa resolver essas questões focando nas particularidades dos felinos, garantindo identificação correta, controle de múltiplos telefones de contato e centralização do histórico médico.


[Clique aqui para ver a o Cenário completo em PDF](banco_dados/cenario/Cenário.pdf)

---

## 🧩 Modelagem Conceitual

### **Entidades e Atributos**

## **TUTOR**
- id_tutor (PK)
- CPF_tutor
- nome_tutor
- email_tutor (multivalorado)
- telefone_tutor (multivalorado)
- logradouro, bairro, numero (Endereço: composto)
   
## **GATO**
- id_gato (PK)
- nome_gato
- raca_gato
- cor_gato
- dataNasc_gato
- idade (derivado)

## **PRONTUARIO**
- id_prontuario (PK)
- alergias_prontuario 
- observacoes_gerais_prontuario
- 
## **CONSULTA** 
- id_consulta (PK)
- data_consulta 
- motivo_consulta
- peso_atual_consulta
- status_fivfelv_consulta
- diagnostico_consulta

## **VACINA** 
- id_vacina (PK)
- nome_vacina 
- fabricante_vacina
- reforco_dias_vacina

## **VETERINARIO**
- id_veterinario (PK)
- nome_veterinario
- especialidade_veterinario

## **MEDICAMENTO**
- id_medicamento (PK)
- nome_medicamento
- princAtiv_medicamento

## 🔗 Relacionamentos e Cardinalidades

| Nº | Entidade A | Entidade B | Cardinalidade | Descrição | 
|----|------------|------------|---------------|-----------|
| 1 | TUTOR | GATO | 1 : N | Um tutor pode ter vários gatos mas um gato só pode ter um tutor responsável |
| 2 | GATO | PRONTUARIO | 1 : 1 | Cada gato tem um único prontuário e um prontuario é referente somente a um gato | 
| 3 | PRONTUARIO | CONSULTA | 1 : N | Um prontuário pode ter várias consultas e uma consulta especifica fica registrada em somente um prontuário |
| 4 | VETERINARIO | CONSULTA | 1 : N | Um veterinário realiza várias consultas  | 
| 5 | GATO | VACINA | N : N | Um gato pode receber várias doses de vacinas e um tpo de vacina pode ser aplicado em diversos gatos | 
| 6 | CONSULTA | MEDICAMENTO | N : N | Uma consulta pode ter vários medicamentos prescritos e um medicamento pode ser usado em várias consultas |


Vizualize o projeto DER feito no Draw.io: [Diagrama de Entidade Relacional](https://viewer.diagrams.net/?tags=%7B%7D&lightbox=1&highlight=0000ff&edit=_blank&layers=1&nav=1&title=DERfinal.drawio&dark=auto#R%3Cmxfile%3E%3Cdiagram%20name%3D%22P%C3%A1gina-1%22%20id%3D%22vLd22eKHMPMLas6_fcbh%22%3E7V1bc6O4Ev41rtp5cApxEfgxt5nZOptUajKb3dmXlGxkmzmAGMCJs79%2BhQ22ETJDiC5MkqcEgQV8ra%2FV6m41I%2Bs8Wn9KUbK8Ij4OR6bhr0fWxcg0gWGb9E%2FR8rRtcWDZsEgDv7xo33Ab%2FIurX5atq8DHWe3CnJAwD5J644zEMZ7ltTaUpuSxftmchPW7JmiBGw23MxQ2W%2F8K%2FHy5bfVMd9%2F%2BGQeLZXVnACfbMxGqLi7fJFsinzweNFmXI%2Bs8JSTf%2Fhetz3FYgFfhsv3dxyNndw%2BW4jjv8oNvSWjcrH8ff%2F%2BO79aPFxG8%2FudqzOmlbMrypwqDHK%2FpubNlHoW0AdB%2FH5dBjm8TNCuueKSSp21ZnpL%2F43MSkpQ2xiSm587mQRgyTSgMFjE9nNE7Ytp%2B9oDTPKCIn5YnosD3i1ufpWQV%2B7h4fIMebR%2FrAYWr8rFGJgyL55oT%2BuiHDwx%2FrEh1YpxthtQpvcA0k%2FWmn%2Bo8%2FW9R%2Ft10NOX2cvz6LEEx9ydhEOPxshwWxa0BcEamw%2B3MPKHnLwK0SFGE6L%2BXcR74yMfjLzhEs4DEKKJAEXrmt4vLLx%2Bqe1M5b29ffyTaPO38mBt85igKwqftY54mOclG5nlxNYqzcYbTYH4MAhQVUo%2BnWVK%2F%2F5HH2kqpat6Iksodrw8GXTluP2ES4Tx9opcsD6hllTx63NPQqdrKXqBRHj%2FVlQgqlcBi1%2FOeJ%2FSfkip82vzvY3x77T386X6d0MEEr8LrdTo24bZj7De0R5NIZJXOcEtnTcIV3d6WhyTNl2RBh0F4uW9lqLG%2F5g9CkpKj33GeP5UKFa3oCKoxGMf%2BaaEe97ykLR%2BDAoZNl7NV%2BrDpH%2BzklaN0gfOWF%2FE4FOVJNaUjOw8e6siJl5H7LqPmi7iDklGn6Yc32Ryg1JhPGm%2F4lSKb9tI5dlPnAKOuc2xQ1zmmIUDpxOlfaLX6%2B084%2FefR8YLPTz8%2B%2FxjTCUTcgLb0DGiKw9%2Fl7zcH34qDE6c6vFgfnrx42h21E6E59vkA2orGOv%2FuXs1SRdMKeKMpxVb5MzL7A02pzd1OieMmFqb2UfkoBZIJCeJ88%2BbO2ci5KI2EUqDA4bHrNwrY%2BfWHzvziol3%2BZGycABu6xyVQdndTPObBJWQ%2Bz6joWRHt7tpfQ1lKNNQnVFh4chSUZzJG0USWVWQrweoK%2B3Qol0axIMgqalW9mNA8cWqoQUcWao4S1O4wPRHEKA3EoQbqA42a33XIoCzIoBLIblKq%2BlZCEWOpCdwaYrYtCzG3C2K0nyDJ8JH1fRt2m0mi7MjmYRn497lMK2y3OqysMGlLP08ukg3kzm8%2BSgPNZWYGaToOdDL0BaIW0weXO%2BIcFjxpI84yRwIXsmYTdpWG%2F4m5M%2Fa%2FHZ7safn3WQI%2Fxy4VzwRTMRMoXjjFMyKXDZbH6F9pRqZliWTDq1oG9yKDXv9Pp%2BWVyHlhFeFUMhdMp84Fy5TGBZEeIWBr5QLQPi3oZUKnxbNAJkxRkMpmgs2sCC3oyIKv0ypaIHwhWaTIp5ySPbGyykQehJ1W1XsIsyVKikYKwjTEl7v2iBItKMCzhJgv4wgFobQByqDrSlsAPXMBrgbcHId4XuhPWYPXrsPrSZsIbZETId%2FPrm6JZD9vKqRHNzgNIryR8iudHy2R0VwL6pHwc6NYbTHTgURwq3Vel6hWq2DVRrU4GD4vmQg4R5KJNuEw8OGlmS8%2FiZIZ0JvUVGsVfBlG0Mx7J2stfDgUstaTJXuQ1XuFZL2WTVZgO0ycZ0hc7WT2V%2FZouiTRdJUVYjowOcrWAyvk5bZpQrJsFfSyTCHHMjXrlilksnbkBcWtSRd85YbeFhLTCyaMjS8t6GtzlJT8GJJM6FwmaCliDHIzh6okfCHzsa0pF3IofkJL5wxutwhOCglmJJWrPpgw6i6QLx66iUgSmMMhwWFM9c3wwFTMAx%2Fl6BplM7lkYKKoQFrkyFYdeEvR6NwanbpI2mTK5mFLS2axJYdqfJQtGTLWzDnkS3PYThh%2FuDyPrS0ydFm9mTaPLXDdukYGwByK31avnha5UapaSmkTszOZHIq58MOZ7rucCzmLdM%2FbmrNyToBj1%2Bk8sX9uYb0FMVfTgxgx6004MU68utYGJ4Znv4u5EDMQKGbAD%2FAoZLNl1tk8IDFrzUV1RLqFgKYwzU7MFoTs5Oz00to1OYoM2mqTs9CUWb3uP6q12cnZML13MRd7fETaYM6AskH1ZEZDrZSV7GPoEjVKpO9%2FAwbjtLGk%2BRscyQmiXQB9kLAHk809Zzb7OtLCcZ5IB46j13hgtI2rQ92oqk3Qir9OdkQy9nUz%2BsZm6AGlRZugyJWyw0%2B7%2BQXLz8CG5LUOe9WbeVGI00WAMhlzq1vPO4LGhClhYEvboVrV9BMz2DV5eV%2F9YJeciNR4WTLNcPqAZgRn9wucokDKsPeYCNakruFtaVs6oMg9B1CTy%2Fs1JrmWyqh3kivkL30HUWcJiKuzBKvMz0GkoUKRy4lhsunXn0Im1kuppaWEGQfDX2uzx6RKd6o2e7QIWD1zJa8dG9Lb5OUq8KXYTDVZR0R1Jm5%2BrsjMRKg73Ka%2FwIujU0dCyaW2GnTAWYJnAb2uSAyTwgvY7mN0pWUpuiJNbEf3tl7QDFAOJ3tIK2dcocaf7kA0NBl%2FsuHAdzEXIQORdHY1%2BUT3yYC6pzmtEQNXtet0Y%2FXJiBEw3xAAJpOE70qLEXgi8zJc7cmxNaX35vig2ruaBPHslL6XFE44LCeYXVqOCE7wi5z3o8QdfCKJk9yd%2FXDn8CuxTrPwpuprGIx46QzRJAH3nYGqFCT%2BRtNRZ%2F9Qm%2FSH6HkVV%2BHesM167Q7zuDRkenPaOCO5tPY5ibNVmEvbDOYBpnq7iDQYPt96ljrhdqZ734Opcg4%2FPvwUaK82%2BHUmwcwkEwM6DvthAxHfq%2BHCqbqipR%2BgRUwyOg0Q8TgyqwSXMYhcEYmL3CmxStoQomB0u8Dct61gVBcpjQh9Jwlk%2BEkNBygi0YhLBkskGXT7CV2VHqThkUF12DDBGblH%2BQqF4glhM4RgaiK5IpKQuCCqDjYVZTCU6xNXhD7hwqfaiZnldABm9%2FPgYY7DB%2FFAMn4baBmMtScESr6dIlAza99jJtlzo3W%2FEX9iHb3MccMX2CAcN%2BJS5iyrKqBZ5eEMyXPT7RtL6gs50jGV46iXiutQyNFjdpA5Isr%2BcId4zxg13%2FDiOzqVKbjaKkzC51e1Wptc6cEXKrjX%2F%2B3Voqh0lRKsuag0VwI9dzcPin9CDAVVORxcKbz0I8Zaqr0rz62vG9260nVbh%2F7QzIQvG0jpgmgZJLKMBYetVSzNWAAil0O66yRZu%2Foauj5IMjx7AvTM3WlzQ2gTsPEu4KaA1XzN%2FA7NgliaJw2YzHZIIXXu%2BakbPTUeH%2Fw3FahqGX%2FaRv8QyqXIpYbFeJnlRXBVO%2BlTPCfpjNz7RaUBwShadWMXmFVF%2BqqCDxDwfUI%2BjFoyjiUPQva79dK2mFVmvxj1rDfXWG1xsCFqZ9XJxnM0Tenam56WTQibLeMuInOPz4ieuQStyknfGs06JEWRZdqhipV4O36AZDF7rtRa53JtcrZrcgYnxruUt1LuWWie35lmj4vY%2Be1Z8pNUJ8H42Xf2tI2bTsv81%2BkOBQbzfXYgbQ1kiTQ%2FLY6t8%2Buan016Ds8ZVn2kt3fYp5L%2FEOM%2BAnf2gEk9gGoel4fy%2BKkl0g7STEFmhnxxwdYmB7XuMOVD%2FtIUBou%2FveiVcRB4jENqSBQcaIqWGmOD3SUgLfhq91zZt2VYa1vwTWrmBl3wdfjY4yuLz7XW%2BBsalxTmOvbxtdPDlBRrs71eoy%2B5vCJ%2BMQlc%2Fgc%3D%3C%2Fdiagram%3E%3C%2Fmxfile%3E))
 
---

## 🧱 Modelagem Lógica

### **Tabelas Derivadas do Modelo Conceitual**

## **TUTOR**
- id_tutor (PK)
- CPF_tutor
- nome_tutor
- logradouro, bairro, numero (Endereço)
  
## **TELEFONE_TUTOR** 
- id_telefone (PK)
- id_tutor (FK)
- telefone_tutor
- tipo_contato_tutor
  
## **EMAIL_TUTOR**
- id_email (PK)
- id_tutor (FK)
- email_tutor
  
## **GATO**
- id_gato (PK)
- id_tutor (FK)
- nome_gato
- raca_gato
- cor_gato
- dataNasc_gato
- idade (derivado)

## **PRONTUARIO**
- id_prontuario (PK)
- id_gato (FK)
- alergias_prontuario 
- observacoes_gerais_prontuario
- 
## **CONSULTA** 
- id_consulta (PK)
- id_prontuario (FK)
- id_veterinario (FK)
- data_consulta 
- motivo_consulta
- peso_atual_consulta
- status_fivfelv_consulta
- diagnostico_consulta

## **VACINA** 
- id_vacina (PK)
- nome_vacina 
- fabricante_vacina
- reforco_dias_vacina

## **GATO_VACINA** 
- (id_gato, id_vacina) (PK)
- id_gato (FK)
- id_vacina (FK)
- dataAplicacao_vacina
- dataReforco_vacina
- lote_vacina

## **VETERINARIO**
- id_veterinario (PK)
- nome_veterinario
- especialidade_veterinario

## **MEDICAMENTO**
- id_medicamento (PK)
- nome_medicamento
- princAtiv_medicamento

## **CONSULTA_MEDICAMENTO**
- (id_consulta, id_medicamento) (PK) 
- id_consulta (FK)
- id_medicamento (FK)
- dose_medicamento
- frequenciaUso_medicamento


## 🔗 Relacionamentos e Cardinalidades

| Nº | Entidade A | Entidade B | Cardinalidade | Descrição | Chave Estrangeira |
|----|------------|------------|---------------|-----------|--------------------|
| 1 | TUTOR | TELEFONE_TUTOR | 1 : N | Um tutor pode ter vários telefones | TELEFONE_TUTOR.id_tutor |
| 2 | TUTOR | EMAIL_TUTOR | 1 : N | Um tutor pode ter vários e-mails | EMAIL_TUTOR.id_tutor |
| 3 | TUTOR | GATO | 1 : N | Um tutor pode ter vários gatos | GATO.id_tutor |
| 4 | GATO | PRONTUARIO | 1 : 1 | Cada gato tem um único prontuário | PRONTUARIO.id_gato |
| 5 | PRONTUARIO | CONSULTA | 1 : N | Um prontuário pode ter várias consultas | CONSULTA.id_prontuario |
| 6 | VETERINARIO | CONSULTA | 1 : N | Um veterinário realiza várias consultas | CONSULTA.id_veterinario |
| 7 | GATO | GATO_VACINA | 1 : N | Um gato pode receber várias doses de vacinas | GATO_VACINA.id_gato |
| 8 | VACINA | GATO_VACINA | 1 : N | Uma vacina pode ser aplicada a vários gatos | GATO_VACINA.id_vacina |
| 9 | CONSULTA | CONSULTA_MEDICAMENTO | 1 : N | Uma consulta pode ter vários medicamentos prescritos | CONSULTA_MEDICAMENTO.id_consulta |
| 10 | MEDICAMENTO | CONSULTA_MEDICAMENTO | 1 : N | Um medicamento pode aparecer em várias consultas | CONSULTA_MEDICAMENTO.id_medicamento |

Vizualize o MER feito do Draw.io [Modelo de Entidade Relacional](https://viewer.diagrams.net/?tags=%7B%7D&lightbox=1&highlight=0000ff&edit=_blank&layers=1&nav=1&title=Mer-final.drawio&dark=auto#R%3Cmxfile%3E%3Cdiagram%20name%3D%22P%C3%A1gina-1%22%20id%3D%22zXirNb4ilJaz9RcqFgmG%22%3E7Z1tc5u4FoB%2FTWZ6P2QngLGdj7abbdObl06Sdrf7JaMaxdZcDC7Gedlff4UNToyFfOogJODMdKYxIcTmPJEeHR2JI2c0e%2F4Ukfn0MvSof2SfeM9Hzscj27b63VP%2BX3LkZX3E7drrA5OIeelJrwdu2b80PXiSHl0yjy62TozD0I%2FZfPvgOAwCOo63jpEoCp%2B2T3sI%2Fe3fOicTunPgdkz83aN%2FMS%2Bero%2F27d7r8c%2BUTabZb7ayDzwj2cnpJ1lMiRc%2BvTnknB05oygM4%2FVXs%2BcR9ZObl92X9c%2F9WfDdzRuLaBBDfuDlbP65ezH0zwffeZys4a9p%2FPex4CrpoUX8kt0D%2Fs7nyZcx%2BZkcGi5iEsVpqJwTfoDf%2FJiwgEb8gLV67ftkvmCr09dHpsz3LshLuIyzC2Wvhg%2FsmXo360gl5%2FKgXfCLJS%2BTiz%2Fwi9%2Bmbyb5NvHZJOBfj%2Fk7Tn7jMKIL%2Fl4uyCJOz5jGMz%2F9cv1ZHom%2FTD%2FLp8HddXqQRjF9fvOZ09v2iYYzGkcv%2FJTpm8huiHx6xcBx0mPpZY7d7KSUdttNX5MUw8nm4q%2BR4l%2BkwfqNwNm7gZMFuCiaNwmRw2kYsX%2BTGPrpPX8b4dXrJzbzScBRJ17u0DBc%2FWmvIsV8fxT6YYJBEAZ0h4TkJC8K53ckmtA4PTAPWRCvbo875P%2F4DRud%2FOEeufy9jvhr6%2FU1%2F5ecHsWjMFjEEScuuQblgX%2BiSfCHcThPL%2BrTh%2Bz6URrD5OufYRyHsyI2DuLCkWDxsn1K6RA4QAjsQgj4j8aM%2BDe86STBxF%2BHbNWSkteQCeIqvNObu5u%2F7fk%2F4ZDf4wd%2F1RhOmedR%2Fuc8fJqymN7OyTg56Yl3Jnv%2BkL%2F%2Bt7RwScKTXuz1%2Fvz21YjPW6mAxPwPZRl4i52Yb97n4Rh0aoJB1nKvzx0ueLBZMLlY%2F2Q3x4lbEifMu5%2BQOCwLFsvdbvLLhcfK9xcV0GMhPjJ8%2BC1RhI7Vrz07LlrIeyzkpEoL6aqykC4QAldz%2B0E9ll2vLAlBBUlj26sJA3v7kDKoCPjtROmQSwe052gFMI8kGk9J9ME9%2BQ%2FKRiEKfZSN2sjGqSrZOAVC0EfZaKxsZElW4yGopPOIyJigbciBgQ5RWgFMZhs22oaMGcHUGOqGobph2ap8w7KhGBRzgMZRe%2BOAzrRpp6CSHmQcRmgccmCgCbF2AIPKAYIGMxxlKUf5hqGskseCpjQs3aOT0gwDhSLzVfODXkn%2F4JGYXJHFGK1CTg14TNoWaijqRDEtWJ1hrk7I8HpfYTA012nrnlpVkLD4E4tCN%2BGFjkC1c1BJX8G8%2B3gZ8zeJclHEAXT02RJgsPBTxoAgLb6rEfy%2Bxdu3WRQF3k2H%2F6M5IgSQ7Cz8SSLDxsQfpN%2BY8VivmIuSz00zC1mVBa89hTeK%2BdUI%2Bbg7f%2FDXq3VsZEJn%2FOuLo5FzNHQm%2FDeVBUQnB8RxJ2cHyhaMCPLYzV7vdfft7vrmoLjBFnzZ25FTNg%2FlQKv0sxCjzW93Ig1Z8QUd02W84JqvZuq9Ax3maQdB16ov1H15xT5U91sKEOq%2FjAlocgFtxIDqKGUrvxxwG9LT3IZgcZTCxgA6ga2dgupWf6F8yOUDkcH1X7%2B9zQW0ZgKlwwDpULYCrAMtgsh4QelooHR0BBMQZlJQSQ8y%2BvonOsee5cPQ7qMdxGTOYXXQOSQsQBd%2BoHMY4BzqloF1oNNvnWIOUDpqLx3Q2TftFFTShfjhJCJeuIxCdI897gEes7QCHMx3gFob8BQvukeD1oN1oHNrGR%2F1Vw00iw50Jk170CvpIH4SFqFV7LUKcA6sFdDgInNQSwOeekOraNCysIy0%2FW3FKVpFU6zCBQ87dQe9msqM5YyiVey1CmjKux3QYCGotIURZESbvaCIzgjz39GGbOYoZMuKcuvB1K0nccGb9xcv%2Bmy1DTZjWZEL3r9f90gSlxWpbc%2BheSjtIOhaVvTe9r8dDlmb9gQXFxkHjwvNUKGTGFBzo%2B6xUtCMlat7HIolN%2Boagy40haWdgkqyEWgfEPsAS2wrmMFqG1BDY6N11Mc6lK0u6kKz3xkvTbIO3D7xNbzQgm%2FtHOD2iUb0H33oqLUlwGCKQ8aAwFCbPW0WU44bp%2FU9M2euxAuymbPKshPgP%2FfirdhbrYvNmDjrQZNUXd1DTZw4U7ujCTRPpR0Ebfvxvb8HaIdIgkce7SQJxVLWDEGzWKglBmSxlNlpD5rFynhpUhYLnSQLLrQn0U5BJSkJFBCggEB3OWgHNpuNclycPpOwAIUGxcMA8VA2fdaD1pP3dD9ECMVDYWMALf%2FUTkE14sHm4f0qVx%2Fj6rN98lGbBgTXtOuAZuwPvv71T%2Fh9fnP8dHP763McXPw8xqSHwUvay9iTTxh1QY5DRkeTTKOdhTrC6ApyHEZSgGU6RnQVgmFqi3HBuRSJLVgnAhdtdpXO97O7s5vzq8HN%2BfVBYEAWtztdBYJQEEDoOHQTajTDJlbpWCfQFSEbZLBOp%2Fa6WBBgaOGefhR0Veo8Uh4GFpCIhSiShXhYCBLK5TvwgVaOopuYMGOmrFTHsqCVoxtkmpTJQjHZRBeaxdbPQXXP0UQVgaBjg%2FuSdqCDK95hLQ60ShQVxAQFUVa0Y1nQQtENMqggjVQQaBGffg6q2W1nMadj%2FlmYRzx0EaCLwIczrWAIK3hy2Px47HcXt9dPX%2Frsn%2FPrL1fsB7s4FkDT7Jm2rzfXV3ffDp9og6yFz%2B0i7fRKEAhh9AQjV1mU0SJrPskmDK5gMCGDBSfYai%2BRwvAKhhJGYqBrcm0e8esuS5XIvlKJzMtFFTaAEFU0sWZvo2Nb5bKTL%2B2pgB3BEBZdxNCMVhmTasLgCgr3ZLBgNquBIiKo%2FTOSgUqyEMSn0YSRBeoHRD%2BgfUgr0Nmsfz8pMYPVPO8QVJiidxjqHWXMpAmDKygJlMGC3tFA7xAV9hkJQSW9R%2FhzQaNHMg7p4n5CeROBCgKCCDqCaQVEqCCgtY3Q3gcVpEGr4EXdjYyOJjkHLoN%2FxUAwg24kBlWtg5%2BQGP2iGBcbccEZFaCLCjKpzS7O%2BTS4uz7%2BPhidXw0O4mITdFl1jmttK0JHWVbCAuemihcqttoMm1GgI1qwKuUFS3Rq74riqglohko7CFrqKz5s7HG0upP3j8lvJcrKd2tV9C0GSjD4QKBwJTwMHsFQBO3E1KkzZSU7Nrh%2B2NbchuDkmcLGAFz5qZuCShITHonJYO6zMRmTMPUQ1JBCJqB1O62Bh6J3FEMAnWJF7zDAO5Qlx2xonahdvAcCekftvQOaItVOQWXecUMfwmiM1rEXHWhatTXooHWsriacT%2B1Ch7loHU2q0ulCH1PQ1b0pRmmW0SqpEMcS%2BrAB7UGvpGfww5iiTexjRjAqbTEzuHsOCBroGBalQoNU5IEoTyoEg1YpH%2FWXCqz9FYVXMAI1k4NaFv82zjGyfcCQlzUvWJ4hgwVc24NuUb1byPh6l1v0bGAb0SsuBUe3qL9b9KBPWdXOQVVugRmMPcRAU50tIQbtQiINjkBFm7226PLs4%2FlocHl2dafuEZsbw8%2BKNtVt%2Bgq1w%2BwdoB1ut0nNWFrkCGxRygsuLaq9LorjC53e1g6Crv1%2FZ3y8MiYzfncwQ1VMB7QMvKUYoVPKmICWgaOTGFDYq2xBkQOt73Z0b%2BOJhb0KGwPo1Lh2Cqp7qGamIBE6iAwIaEl4O8jBShwQNNBicHQPA9xD2aKi7Mlb%2BzHQvb8WuofCRyGBk6O6KaikB5lHLBgPYvaIORAQPeCcaivoQf8A7esoyL82ez5tdH11%2B%2B3i7sCN%2BnoSSchaku62NNhlPEZTHDzozLnkybmtlsfaTaaJowtdNpTxgpNptfdHcXyha4G0g6BrMo1%2FlMXSj7EaqxAN0S4nyBDOpMEaIEHyHIXE1GxWGTNp4uhC15lJlgBgNqv2NgJdZaadgsq2yEH%2F2O8f4C6kLdTg7jgSWqArE1E4DBCOMqbPxBhAH2aU8YLC0UDhyG6F%2BRRU0nXMwpg9hqgc%2B7mBDlfawU02cebixJmMBeg6VzQPA8xD3UZ9og3opcCgejRRPaBTcNopqKZyhy7CexIviY%2F6sZ8daJ6sHex4dMxmxP%2FA29WRjQZSjINoKTwaiCkb7SjbxE%2B0gl7KR%2F2FA%2F1CtF7ezKBX0kfwpileLu4f2OMD9R%2FRMfbzAx2ttoOfJL%2BBZlEMAdaVGmwWyrbwE62Dl%2FKBZtEAs4DW%2B2kPejWjT0YmQbiI2RhnTgDwQIs12gFPNnPi4MyJjAVwdSDaReV2YVvK7AKa5nR0P%2FMdNwhW%2BecvWupuJgdVbRA8j3jztSQRw8XNxdSAs57toAaXochggWZL0TA0GEZHlWF0oEnOjA80jGYaBjR9qZ2Dyh5BQPlNZwEqhhQbaPqzJdigYsgYEKRNm71vyvfB6PzqsF1TNgGSPYLAtbY9oaesZLMDzVp2ih%2FA3mo9bMa2KR1oHrKje6Uhbpuiti2HZia1g6Br2xR8hJWcIBcJQpU8GB5oQhx1xICVRMo2TXGhGe6MlyZlr9BFsuBCU9faKaju8QNoH3se5w7tQNrBDG78C2powJMlaB36rUPZzikudK7E1b34EK1DYWMAnfrQTkElPcgD%2BRmxMQlidI%2B97gEetbSCHHQPUHMDXXOA7mGAe6jbO8WFTsS5xRygfNRePqDzcNopqKQLiehDGI3De4%2BRBerHPv0Ap8tawQ5OtMhg6QlGOc2u2cmedXR8efbxfDS4PLu6uz4IkE30f%2BO5R27fVeQNPag%2F9oqftNpqf2xGAU8Pqo893Y0%2FFvCobdihBqkdBC3lFx%2B2Hnw0Wt3Nt4%2FULC1VYZ%2Bo9MvN1Sskq49kVeWbOXbKHpxogKcHrQpDTTEgzaWssCdT5%2F0Y6H4uL2a5FPYk0IkS7RRUs89OuKAqHuvdQAUB9yLtACfdHtgtd3vg5tlHH5oaRfswwD6UFfj0oXVeGS9oH020D2iZl3YKqinwieivJQ3GjHxbhKghEIJOoaOYdhCkYqu%2FBjoItK4QHcQAB1FX6NOHTtj1izmorYTgzjyv4YXO2GnnoKqdecreY7iB4gFNnLWEGZxykcGCSQ9zd%2F5T90ykU2iSI%2BMD%2FaKRfnEKTXNo56Aqv8DcBgQb6DC1JdigYsgYSMey1JvQN7dGXFYcLqNxetbL2fxz92Lonw%2B%2BTy9Da%2FhrGv8tei5Gct2sTodfj8UvN9QnMQuDs9fvrKt51h5i2dvxpIE3iKIVAmc3HLK78JIELwlIyT2hmaesf3GcGUfRx7V38NgPwiYs0eqdP27fJ1n8BDh8DVc8blqbfUmL9T1Pf%2Bo1%2FDsX6uT3Jc5dZ31ndq5TGka9ZmBEn1n8d%2FL1H6e8912%2F%2FrF6baWvPj6%2FOfXjy5sXX2nEZnRV116ApPDTdk1j0u7lmDzJVb4fymT%2BYRyqmTxtBpNAjrKHdhvD0U7blo9%2FTTjafPRSQNp1rnI5mpHAu1652Gp0L%2FrGQT3nqWl0dbahcPLDcTBduQvZ%2BQspx8uuEV7vNrBuzzCQjjerwTKSDnWw49yFqpYw68Q5jCTo5p6GodSzTEepf2ijlEepV3mj1DkMpR%2BP%2Fe7i9vrpS5%2F9c3795Yr9YBfmN0rZY5aMIWlTQZfGv3Nom%2BSc7mnclIPklti7WSfGN0rZ4zSMQambI8DKLw2BotTLXSh%2FHeUkHZiqEl%2FNpPGcdALYWJAO9qQ8SNV70oHZKmHn5uxuumAYSVme3xiS7NzeCt38bhzg3m1nk4aySOIvozCM354ekTnviTyanPF%2F%3C%2Fdiagram%3E%3C%2Fmxfile%3E)

---

## 🛠 Modelagem Física

A Modelagem Física consiste na transformação das tabelas acima em comandos SQL de criação, relacionamento e restrições (PK, FK, UNIQUE).  
Inclui:

- Criação do banco de dados  
- Criação das tabelas  
- Definição de relacionamentos  
- Definição de atributos multivalorados através de tabelas auxiliares  
- Aplicação de chaves primárias, estrangeiras e restrições  
[Clique aqui para ver a Modelagem Física em PDF](banco_dados/modelagem_fisica/modelagem_fisica.pdf)
---

## 📊 Dados

Exemplos de dados previstos no sistema:

- Cadastro do tutor com múltiplos e-mails e telefones  
- Registro do gato vinculado ao tutor  
- Prontuário exclusivo do gato  
- Associação do gato aos veterinários que o atenderam  
- Lista de medicamentos utilizados pelo gato ao longo da vida

[Clique aqui para ver as inserções dos dados em PDF](banco_dados/dados_tabelas/dados_tabelas.pdf)

---

## 🔄 CRUD

### **CREATE**  
Cadastro de tutor, gato, veterinário, medicamento e prontuário.

### **READ**  
Consultas para listar gatos, prontuários, vacinas pendentes, contatos dos tutores, etc.

### **UPDATE**  
Atualização de dados como endereço, telefone, status FIV/FELV, reforço de vacinas.

### **DELETE**  
Exclusão de registros respeitando integridade referencial do banco.

[Clique aqui para ver as operações CRUD em PDF](banco_dados/crud/crud.pdf)

---

## 📈 Relatórios

O sistema deve fornecer relatórios como:

- Lista de gatos e seus respectivos tutores  
- Histórico de consultas por gato  
- Status FIV/FELV e vacinas pendentes  
- Lista de veterinários que atenderam cada gato  
- Medicamentos já aplicados ao longo da vida  
- Agenda de consultas (ordenada por data)  

[Clique aqui para ver a Modelagem Física em PDF](banco_dados/relatorio/relatorio.pdf)

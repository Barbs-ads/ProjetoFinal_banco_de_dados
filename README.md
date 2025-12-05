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


[Clique aqui para ver a o Cenário completo em PDF](banco_dados/cenario2.0.pdf)

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


Vizualize o projeto DER feito no Draw.io: [Diagrama de Entidade Relacional](https://viewer.diagrams.net/?tags=%7B%7D&lightbox=1&highlight=0000ff&edit=_blank&layers=1&nav=1&title=DERfinal.drawio&dark=auto#R%3Cmxfile%3E%3Cdiagram%20name%3D%22P%C3%A1gina-1%22%20id%3D%22vLd22eKHMPMLas6_fcbh%22%3E7V1bd6M2EP41Pqf74BzEReDH3Ha3p01OTrNNu33JkY1sswXEAk6c%2FvoKG2wjZJYQXdgkTwkCC%2FhG32g0MxpG1nm0%2FpSiZHlFfByOTMNfj6yLkWkCwzbpn6LladviwLJhkQZ%2BedG%2B4Tb4D1e%2FLFtXgY%2Bz2oU5IWEeJPXGGYljPMtrbShNyWP9sjkJ63dN0AI3Gm5nKGy2%2FhX4%2BXLb6pnuvv0zDhbL6s4ATrZnIlRdXL5JtkQ%2BeTxosi5H1nlKSL79L1qf47AAr8Jl%2B7uPR87uHizFcd7lB1%2BT0LhZ%2Fzr%2B9g3frR8vInj9z9WY00vZlOVPFQY5XtNzZ8s8CmkDoP8%2BLoMc3yZoVlzxSCVP27I8Jf%2FicxKSlDbGJKbnzuZBGDJNKAwWMT2c0Tti2n72gNM8oIiflieiwPeLW5%2BlZBX7uHh8gx5tH%2BsBhavysUYmDIvnmhP66IcPDL%2BvSHVinG2G1Cm9wDST9aaf6jz9b1H%2B3XQ05fZy%2FPosQTH3J2EQ4%2FGyHBbFrQFwRqbD7cw8oecvArRIUYTov5dxHvjIx%2BM%2FcIhmAYlRRIEi9MwvF5d%2FfKjuTeW8vX39kWjztPNjbvCZoygIn7aPeZrkJBuZ58XVKM7GGU6D%2BTEIUFRIPZ5mSf3%2BRx5rK6WqeSNKKne8Phh05bj9hEmE8%2FSJXrI8oJZV8uhxT0Onait7gUZ5%2FFRXIqhUAotdz3ue0H9KqvBp89vH%2BPbae%2FjT%2FTKhgwlehdfrdGzCbcfYb2iPJpHIKp3hls6ahCu6vS0PSZovyYIOg%2FBy38pQY3%2FN74QkJUe%2F4Tx%2FKhUqWtERVGMwjv3TQj3ueUlbPgYFDJsuZ6v0YdM%2F2MkrR%2BkC5y0v4nEoypNqSkd2HjzUkRMvI%2FddRs0XcQclo07TD2%2ByOUCpMZ803vALRTbtpXPsps4BRl3n2KCuc0xDgNKJ07%2FQavX3n3D6z6PjBZ%2Bfvn%2F%2BPqYTiLgBbekZ0BSHv8vfbw6%2BFgcnTnV4sT48efG0O2onQnPs8wG0FY11%2Ft29mqWKphXwRlOKrfJnZPY7mlKbu50Sx00sTO2j8lEKJBMSxPnmzZ2zkXNRGgmlQIHDY9cvFLDz6w%2Bd%2BcVFu%2FzJ2DgBNnSPS6Ds7qZ4zINLyHyeUdGzItrdtb%2BGspRoqE%2BosPDkKCjPZIyiiSyryFaC1RX26VAujWJBkFXUqnoxoXni1FCDjizUHCWo3WF6IohRGohDDdQHGjW%2F65BBWZBBJZDdpFT1rYQixlITuDXEbFsWYm4XxGg%2FQZLhI%2Bv7Nuw2k0TZkc3DMvDvc5lW2G51WFlh0pZ%2BnlwkG8id33yUBprLzAzSdBzoZOgLRC2mDy53xDkseNJGnGWOBC5kzSbsKg3%2FE3Nn7H89PNnT8u%2BzBH6OXSqeCaZiJlC8cIpnRC4bLI%2FRv9KMTMsSyYZXtQzuRQa9%2Fp9OyyuR88IqwqlkLphOnQuWKY0LIj1CwNbKBaB9WtDLhE6LZ4FMmKIglc0Em1kRWtCRBV%2BnVbRA%2BEKySJFPOSV7YmWViTwIO62q9xBmS5QUjRSEaYgvd%2B0RJVpQgGcJMV%2FGEQpCaQOUQdeVtgB65gJcDbg5DvG80J%2ByBq9dh9eTNhHaIidCvp9d3RLJft5USI9ucBpEeCPlVzo%2FWiKjuRbUI%2BHnRrHaYqYDieBW67wuUa1WwaqNanEwfF4yEXCOJBNtwmHgw0szX34QJTOgN6mp1ir4MoygmfdO1lr4cChkrSdL9iCr9wrJei2brMB2mDjPkLjayeyv7NF0SaLpKivEdGBylK0HVsjLbdOEZNkq6GWZQo5latYtU8hk7cgLiluTLvjKDb0tJKYXTBgbX1rQ1%2BYoKfkxJJnQuUzQUsQY5GYOVUn4QuZjW1Mu5FD8hJbOGdxuEZwUEsxIKld9MGHUXSBfPHQTkSQwh0OCw5jqm%2BGBqZgHPsrRNcpmcsnARFGBtMiRrTrwlqLRuTU6dZG0yZTNw5aWzGJLDtX4KFsyZKyZc8iX5rCdMP5weR5bW2TosnozbR5b4Lp1jQyAORS%2FrV49LXKjVLWU0iZmZzI5FHPhhzPddzkXchbpnrc1Z%2BWcAMeu03li%2F9jCegtirqYHMWLWm3BinHh1rQ1ODM9%2BF3MhZiBQzIAf4FHIZsuss3lAYtaai%2BqIdAsBTWGanZgtCNnJ2emltWtyFBm01SZnoSmzet1%2FVGuzk7Nheu9iLvb4iLTBnAFlg%2BrJjIZaKSvZx9AlapRI3%2F8GDMZpY0nzNziSE0S7APogYQ8mm3vObPZ1pIXjPJEOHEev8cBoG1eHulFVm6AVf53siGTs62b0jc3QA0qLNkGRK2WHn3bzE5afgQ3Jax32qjfzohCniwBlMuZWt553BI0JU8LAlrZDtarpJ2awa%2FLyvvrBLjkRqfGyZJrh9AHNCM7uFzhFgZRh7zERrEldw9vStnRAkXsOoCaX92tMci2VUe8kV8hf%2Bg6izhIQV2cJVpmfg0hDhSKXE8Nk088%2FhUysl1JLSwkzDoY%2F12aPSZXuVG32aBGweuZKXjs2pLfJy1XgS7GZarKOiOpM3PxckZmJUHe4TX%2BBF0enjoSSS2016ICzBM8Cel2RGCaFF7Ddx%2BhKy1J0RZrYju5tvaAZoBxO9pBWzrhCjT%2FdgWhoMv5kw4HvYi5CBiLp7Gryie6TAXVPc1ojBq5q1%2BnG6pMRI2C%2BIQBMJgnflRYj8ETmZbjak2NrSu%2FN8UG1dzUJ4tkpfS8pnHBYTjC7tBwRnOAXOe9HiTv4RBInuTv77s7hF2KdZuFN1dcwGPHSGaJJAu47A1UpSPyNpqPO%2FqE26Q%2FR8yquwr1hm%2FXaHeZxacj05rRxRnJp7XMSZ6swl7YZzANM9XYRaTB8vvUsdcLtTPe%2BB1PlHH58%2BCnQXm3w60yCmUkmBnQc9sMGIr5Xw4VTdUVLP0CLmGR0GiDicWRWCS5jELkiEhe5U2KVtCFEweh2gblvW8GoLlIaEfpOEsjwgxoOUESiEZcMlkgy6PYTuio9SMMjg%2BqwYYIzco%2FyFQrFE8JmCMHURHJFJCFxQVQdbCrKYCjXJ64IfcKFT7UTM8vpAMzu58HDHIcP4oFk%2FDbQMhhrTwiUfDtFoGbWvsdMsudG634j%2FsQ6epnjhi%2BwQThuxKXMWVZVQLPKwxmS56bbN5bUF3KkYyrHUS8V16GQo8fsIHNElP3hDvGeMWq%2B4cV3dCpTcLVVmITPr2q1NrnSgy9UcK%2F%2F26tFUekqJVhzUWmuBHrubh4U%2F4QYCqpyOLhSeOlHjLVUe1eeW183unWl67YO%2FaGZCXP0nywbwWFLFEuzEYDIVZDu8kjWrqyGru%2BQDM%2BMAD1Tdtq8D9oEbLwLuClgNR8xv0OzIJbmQAMmswtSSHl7fsZGT43HB%2F9Nxadaxp%2B20T%2BEKilyqWExzmV5gVvVvvkUz0k6I%2Fd%2BUWBAMIpW3cYFZlWIvircAwR8lpAPo5ZEY8mDkP1cvbSdZZW1L0Y9600xVlsTbIjaWXWO8RxNU7rkpqdlE8Jmq7eLSNjjM6JnCkGrctK3RrMOSVEkl3YoXiXejh8gWcyeK7XWuVybnO2anMGJ8S7lrZR71pfnd6bZ4yJ2fnuW%2FCSVRzB%2B9Hk9beOm0zJfvRc0J1G%2FSbaDGxQYzOfYgbS1jyXS7LQ4Ns7Pa3Y2aTk8J1j1Td7eUZ5K%2FkMM8wjcyAMm9XipeVweysOllkj7RzMFmZnxxfVZmxzUuqGUD%2FlLMxYs%2Fm6iV8ZB4DGOqCFRcKAZWQkV4ywNeu4X7mRpsDsCpEVc7Z7L%2BbZsam2rvEnN1qCrvA4fdnxlQbnWen5DI5LCvMY%2BDnZ6mJJiQbZXavQll1fEL2aAy%2F8B%3C%2Fdiagram%3E%3C%2Fmxfile%3E)

 [Clique aqui para ver a o DER em PDF](banco_dados/DER_print2.0.pdf)
 
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

[Clique aqui para ver a o MER em PDF](banco_dados/MER_print2.0.pdf)

---

## 🛠 Modelagem Física

A Modelagem Física consiste na transformação das tabelas acima em comandos SQL de criação, relacionamento e restrições (PK, FK, UNIQUE).  
Inclui:

- Criação do banco de dados  
- Criação das tabelas  
- Definição de relacionamentos  
- Definição de atributos multivalorados através de tabelas auxiliares  
- Aplicação de chaves primárias e estrangeiras
  
[Clique aqui para ver a Modelagem Física em PDF](banco_dados/modelagem_fisica2.0.pdf)

---

## 📊 Dados

Exemplos de dados previstos no sistema:

- Cadastro do tutor com múltiplos e-mails e telefones  
- Registro do gato vinculado ao tutor  
- Prontuário exclusivo do gato  
- Associação do gato aos veterinários que o atenderam  
- Lista de medicamentos utilizados pelo gato ao longo da vida

[Clique aqui para ver as inserções dos dados em PDF](banco_dados/dados_tabela2.0.pdf)

---

## 🔄 CRUD

### **CREATE**  
Cadastro de tutor, telefone_tutor, email_tutor, gato, veterinário, medicamento, prontuário, consulta, vacina, gato_vacina e consulta_medicamento.

### **READ**  
Consultas para identificar gatos,  listar prontuários, vacinas pendentes, contatos dos tutores, etc.

### **UPDATE**  
Atualização de dados como contratação de novos veterinários.

### **DELETE**  
Exclusão de registros respeitando integridade referencial do banco.

[Clique aqui para ver as operações CRUD em PDF](banco_dados/crud2.0.pdf)

---

## 📈 Relatórios

O sistema deve fornecer relatórios como:


### 🐾 1. Identificação – Listagem de Gatos e seus Tutores
**Objetivo:** Exibir informações completas sobre o gato e seu tutor.  
**Problema resolvido:** Facilita diferenciar gatos com nomes e cores iguais, exibindo tutor e raça.


### 📞 2. Contato de Emergência – Telefones de um Tutor
**Objetivo:** Listar todos os contatos associados a um tutor específico.  
**Problema resolvido:** O cadastro antigo aceitava apenas um telefone; agora é possível visualizar vários, incluindo contatos de emergência.


### 💉 3. Controle de Vacinas – Reforços Vencendo
**Objetivo:** Identificar gatos com vacinas próximas do vencimento.  
**Problema resolvido:** Evita atrasos que podem deixar o gato vulnerável a doenças.


### 📚 4. Histórico Médico – Consultas por Gato
**Objetivo:** Exibir todas as consultas de um gato específico.  
**Problema resolvido:** Centraliza o histórico para evitar estresse no manejo e melhorar o atendimento.


### ⚠️ 5. Identificação de Risco – FIV/FELV
**Objetivo:** Listar gatos positivos para FIV ou FELV.  
**Problema resolvido:** Garante manejo especial e controlado para gatos com essas doenças.


### 💊 6. Medicamentos Receitados – Consultas e Prescrições
**Objetivo:** Exibir medicamentos receitados em cada consulta.  
**Problema resolvido:** Informa doses e remédios de forma precisa para manter o tratamento correto.


### 🧓 7. Gatos Sêniores – Check-up Geriátrico
**Objetivo:** Identificar gatos com 10 anos ou mais.  
**Problema resolvido:** Permite aplicar protocolos específicos para gatos idosos.


### ⚖️ 8. Monitoramento de Peso – Evolução do Peso
**Objetivo:** Acompanhar a evolução de peso dos gatos.  
**Problema resolvido:** Detecta perda de peso rápida, permitindo intervenção antecipada.


### 🧪 9. Rastreamento de Medicamentos Controlados
**Objetivo:** Identificar gatos em tratamentos com medicamentos controlados.  
**Problema resolvido:** Facilita a gestão e o controle desses remédios.


### ✉️ 10. Lista de E-mails – Campanhas de Vacinação
**Objetivo:** Reunir e-mails de tutores para envio de campanhas.  
**Problema resolvido:** Agiliza comunicação em massa sobre vacinas e eventos da clínica.


[Clique aqui para ver o Relatório completo em PDF](banco_dados/relatorio2.0.pdf)

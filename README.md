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


### **Relacionamentos**

| Relacionamento | Tipo | Descrição |
|----------------|------|-----------|
| Tutor → Gato | 1:N | Um tutor possui vários gatos |
| Gato → Prontuário | 1:1 | Cada gato possui um único prontuário |
| Gato ↔ Veterinário | N:N | Vários veterinários podem atender o mesmo gato e um gato pode passar por vários veterinários |
| Gato ↔ Medicamento | N:N | Um gato pode receber vários medicamentos e um medicamento pode ser usado por vários gatos |

Vizualize o projeto DER feito no Draw.io: [Diagrama de Entidade Relacional](https://viewer.diagrams.net/?tags=%7B%7D&lightbox=1&highlight=0000ff&edit=_blank&layers=1&nav=1&title=DERfinal.drawio&dark=auto#R%3Cmxfile%3E%3Cdiagram%20name%3D%22P%C3%A1gina-1%22%20id%3D%22vLd22eKHMPMLas6_fcbh%22%3E7V1dc5s4FP01nmkf7EGABDwmTtLd2TaTabrd7b50ZCPbdAF5ASd2f%2F0KG2wjcEIcXeSkebIRWIhzda7ul3DPGkbLDwmdzz5xn4U90%2FCXPeuiZ5rIsE3xkbesNi2YFA3TJPCLi3YNt8FPVv6yaF0EPksrF2ach1kwrzaOeRyzcVZpo0nC76uXTXhYveucTlmt4XZMw3rrX4GfzTatruns2n9jwXRW3hkRb3MmouXFxZOkM%2Brz%2B70m67JnDRPOs823aDlkYQ5eicvmd1cHzm4HlrA4a%2FODb%2FPQuFn%2B3v%2Fxg31d3l9E5PqfT%2F2GXoqmNFuVGGRsKc6dz7IoFA1IfL2fBRm7ndNxfsW9kLxoS7OE%2F8uGPOSJaIx5LM6dT4IwlJpoGExjcTgWd2Si%2FfyOJVkgED8rTkSB7%2Be3Pk%2F4IvZZPnxDHG2GdUfDRTGsnknCfFwTLoa%2BP2Dy34KXJ%2FrpekqdiQtMc75c91OeF9%2Bmxee6o1FjL4evT%2Bc0bvxJGMSsPyumRX5rhHDPxI2dmQNx%2FiKg04RGVHy9jLPApz7rf2YhHQc8ppEAiosz7y4uP78v7y3kvLl9dUiiedR6mGt8JjQKwtVmmGfzjKc9c5hfTeO0n7IkmByCgEa51ONROq%2Fe%2F8CwNlIqm9eiFHJny71JV8zbD4xHLEtW4pLZHrWsgkf3Oxrisq3ohRjF8aqqRGihBKbbnnc8EV8KqjTT5o%2Br%2BPbavfvT%2BeKJyUQ%2BhdfLpG%2BSTcfMr2mPOpH4IhmzBzqrEy7v9rY45Ek241MxDcLLXatEjd01HzmfFxz9wbJsVShUuhAzqMJgFvtnuXrc8VK0XAU5DOsux4vkbt0%2F2soro8mUZQ88iNtA0SapJmJmZ8FdFTn1MnLeZFR%2FEOekZNRq%2BWlabPZQqq0ntSf8IpBNjtI5dl3nIKOqc2xU1Tm2CaV0rE7A%2BkDzxQYGK9fsCiu7E6w%2BMV8YLsX6DAMZMj0JMwsKM9wJZl%2BZOBHENAngpplESUSgICOdQHaTCNtpAYqYREziQSHmtEFM9CP8O3bA0XgIu9zKLFdluwnLwP%2BeQS4HWzMVnK4uLJI15IY3V2CgOVXQLAcKNNTK4lCIWiwGDjvjsAwe2IyzitCNGovarMPehUktgPg7%2F%2F1g7Y%2Bvj7%2Ftn7xYFr1vjlbbI%2FW2%2BAH5d2R6mx0zgY18lrAxh2WD5VbZgMFiAJalkg2WXjbsU8EYYB1k0OuItnKuVK4LvaHZOzeAjREskcEGIwNWSQZbKxmQ9nVBLxVa%2Bc4KqTCigUAQlgk2kZjgYij4WrnRCuEL%2BTShvuAU9MoqKxM4CFu51TsI0xmd540ChFHILrftkSBakINnKbFf%2BhENQrAJKqFrgnng6IkueDfoZixkk1yBQs1eW%2FKSDLCl0Fa5FGKtS6ExsJ%2B2GIqjG5YEEVuL%2BZWukJbKzJJF9Ej4YaG0lUONxzrlUqrMohaEjkpAjbp4HhSsJIuPdMTCRxTa4SIGlgY%2Fi6HkyM55EGfrJ8fnPXzRpAufWtiA8IHChncC6SF6%2F9wsfKP0ip%2F0jYFBXK%2BiW8vsS5OAi95vchT2LuGTSSpmmjwDtoN4BlndN7JW8oenQtZq4dYRZHVfIVmvocmKbOxUyHpSXG1l%2BJcGaTLj0WiR5mLaMzmK1j0r5PnG6Zyn6SI4yjQlDaapWTVNiVxBABey9NrgC5t9mwLWF3iSkW%2B6UEjaDVoKPo8EiZ0jJS4tsFlod52DG%2FMEFDpkSAzGYPlL21NozZS12acQZ93Px3UYarV0mkAl%2Fp0RwacZvabpGJgNUhWuBZZ1sLvO2iS0N7R6Zw4F08KyLQCnSYDD%2FD5NZxIbK4YA9cFifZ4cqQaL9dkq017lk2mL9SHHqapkhMxTifjpVdQqy%2F1LI1ybmLHn7Ys5j%2BCYzpucczmrDOzamks6BgjbVTp79uMm1i8hZpUhQbth0dRJZzQwMHkTc17PbqgUs96aFGPgVhdnIWbXfhNzLmakUMyoOQPUodK2zF5FaZ%2BQmLXWq2JTpZg15XG2YrYI2RdzboPhoxbnihxVZnW1yVlpWa3uxdmVbTDDdN%2FEnO8DUmlq4xMqGH1%2B9XRL8RGtLAWOHrXJJM3Bt8UhQ0oowe2Lw8Blo20AvYPfmunU3tAAtj1OZWgO67UXJAXj6MiU2FrVzRMrgiHYEQFs9pYqAZBcBWyDpU6ISucYN5fivMDXY5Ca5LVO%2B673%2BOYJwiGP00WYUYj11anWI2HXHuDKhHfAqg7K946pmfCaYvivfsIDFyjVHvY2o9ki%2FT4J7q5YeAcx5V3JAJJ2aztgJUpE5T4EoimZ8RoLXwtFdHThK2n2doELX9cm0kZQCDdRaVts3pI4jxWqkrIa9CRKU4lKd%2BI02fTylw%2FPei61mrdbveyacvgNIF5ZyVZuAHlAwN0zt1WRWPdF5RmLjjIyWlSUyy%2FAwg7UVl0C7JjXUFvXQXcQqHIlTxzMTHNU1hYRvelLPYFwrHPJIcAvNKsRgKVzNg7EdXkFJQgTiBwEl2O2YK%2FTc1T66E6DGPQbWS3n9Gm5LC55pl1VCvYUXZZrZS6LjRy3ageZJ2QHOSoT6y%2BaXPi0yOU8l1zN3uRrIpcxML3SuVs9Ko7uqdVqR1v3LgbNBD%2BO22bRxsuQ7AITzi5QGcrEul%2Bpguq1XzD1909Rh9rqgJTG1XSX9RFTcoGAarFfgmRdlaR1NGWYd1X2%2B3LV8VJArfUXTteJ6HWYB6LiQvrHGGS61QQ0xlCLmKvU%2Fta%2Biayi5345PnSdp%2FZ5SqcsAqEElinhVClhgf1Lh6ty60YZof2lYp9ad964xapwtOfqNkcRXna6DfYVTsJ98PAp%2Bb6uypitZg4bWjisdSUrX913PIe1hHZfNIdzj98qgT8NErd6nZWGHDmPjnvVSovwFTLkf9Y6ws4Rh7t%2FcN1IY%2Fc%2FuNbl%2Fw%3D%3D%3C%2Fdiagram%3E%3C%2Fmxfile%3E)
 
---

## 🧱 Modelagem Lógica

### **Tabelas Derivadas do Modelo Conceitual**

- **TUTOR**
  - id_tutor (PK), CPF_tutor, nome_tutor, logradouro, bairro, número
- **EMAIL_TUTOR**
  - id_email (PK), id_tutor (FK), email
- **TELEFONE_TUTOR**
  - id_tel (PK), id_tutor (FK), telefone
- **GATO**
  - id_gato (PK), nome_gato, raca_gato, cor_gato, dataNasc_gato, id_tutor (FK)
- **PRONTUARIO**
  - id_prontuario (PK), dataConsulta, status_fivfelv, id_gato (FK UNIQUE)
- **VETERINARIO**
  - id_veterinario (PK), nome, especialidade
- **MEDICAMENTO**
  - id_medicamento (PK), nome, dosagem
- **GATO_VETERINARIO**
  - id_gato (FK), id_veterinario (FK), PK composto
- **GATO_MEDICAMENTO**
  - id_gato (FK), id_medicamento (FK), PK composto

Vizualize o MER feito do Draw.io [Modelo de Entidade Relacional]( https://viewer.diagrams.net/?tags=%7B%7D&lightbox=1&highlight=0000ff&edit=_blank&layers=1&nav=1&title=Mer-final.drawio&dark=auto#R%3Cmxfile%3E%3Cdiagram%20name%3D%22P%C3%A1gina-1%22%20id%3D%22zXirNb4ilJaz9RcqFgmG%22%3E7Z1dc6O4EoZ%2FjavmXGTKgPHHZezJzGY3k0wl2T0z52ZKYxSbWgw%2BWE7i%2FfUrMPIHBrnjIIShq1IVI2MZqx9ar7ol0bJGs9cvIZlPvwYO9Vpm23ltWZ9apmn0uwP%2BLypZrUvsrrkumISuk5y0LXhw%2F6FJYTspXboOXeydyILAY%2B58v3Ac%2BD4ds70yEobBy%2F5pT4G3%2F61zMqEHBQ9j4h2W%2Ftd12HRd2jd72%2FLfqDuZim82xA%2BeEXFy8ksWU%2BIELztF1lXLGoVBwNavZq8j6kWNJ9pl%2FbnPOe9uLiykPoN8YHU1%2F617M%2FSuL%2F%2FidjKG%2F5%2By7xcZtSRFC7YSbcCvfB69ZORXVDRcMBKyxFRWmxfwxmfE9WnIC4z42PPIfOHGp69Lpq7n3JBVsGSiInE0fHJfqXO%2FtlR0LjfaDa8sOowqf%2BKVPyQXE71NPHfi89djfsXRNw5DuuDXckMWLDljymZe8nL9W56Jt0x%2By5fLx7ukkIaMvu785qTZvtBgRlm44qdMdyxrdhI7vmwxsKykLKnmwhgkBQntVj85JgmGk03lW0vxF4mx3mA489BwMgPnWfM%2BInI4DUL3n8iGXtLmuxaOj1%2FcmUd8jjpxUkXDIL61Y0u5njcKvCDCwA98ekBCdJITBvNHEk4oSwrmgeuzuHnsIf%2FjDTZqf7RbNr%2FWET82tsf8Lzo9ZKPAX7CQExfVQbnhX2hk%2FCEL5kmlHn0S9YeJDaPXvwLGglkeGydxYUmwWO2fUjgEFhACMxcC%2FlHmEu%2Beu07iT7y1yWJPSrYmy7BrZktvWjfd7OlbOOBt%2FOTFznDqOg7lt%2FPwZeoy%2BjAn4%2BikF96ZHLmRv%2F1RmLkk5kkq27bPm2sjHvdSPmH8Rln6zuLA5pvrPB2DzplgIDz3%2Btzhghvb9Sc36092U5zYBXHiOj8nhAVFwWLY%2By6%2FWHg2tZdIj4H4yPDhTaIIHUMmDs6DHRtVyHtUSLtMFdJVpUK6QAhszf6DOq6orygRghIksW3vTBg42ocUQYXPmxNFh1x0QHuORgDzTMLxlIQf7PZ%2FUGzkotBHsXE2YmOgSmwMgBD0UWzUVmyI3EDlISil8wjJmKDakAMDHaI0AhihNkxUGzJmMlJjKDcqKjcMU5XeMEwoBvkcoOI4e8UBzbRpp6CUHmQchKg45MBAA2LNAAYlBwgajHAUJTmKVxhpHopTGNCQhqF7dFKYwkBBIfRq9Y1eSv%2FgEEZuyWKMqkJODXhM2hRqKMqJfFpwdkZ15YS6icHQWKepO7WqIGDxGSeFbswLHYFq56CUvsJ1frIl4xeJ4iKPA%2BjosyHA4MRPGQPgQStqi7K1xWbtXPHrTaCjVoEHaotaagsLOg7VzkFZ2mIecve1JKGL0Yt8akykBgUGVGBkwHKoJXi7sf1mzrIC76uDv2mKiAxIDlYWR5Zxx8S7TN6YcVvHzIXR76ZCisTrjtZihY%2B60ssd03a3PvLjeKE8mdAZf33TGlmtoTXh31QUEJ0DIAZ7EkHdfAkrI1Ne7xXlj38%2B3t2fZLiNUJMsKTf7%2B%2BLO6CmzHHQdoDAxavr9XqQma8qhUWPBC64qr6nIhwaStYOga105BhTlawKhAcWGAoT6X8YENH2BaqQC86%2BVrS23wD6kp9mH4PRrhc4Amm3QTkF568tRfMjFByKDK8zfvJEWNL%2BFoqMCokPZGvMONL0leEHRUUPR0cnIQFSTglJ6kNG3z6g5jmxQAu0%2BmkGM0BxGBzWHhAXo0lLUHBXQHOoSpx1o%2Bq2TzwGKjrMXHdDsm3YKSulCvGASEidYhgFqjyPaAzxmaQQ4GO8AeRtwihe1R41WnHeguTXBx%2FlLDVQWHWgmTbvRS%2BkgfhE3RFVxVFWAY2CNgAa3sQF5GnDqDVVFjRaeC9KO%2BwrdyztQVRT3ABDwsFO30cuZmdEama1hG2XFEVkBjXk3gxqcCSp1MRkh0XqvKKIz4nrv8CGbJIVkXVE3%2FaTKtjJdAH4%2BUP6%2BEo2Wg%2FVYV2SDHxGkeyiJ64rU%2BnNoIEo7CLrWFb3X%2FzdDQ56NP8HVRZWDx4aGqFCTVGDSjbonV0JDVrbucSjOuVHnDLrQGJZ2CkqJRqD6gKgPsIhtBDM43QbkaExUHeejOpQtL%2BpCo9%2BClzqpDtxFcWte6Ixv7RzgDs2V6D%2F60FFrQ4DBEIeMgQyFWu%2B0GaMcN05ryZkzdTvydcH3e%2F7jXhqtF%2BuRORN8HcdA91gTM2dq9zSBBqq0g6BtR773dwHNUJLgoUczSUJlKXND0DAWypIKhLGUJc960DCW4KVOYSzUJMK40J5EOwWlxCRQgAAFCHSfg2Zgs9kqx8b8mYQFKDQoPCogPJTlz3rQCeU93Q8qxPyZUncAnQGqnQPMn1Wi%2F%2BifjePA%2FJl2WET31Zz82ZfLx7uLv64er%2B6vby%2Fvr%2B9OggOSQUs%2F06qTNm9hUmEAjZgLa6NirGMGbQCNWA7y73DMoNVAMg6gMUvtIGjJe3zgGnJCWBB5lKglfz5TbhLXj55rqywwcf660mgjVig0T%2FZJ0Ag6apQKRLWUpdMG0ODmQPfT8jCqpdQdQIMU2jkoK6q1ViQoPvLEB7j%2FaAYwKDZkDEBj5ig2KiA2lKXQBtDlqwPdT8dDsaHUHUBXGGjnoCyxsRPxQM2RrznAg5VmcIOaQ0pLxpCm3qm0MrJovfa%2BWFCXRTPaUNW4MTXKxjrm0Yw2VDdukMFMWj2Vo9GGSkf9KOhajYZaEgKSgSChuHwHPhnztFCbVDakpSx%2FZhjQuV4bZOoU1EJhsrGueTYclPNMEt6kKEVA6JjgvqQZ6OC2jjCPA53%2BhRKkChJEWVbNMKCp%2BA0yKEFqKUGg6RH9HJSzpfRiTsf8t7gOcVCLALUIfDjTCIbw2aspbH4897uLh7uX3%2Fvu%2F67vfr91f7g3FxnQ1DvT9u3%2B7vbxT7XL1VIbPtpFCIhM62WMXGVWRhV55km2TONmDCZksGCC7exFZKZ5M4YSlcRAV3JtHvJ6lygipWoAIcLE2onsZAxhUYtUNKJVRFIt07gZE%2FdksGA0q4ZCJGPuXyUZKCUK4RBGIuew9BhBCQKRINB%2BpCn4UNQcuQxkzC5FzVFRzaEsCJYxHVAGC2qOGmqOrEl9lYSglF6DOy62XPx8cp%2BfqPeMsgMCEHTk0giAosQZyo58WDKGOPXOmsVbPX69%2BnQ9uvx6dfuoLndmpRap9ZSlTQyweMxfRdBo9ViP7FnWahIpL5g%2Fq6eEzJrLW00QqrHV45yPZxzc5VECVMbcGgQKs2kweExUJ%2BcT21KWTzPBk3tMzT4E911S6g7AEzN0c4CbPFai%2B4Bm0RrCC2oNGQPQ2CdqjQpoDXWTyaETN8z8RYmoNWqgNaCBUe0clKU1Zhy4MZnx1kDJkU8DNJDaEGxQckgYEJfRnAxaGcmznrEvFdQlzyxobFNcAUrGOibPLGiU0sq%2FuTF5VgPNaEHjlNpB0LX8DDUkBCNomLOhGKGmlDEBjXmiJqlAGEtZysyCRjMt3StIcEK4QmcADWZqp6C8PR2FBAlRg8iAgIY%2Fm0EObqMEggYa%2FETtUQHtoSyF1oHOIRW8oPaoofbogIOjuikoZw1zsCATOsMICIgdcES1GezQsTsj3gcutUYmChAJN0nkjDoTutM02Rm2YBmOk7Mydwi1Dh%2F8G9Urwlm8Ppet7qlHmBv4V9t31kGvtUoxzH3TUt%2B5DMOYhqt7zttj8JX4q4ipqE2oUDHrL2ZCj%2BRdYc%2FO7H6OpNDE2rIwvvTn%2FYbaNWD7OA%2FfgjgaJxCyO%2FsS48AVrRs9%2BdTW%2FgcVdVMVGemK1m1zUFFhINn1AInXHa6%2B7x78iA4%2B2uLw0%2Bvum59WbwOwK%2BQOAlg0gIMCATQPe8liAZwR37mLe894iJb1hiouZRvzVRbLbq8gLO10RYqxtM0Cscx6MlnFeljxIN7KkHRh9vcJ6J%2BK0oWRqqlXNktWkS5OXxf76rLv4iP89Y4j40dbPxYdvNWNVc6PpUJIRts41ZGlg1HpihTD1zVqBV%2F744C7ql0AeR8jRTA6%2BEZDd0bjaXxvcoqdimFppmb82eJB62%2F3ialN6ztlY1mkT9Q57hBcvsspZt9sVRv09lId8qlDDiNV0cG8VdXsnRg8gU5NKn%2FMy51iZ3980T8yvoiPjrtF6Yz%2ByoBpp9ziIJ3xAXfWqYr66YpOJpMfhkHAdk8PyZzf7A6NzvgX%3C%2Fdiagram%3E%3C%2Fmxfile%3E)

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

# 🐱 Clínica Veterinária Gatices – Sistema de Gestão Exclusivo para Gatos

## 📌 Cenário

### **Sistema de Clínica Veterinária Exclusiva para Gatos**

A clínica **Gatices**, certificada com o selo *Cat Friendly*, oferece um ambiente totalmente voltado ao bem-estar dos felinos — sem latidos, cheiros de cães ou estímulos que gerem estresse.  
Apesar do atendimento de excelência, o controle de informações ainda é feito em papel, trazendo diversos riscos.

### **Problemas Identificados**

- **Dificuldade de Identificação:**  
  Muitos gatos têm o mesmo nome e mesma cor, gerando confusões perigosas.
- **Controle de Vacinas Vulnerável:**  
  As vacinas V3, V4, V5 e testes FIV/FELV exigem rigor nos prazos, mas com anotações manuais os reforços podem ser esquecidos.
- **Contato Emergencial Insuficiente:**  
  O cadastro atual permite apenas um telefone, mas quando o tutor viaja o gato fica sem novo contato registrado.

### **Necessidade da Clínica**

O novo sistema deve:
- Garantir identificação precisa dos gatos.
- Permitir múltiplos telefones e e-mails do tutor.
- Centralizar todo o histórico médico.
- Registrar consultas e medicamentos com datas confiáveis.
- Reduzir retrabalho e estresse dos animais.

---

## 🧩 Modelagem Conceitual

### **Entidades e Atributos**

#### **TUTOR**
- id_tutor (PK)
- CPF_tutor (único)
- nome_tutor
- emails (multivalorado)
- telefones (multivalorado)
- logradouro_tutor
- bairro_tutor
- numero_tutor

#### **GATO**
- id_gato (PK)
- nome_gato
- raca_gato
- cor_gato
- dataNasc_gato
- idade (derivada)

#### **VETERINARIO**
- id_veterinario (PK)
- nome_veterinario
- especialidade_veterinario

#### **MEDICAMENTO**
- id_medicamento (PK)
- nome_medicamento
- dosagem_medicamento

#### **PRONTUARIO**
- id_prontuario (PK)
- dataConsulta_prontuario
- status_fivfelv_prontuario

### **Relacionamentos**

| Relacionamento | Tipo | Descrição |
|----------------|------|-----------|
| Tutor → Gato | 1:N | Um tutor possui vários gatos |
| Gato → Prontuário | 1:1 | Cada gato possui um único prontuário |
| Gato ↔ Veterinário | N:N | Vários veterinários podem atender o mesmo gato e um gato pode passar por vários veterinários |
| Gato ↔ Medicamento | N:N | Um gato pode receber vários medicamentos e um medicamento pode ser usado por vários gatos |

Vizualize o projeto feito no Draw.io: https://viewer.diagrams.net/?tags=%7B%7D&lightbox=1&highlight=0000ff&edit=_blank&layers=1&nav=1&title=DERfinal.drawio&dark=auto#R%3Cmxfile%3E%3Cdiagram%20name%3D%22P%C3%A1gina-1%22%20id%3D%22vLd22eKHMPMLas6_fcbh%22%3E7V1dc5s4FP01nmkf7EGABDwmTtLd2TaTabrd7b50ZCPbdAF5ASd2f%2F0KG2wjcEIcXeSkebIRWIhzda7ul3DPGkbLDwmdzz5xn4U90%2FCXPeuiZ5rIsE3xkbesNi2YFA3TJPCLi3YNt8FPVv6yaF0EPksrF2ach1kwrzaOeRyzcVZpo0nC76uXTXhYveucTlmt4XZMw3rrX4GfzTatruns2n9jwXRW3hkRb3MmouXFxZOkM%2Brz%2B70m67JnDRPOs823aDlkYQ5eicvmd1cHzm4HlrA4a%2FODb%2FPQuFn%2B3v%2Fxg31d3l9E5PqfT%2F2GXoqmNFuVGGRsKc6dz7IoFA1IfL2fBRm7ndNxfsW9kLxoS7OE%2F8uGPOSJaIx5LM6dT4IwlJpoGExjcTgWd2Si%2FfyOJVkgED8rTkSB7%2Be3Pk%2F4IvZZPnxDHG2GdUfDRTGsnknCfFwTLoa%2BP2Dy34KXJ%2FrpekqdiQtMc75c91OeF9%2Bmxee6o1FjL4evT%2Bc0bvxJGMSsPyumRX5rhHDPxI2dmQNx%2FiKg04RGVHy9jLPApz7rf2YhHQc8ppEAiosz7y4uP78v7y3kvLl9dUiiedR6mGt8JjQKwtVmmGfzjKc9c5hfTeO0n7IkmByCgEa51ONROq%2Fe%2F8CwNlIqm9eiFHJny71JV8zbD4xHLEtW4pLZHrWsgkf3Oxrisq3ohRjF8aqqRGihBKbbnnc8EV8KqjTT5o%2Br%2BPbavfvT%2BeKJyUQ%2BhdfLpG%2BSTcfMr2mPOpH4IhmzBzqrEy7v9rY45Ek241MxDcLLXatEjd01HzmfFxz9wbJsVShUuhAzqMJgFvtnuXrc8VK0XAU5DOsux4vkbt0%2F2soro8mUZQ88iNtA0SapJmJmZ8FdFTn1MnLeZFR%2FEOekZNRq%2BWlabPZQqq0ntSf8IpBNjtI5dl3nIKOqc2xU1Tm2CaV0rE7A%2BkDzxQYGK9fsCiu7E6w%2BMV8YLsX6DAMZMj0JMwsKM9wJZl%2BZOBHENAngpplESUSgICOdQHaTCNtpAYqYREziQSHmtEFM9CP8O3bA0XgIu9zKLFdluwnLwP%2BeQS4HWzMVnK4uLJI15IY3V2CgOVXQLAcKNNTK4lCIWiwGDjvjsAwe2IyzitCNGovarMPehUktgPg7%2F%2F1g7Y%2Bvj7%2Ftn7xYFr1vjlbbI%2FW2%2BAH5d2R6mx0zgY18lrAxh2WD5VbZgMFiAJalkg2WXjbsU8EYYB1k0OuItnKuVK4LvaHZOzeAjREskcEGIwNWSQZbKxmQ9nVBLxVa%2Bc4KqTCigUAQlgk2kZjgYij4WrnRCuEL%2BTShvuAU9MoqKxM4CFu51TsI0xmd540ChFHILrftkSBakINnKbFf%2BhENQrAJKqFrgnng6IkueDfoZixkk1yBQs1eW%2FKSDLCl0Fa5FGKtS6ExsJ%2B2GIqjG5YEEVuL%2BZWukJbKzJJF9Ej4YaG0lUONxzrlUqrMohaEjkpAjbp4HhSsJIuPdMTCRxTa4SIGlgY%2Fi6HkyM55EGfrJ8fnPXzRpAufWtiA8IHChncC6SF6%2F9wsfKP0ip%2F0jYFBXK%2BiW8vsS5OAi95vchT2LuGTSSpmmjwDtoN4BlndN7JW8oenQtZq4dYRZHVfIVmvocmKbOxUyHpSXG1l%2BJcGaTLj0WiR5mLaMzmK1j0r5PnG6Zyn6SI4yjQlDaapWTVNiVxBABey9NrgC5t9mwLWF3iSkW%2B6UEjaDVoKPo8EiZ0jJS4tsFlod52DG%2FMEFDpkSAzGYPlL21NozZS12acQZ93Px3UYarV0mkAl%2Fp0RwacZvabpGJgNUhWuBZZ1sLvO2iS0N7R6Zw4F08KyLQCnSYDD%2FD5NZxIbK4YA9cFifZ4cqQaL9dkq017lk2mL9SHHqapkhMxTifjpVdQqy%2F1LI1ybmLHn7Ys5j%2BCYzpucczmrDOzamks6BgjbVTp79uMm1i8hZpUhQbth0dRJZzQwMHkTc17PbqgUs96aFGPgVhdnIWbXfhNzLmakUMyoOQPUodK2zF5FaZ%2BQmLXWq2JTpZg15XG2YrYI2RdzboPhoxbnihxVZnW1yVlpWa3uxdmVbTDDdN%2FEnO8DUmlq4xMqGH1%2B9XRL8RGtLAWOHrXJJM3Bt8UhQ0oowe2Lw8Blo20AvYPfmunU3tAAtj1OZWgO67UXJAXj6MiU2FrVzRMrgiHYEQFs9pYqAZBcBWyDpU6ISucYN5fivMDXY5Ca5LVO%2B673%2BOYJwiGP00WYUYj11anWI2HXHuDKhHfAqg7K946pmfCaYvivfsIDFyjVHvY2o9ki%2FT4J7q5YeAcx5V3JAJJ2aztgJUpE5T4EoimZ8RoLXwtFdHThK2n2doELX9cm0kZQCDdRaVts3pI4jxWqkrIa9CRKU4lKd%2BI02fTylw%2FPei61mrdbveyacvgNIF5ZyVZuAHlAwN0zt1WRWPdF5RmLjjIyWlSUyy%2FAwg7UVl0C7JjXUFvXQXcQqHIlTxzMTHNU1hYRvelLPYFwrHPJIcAvNKsRgKVzNg7EdXkFJQgTiBwEl2O2YK%2FTc1T66E6DGPQbWS3n9Gm5LC55pl1VCvYUXZZrZS6LjRy3ageZJ2QHOSoT6y%2BaXPi0yOU8l1zN3uRrIpcxML3SuVs9Ko7uqdVqR1v3LgbNBD%2BO22bRxsuQ7AITzi5QGcrEul%2Bpguq1XzD1909Rh9rqgJTG1XSX9RFTcoGAarFfgmRdlaR1NGWYd1X2%2B3LV8VJArfUXTteJ6HWYB6LiQvrHGGS61QQ0xlCLmKvU%2Fta%2Biayi5345PnSdp%2FZ5SqcsAqEElinhVClhgf1Lh6ty60YZof2lYp9ad964xapwtOfqNkcRXna6DfYVTsJ98PAp%2Bb6uypitZg4bWjisdSUrX913PIe1hHZfNIdzj98qgT8NErd6nZWGHDmPjnvVSovwFTLkf9Y6ws4Rh7t%2FcN1IY%2Fc%2FuNbl%2Fw%3D%3D%3C%2Fdiagram%3E%3C%2Fmxfile%3E
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

---

## 🛠 Modelagem Física

A Modelagem Física consiste na transformação das tabelas acima em comandos SQL de criação, relacionamento e restrições (PK, FK, UNIQUE).  
Inclui:

- Criação do banco de dados  
- Criação das tabelas  
- Definição de relacionamentos  
- Definição de atributos multivalorados através de tabelas auxiliares  
- Aplicação de chaves primárias, estrangeiras e restrições  

---

## 📊 Dados

Exemplos de dados previstos no sistema:

- Cadastro do tutor com múltiplos e-mails e telefones  
- Registro do gato vinculado ao tutor  
- Prontuário exclusivo do gato  
- Associação do gato aos veterinários que o atenderam  
- Lista de medicamentos utilizados pelo gato ao longo da vida  

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

---

## 📈 Relatórios

O sistema deve fornecer relatórios como:

- Lista de gatos e seus respectivos tutores  
- Histórico de consultas por gato  
- Status FIV/FELV e vacinas pendentes  
- Lista de veterinários que atenderam cada gato  
- Medicamentos já aplicados ao longo da vida  
- Agenda de consultas (ordenada por data)  



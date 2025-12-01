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



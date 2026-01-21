---

title: Ferramentas
excerpt: "Entenda conceitos fundamentais de bancos de dados relacionais."
categories:
  - "introducao-a-banco-de-dados"
  - "capitulo-1"
date: 2024-03-01T08:48:05-04:00
order: 12
tags:
  - banco-de-dados
sidebar:
  nav: introducao-a-banco-de-dados
---

# FERRAMENTAS

**BANCO DE DADOS I**
Marco Yerco Mendizabel Cabrera
Analista de Sistemas

## Objetivos

- Produtos de banco de dados
- A estrutura do Oracle Server (SGBD)
- As ferramentas

---

## PRODUTOS

(Imagem/lista de produtos de banco de dados)

---

## ORACLE

An Oracle database is a collection of data treated as a unit. The purpose of a database is to store and retrieve related information. A database server is the key to solving the problems of information management. In general, a server reliably manages a large amount of data in a multiuser environment so that many users can concurrently access the same data. All this is accomplished while delivering high performance. A database server also prevents unauthorized access and provides efficient solutions for failure recovery.

The database has **logical structures** and **physical structures**. Because the physical and logical structures are separate, the physical storage of data can be managed without affecting the access to logical storage structures.

---

## CLIENTE-SERVIDOR

A tecnologia cliente/servidor é uma arquitetura na qual o processamento da informação é dividido em módulos ou processos distintos. Um processo é responsável pela manutenção da informação (servidores) e outros responsáveis pela obtenção dos dados (os clientes).

---

## ESTRUTURA DO SERVIDOR

(Imagem/diagrama da estrutura do servidor Oracle)

---

## ORACLE SERVER

**Oracle Database Express Edition 11G**

1. Faça download do Oracle Database Express Edition 11g Release 2 for Windows x64*
2. Descompacte o arquivo .zip e execute DISK1/setup.exe
3. Recomendações de instalação:
   - Diretório sugerido: `C:\ORACLEXE`
   - Senha do usuário SYSTEM: `12345678`

---

## PROCESSOS

(Imagem/diagrama dos processos Oracle)

---

## ORACLE DEVELOPER

**Oracle SQL Developer**

1. Faça download escolhendo a opção Windows 64-bit - zip file includes the JDK 7
2. Descompacte o arquivo .zip e copie o conteúdo para uma pasta de trabalho
3. Recomendações de instalação:
   - Diretório sugerido: `C:\SQL\SQLDeveloper4`

---

## AMBIENTE


┌─────────────────────────────────────┐
│ Conexões e Objetos de banco de dados│
│ • Tabelas │
│ • Views │
│ • Procedure │
├─────────────────────────────────────┤
│ Área de trabalho │
│ • Comandos SQL │
│ • Scripts │
│ • Avaliação │
└─────────────────────────────────────┘

---

## NOVA CONEXÃO

- **Nome da Conexão**: Aula
- **Nome do usuário**: system
- **Senha**: 12345678
- **Nome do Host**: Localhost
- **Porta**: 1521
- **SID**: xe
- **Conectar**

---

## ÁREA DE TRABALHO


┌─────────────────────────────────────┐
│ Comandos SQL │
├─────────────────────────────────────┤
│ Resultado do comando │
└─────────────────────────────────────┘

---

## Próximo tópico

- Abstração de dados

### O que foi visto

- Produtos de banco de dados
- A estrutura do Oracle Server (SGBD)
- As ferramentas

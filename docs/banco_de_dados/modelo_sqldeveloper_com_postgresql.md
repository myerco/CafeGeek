---
title: SQLDeveloper com PostgreSQL
description: SQLDeveloper com PostgreSQL
tags: [Banco de Dados, Oracle, Oracle SQLDeveloper, MER, modelo relacional,PostgreSQL]
---

# SQLDeveloper com PostgreSQL

## 1. Características
- Ferramenta gráfica desenvolvida pela ORACLE;
- Permite a implementação de estruturas de banco de dados executando comandos SQL;
- Construção de modelos lógicos e físicos;

## 2. Instalação
1. Instalando no linux Ubuntu
    - Instalando Java 8;
    - Baixando o  SQLDeveloper Oracle;
    - Descompactando o SQLDeveloper.
      - Descompacte o programa no diretório /opt para padronizar as instalação
      ```bash
      sudo unzip ~/Downloads/sqldeveloper-*-no-jre.zip -d /opt/
      sudo chmod +x /opt/sqldeveloper/sqldeveloper.sh
      sudo ln -s /opt/sqldeveloper/sqldeveloper.sh /usr/local/bin/sqldeveloper
    ```  
    - Alterando o arquivo sqldeveloper.sh
    ```bash
    #!/bin/bash
    unset -v GNOME_DESKTOP_SESSION_ID<
    cd /opt/sqldeveloper/sqldeveloper/bin && bash sqldeveloper $*
    ```
    - Testando.
    ```bash
    sqldeveloper.sh
    ```
    - ADICIONANDO AO DESKTOP

    Arquivo : `/usr/share/applications/sqldeveloper.desktop`
    ```bash
    [Desktop Entry]
    Exec=sqldeveloper
    Terminal=false
    StartupNotify=true
    Categories=GNOME;Oracle;Utility;Development;
    Type=Application
    Icon=/opt/sqldeveloper/icon.png
    Name=Oracle SQL Developer
    Comment=SQLDeveloper Oracle
    Version=?
    GenericName=ORACLE SQL DEVELOPER
    ```

1. Instalando no Windows
    - Baixe o aplicativo de preferência com JDK incluído
    - Descompacte em uma pasta de trabalho, por exemplo: `c:\desenvolvimento\SQLDeveloper`
    - Baixe o driver JDBC para [PostgreSQL](https://jdbc.postgresql.org/download.html);
    - Execute o `SQLDeveloper.exe`;
    - Adicione o driver do PostgreSQL : Menu->Ferramentas->Banco de Dados->Drivers JDBC de Terceiros;

## 3. Data Modeler
- Menu > Exibir > Data Modeler > Browser
- Na janela Browser clique no Modelo Lógico com botão direito e escolha Mostrar para que barra de menu apresente as opções de construção de modelos;

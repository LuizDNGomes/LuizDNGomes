# Programa de Cálculo de Recalques

# Soil Deformation Program

## Descrição
O **Soil Deformation Program** é uma aplicação desenvolvida em Python para calcular recalques (deformações) em solos devido a cargas aplicadas, como fundações de estruturas (cilíndricas ou prismáticas). O programa processa dados de entrada sobre o solo, cargas e pontos de análise, fornecendo resultados detalhados sobre os recalques totais, de ponta e de atrito.

Esta é uma versão em Python baseada em um programa original em BASIC, desenvolvido por N. Aoki e P. C. Aoki, com contribuições de George Drozczak e Luiz Henrique Olavo. A versão atual foi desenvolvida por LuizDNGomes.

## Funcionalidades
- **Leitura de Dados**: Lê arquivos de entrada (`.DAT`) contendo informações sobre a obra, propriedades do solo, superfícies carregadas e coordenadas de pontos para análise.
- **Cálculos de Recalque**: Utiliza o método de Mindlin e Steinbrenner para calcular deformações no solo, considerando diferentes tipos de fundações (cilíndricas ou prismáticas).
- **Saída de Resultados**: Gera um arquivo `RESULTS.DAT` com os resultados dos recalques e permite visualizá-los no Bloco de Notas ou na tela.
- **Interface de Usuário**: Interface de linha de comando com menus interativos e notificações do sistema (usando `win10toast` no Windows).

## Requisitos
- **Sistema Operacional**: Windows
- **Bibliotecas Utilizadas**:
  - `tkinter`
  - `win10toast`
  - `datetime`, `math`, `os`, `sys`, `time`, `threading`
    
- **Arquivos de Entrada**:
  - `OBRA.DAT`: Informações gerais da obra.
  - `SOLO.DAT`: Dados das camadas do solo.
  - `Carga.dat`: Informações sobre as superfícies carregadas.
  - `Pontos.dat`: Coordenadas dos pontos de cálculo.

## Créditos
- **Desenvolvedor Python**: LuizDNGomes (luizdngomes@live.com)
- **Apoio**: George Drozczak (george@drkengenharia.com.br), Luiz Henrique Olavo (luiz@ensolo.com.br)
- **Versão Original em BASIC**: N. Aoki e P. C. Aoki

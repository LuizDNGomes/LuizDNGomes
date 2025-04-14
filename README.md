# Programa de Cálculo de Recalques

Este programa calcula os recalques (afundamentos) no solo causados por cargas de fundações (estacas cilíndricas ou prismáticas), com base nos métodos de Aoki & Lopes e Mindlin, utilizando a teoria da elasticidade.

## Explicação para o Usuário Final

### O que o programa faz?
Calcula os recalques esperados em pontos específicos do solo devido às cargas aplicadas por um grupo de estacas. Os resultados são apresentados em um arquivo `RESULTS.DAT` e podem ser exibidos na tela ou em um relatório detalhado (`printout.txt`).

### Como usar
#### 1. Preparar os Arquivos de Entrada
Você precisa de quatro arquivos de texto (.DAT) na mesma pasta do programa:
- **OBRA.DAT**: Informações do projeto (Cliente, Obra, Título, Data).
  - Formato: 4 linhas (strings, com a data no formato `"DD","MM","YYYY"` ou `DD MM YYYY`).
- **SOLO.DAT**: Propriedades das camadas do solo.
  - Formato: Número de perfis (NPERFIS), número máximo de camadas (NMCP), seguido por NCAM_i (número de camadas do perfil i) e, para cada camada, profundidade (PROF), módulo edométrico (EC), coeficiente de Poisson (MC).
- **Carga.dat**: Dados das estacas e cargas.
  - Formato: Número de estacas (NE), número máximo de diagramas (NMT), seguido por tipo ('C' para cilíndrica, 'P' para prismática), coordenadas (XA, YA), dimensões, carga de ponta (PB), subdivisões (N1P, N2P, N1L, N3L, N2L para prismas), ângulo (prismas) e diagramas de carga lateral (D1, D2, F1, F2).
- **Pontos.dat**: Pontos onde o recalque será calculado.
  - Formato: Número de pontos (NP), seguido por coordenadas (XB, YB, ZB) e perfil de solo (PDP) para cada ponto.

**Nota**: Consulte os arquivos de exemplo para garantir o formato correto. O arquivo `Carga.dat` varia entre estacas cilíndricas e prismáticas.

#### 2. Executar o Programa
- **Pré-requisitos**: Python 3.x instalado.
- Salve o script Python (ex: `aoki_recalque.py`) e os arquivos .DAT na mesma pasta.
- Abra um terminal e navegue até a pasta com `cd caminho/para/pasta`.
- Execute o programa: `python aoki_recalque.py`.
- Uma janela será aberta para selecionar a pasta dos arquivos .DAT. Escolha a pasta correta e clique em "Selecionar pasta".
- O programa lerá os dados, exibirá informações (pressione Enter para continuar) e calculará os recalques. Isso pode levar tempo, dependendo do número de estacas e pontos.
- Após o cálculo, um menu de saída será exibido.

#### 3. Ver os Resultados
- **Menu de Saída**:
  - **Opção 1 (Impressora/Arquivo)**: Gera um relatório detalhado em `printout.txt`.
  - **Opção 2 (Tela)**: Exibe dados de entrada e resultados no terminal (pressione Enter para avançar).
  - **Opção 3 (Sair)**: Encerra o programa.
- **Arquivo RESULTS.DAT**: Contém os resultados principais:
  - Coluna 1: Número do ponto.
  - Coluna 2: Recalque devido à carga de ponta (WP, em metros).
  - Coluna 3: Recalque devido ao atrito lateral (WL, em metros).
  - Coluna 4: Recalque total (WT = WP + WL, em metros).

#### 4. Solução de Problemas
Se houver erros, verifique:
- Existência e nomes corretos dos arquivos .DAT.
- Formato correto dos dados nos arquivos (números válidos, ordem correta).
- Instalação correta do Python.

## Documentação Técnica para Desenvolvedores

### Visão Geral
- **Base**: Conversão do programa `SOILDEF.BAS` (Aoki & Lopes, 1975/1991).
- **Linguagem**: Python 3.x.
- **Dependências**: `os`, `sys`, `math`, `tkinter` (para seleção de pasta), `datetime`. Não requer bibliotecas externas como NumPy.

### Fluxo de Execução
1. **verificar_arquivos()**: Solicita a pasta dos arquivos .DAT via Tkinter e verifica a existência de `OBRA.DAT`, `SOLO.DAT`, `Carga.dat`, `Pontos.dat`.
2. **apresentacao()**: Exibe a tela inicial.
3. **job_information()**: Lê dados gerais de `OBRA.DAT`.
4. **soil_section(), layers_input()**: Lê propriedades do solo de `SOLO.DAT`.
5. **loaded_surfaces(), loaded_surfaces_input()**: Lê dados das estacas de `Carga.dat`.
6. **point_coordinates()**: Lê pontos de cálculo de `Pontos.dat`.
7. **processing()**: Realiza os cálculos:
   - Itera sobre pontos (ip) e estacas (ine).
   - Chama `calc_cilindro` ou `calc_prisma` conforme o tipo de estaca.
   - Salva resultados em `RESULTS.DAT`.
8. **output_menu()**: Apresenta opções de saída ([1] Arquivo, [2] Tela, [3] Sair).

### Funções de Cálculo
- **calc_cilindro(ip, ine) / calc_prisma(ip, ine)**: Calculam recalques WP e WL, subdividindo estacas em elementos menores e chamando `steinbrenner()` para cada um.
- **steinbrenner(ip, c_load, p_load, rij)**: Integra a solução de Mindlin por camadas de solo.
- **mindlin(p, z, c, e, m, rij)**: Calcula deslocamento vertical com base na teoria de Mindlin, com verificações numéricas.

### Status Atual
- Resultados estão próximos dos esperados, mas há pequenas discrepâncias na componente WL (atrito lateral).
- Fórmula de `p_seg` para prismas foi ajustada para `p_seg = avg_f_k * d2d1n3 * segment_width`.
- Possíveis melhorias:
  - Validar fórmula de `p_seg` contra a teoria original.
  - Testar fator de divisão alternativo (16).
  - Investigar sensibilidade numérica em casos extremos.
  - Refatorar com NumPy para maior eficiência.

## Licença
Este projeto é fornecido sem garantia. Consulte a licença específica (se aplicável) ou entre em contato com os desenvolvedores para mais informações.
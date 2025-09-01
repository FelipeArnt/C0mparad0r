# C0mparad0r
Script desenvolvido no LABELO para comparação recursiva entre diretórios/pastas, identificando recursivamente mudanças entre ambas.

O script identifica arquivos que foram **adicionados**, **removidos** ou **modificados** entre as duas versões, incluindo todas as subpastas.

## Funcionalidades

* **Interface Gráfica**: Utiliza uma janela de diálogo nativa do sistema para a seleção das pastas, tornando o uso mais intuitivo.
* **Comparação Recursiva**: Analisa não apenas os arquivos na raiz das pastas selecionadas, mas também em todos os seus subdiretórios.
* **Relatório Detalhado**: Apresenta um relatório claro e formatado no terminal, destacando:
    * `[MODIFICADOS]`: Arquivos que existem em ambas as pastas, mas com conteúdo diferente.
    * `[REMOVIDOS]`: Arquivos que só existem na pasta antiga.
    * `[ADICIONADOS]`: Arquivos que só existem na pasta nova.
* **Medição de Desempenho**: Calcula e exibe o tempo total da operação de comparação.
* **Portabilidade**: Escrito em Python com bibliotecas padrão, não necessitando de instalação de pacotes externos.

## Requisitos

* **Python 3.x**

Todas as bibliotecas utilizadas (`os`, `sys`, `filecmp`, `tkinter`, `time`) fazem parte da biblioteca padrão do Python, portanto, nenhuma instalação adicional é necessária.

## Como Usar

1.  Salve o código em um arquivo com a extensão `.py`, por exemplo, `comparador.py`.
2.  Abra um terminal (Prompt de Comando, PowerShell, ou Terminal do Linux/macOS).
3.  Navegue até o diretório onde você salvou o arquivo.
4.  Execute o script com o seguinte comando:
    ```bash
    python comparador.py
    ```
5.  Uma janela de seleção de pasta será aberta. Selecione a primeira pasta ("PACOTE ANTIGO").
6.  Em seguida, outra janela será aberta. Selecione a segunda pasta ("PACOTE ATUALIZADO").
7.  Após a seleção, o script realizará a comparação e exibirá o relatório completo diretamente no terminal.

## Explicação do Código e da Biblioteca `filecmp`

O script é dividido em funções lógicas que orquestram a seleção, comparação e formatação dos resultados. O coração da lógica de comparação é a biblioteca nativa do Python `filecmp`.

### A Biblioteca `filecmp`

`filecmp` é um módulo poderoso para comparações de arquivos e diretórios. A classe principal utilizada neste script é a `filecmp.dircmp`.

#### Como funciona `filecmp.dircmp`?

Ao criar um objeto `dircmp(pasta1, pasta2)`, a classe realiza uma comparação superficial (não lê o conteúdo dos arquivos ainda) entre os dois diretórios e expõe os resultados através de seus atributos. Os mais importantes usados no script são:

* `dircmp.left_only`: Uma lista de arquivos e subdiretórios que existem **apenas** no primeiro diretório (`pasta1`). O script interpreta isso como **[REMOVIDOS]**.
* `dircmp.right_only`: Uma lista de arquivos e subdiretórios que existem **apenas** no segundo diretório (`pasta2`). O script interpreta isso como **[ADICIONADOS]**.
* `dircmp.diff_files`: Uma lista de arquivos que existem em ambos os diretórios, mas cujo conteúdo é **diferente**. Para determinar isso, `dircmp` realiza uma comparação binária dos arquivos. O script chama isso de **[MODIFICADOS]**.
* `dircmp.subdirs`: Um dicionário que mapeia os nomes dos subdiretórios que são comuns a ambas as pastas para novos objetos `dircmp`. É essa estrutura que permite ao script navegar e comparar as pastas de forma **recursiva**.

### Funções do Script

* `selecionar_pasta(titulo)`: Usa a biblioteca `tkinter` para criar uma janela de diálogo gráfica, permitindo que o usuário selecione uma pasta de forma interativa. É uma melhoria de usabilidade em relação a ter que digitar os caminhos no terminal.
* `comparar_pastas(pasta1, pasta2)`: É a função principal da lógica de comparação. Ela cria o objeto `dircmp`, coleta os resultados (`left_only`, `right_only`, `diff_files`) e, o mais importante, itera sobre `dircmp.subdirs` para chamar a si mesma, aplicando a mesma lógica de comparação para cada subpasta encontrada.
* `formatar_resultados(resultados, nivel)`: Pega o dicionário de resultados gerado pela função `comparar_pastas` e o transforma em uma string formatada e indentada, pronta para ser exibida ao usuário.
* `main()`: É a função que orquestra todo o processo: chama a seleção de pastas, inicia a comparação, verifica se houve alguma alteração e, por fim, imprime o relatório final.

## Exemplo de Saída
```bash

================================================================================

================================================================================
Comparando pastas:

Primeiro pacote: /caminho/para/pacote_v1

Pacote Atualizado: /caminho/para/pacote_v2
================================================================================

================================================================================
ALTERAÇÕES ENCONTRADAS:

[MODIFICADOS]:

config.ini

main.py

[REMOVIDOS]:

arquivo_antigo.txt

manual.pdf

[ADICIONADOS]:

novo_recurso.py

documentacao.html

Subdiretório: assets
[ADICIONADOS]:
- icone_novo.png

Subdiretório: lib
[MODIFICADOS]:
- utils.py
```

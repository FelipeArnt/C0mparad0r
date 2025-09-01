# 🔎 C0mparad0r
Script desenvolvido durante o período de assistente de laboratório no LABELO para comparação recursiva entre diretórios/pastas, identificando mudanças feitas em ambas.

## Funcionalidades
- **Interface Gráfica**: Utiliza uma janela de diálogo nativa do sistema para a seleção das pastas, tornando o uso mais intuitivo.
- **Comparação Recursiva**: Analisa não apenas os arquivos na raiz das pastas selecionadas, mas também em todos os seus subdiretórios.
- **Relatório Detalhado**: Apresenta um relatório claro e formatado no terminal, destacando:
    - `[MODIFICADOS]`: Arquivos que existem em ambas as pastas, mas com conteúdo diferente.
    - `[REMOVIDOS]`: Arquivos que só existem na pasta antiga.
    - `[ADICIONADOS]`: Arquivos que só existem na pasta nova.
- **Medição de Desempenho**: Calcula e exibe o tempo total da operação de comparação.
- **Portabilidade**: Escrito em Python com bibliotecas padrão, não necessitando de instalação de pacotes externos.

## Requisitos
- **Python 3.x**
- Todas as bibliotecas utilizadas (`os`, `sys`, `filecmp`, `tkinter`, `time`) fazem parte da biblioteca padrão do Python, portanto, nenhuma instalação adicional é necessária.

## Uso
- Execute o script com o seguinte comando:
    ```bash
    python comparador.py
    ```
- Uma janela de seleção de pasta será aberta. Selecione a primeira pasta ("PACOTE ANTIGO").
- Em seguida, outra janela será aberta. Selecione a segunda pasta ("PACOTE ATUALIZADO").
- Após a seleção, o script realizará a comparação e exibirá o relatório completo diretamente no terminal.

## Exemplo de Saída
```bash
================================================================================
Comparando pastas:
================================================================================
Primeiro pacote: /caminho/para/pacote_v1
Pacote Atualizado: /caminho/para/pacote_v2
================================================================================

ALTERAÇÕES ENCONTRADAS:
================================================================================
[MODIFICADOS]:
- config.ini
- main.py
================================================================================
[REMOVIDOS]:
- arquivo_antigo.txt
- manual.pdf
================================================================================
[ADICIONADOS]:
- novo_recurso.py
- documentacao.html

- Subdiretório: assets
================================================================================
[ADICIONADOS]:
- icone_novo.png
- Subdiretório: lib
================================================================================
[MODIFICADOS]:
- utils.py
================================================================================
```

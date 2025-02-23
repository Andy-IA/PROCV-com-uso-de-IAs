# Explicação Detalhada dos Passos para Usar o PROCV no LibreOffice Calc

Fico muito feliz que tenha dado certo! 😊 Vou explicar detalhadamente os passos que realizamos para que você possa compreender plenamente como a fórmula funciona e possa aplicá-la com confiança no futuro.

## Contextualizando o Problema

**Objetivo:** Unir duas planilhas, **"filtrada status"** e **"fundamentos"**, baseadas em uma coluna comum (**"TICKER"** em uma e **"papel"** em outra), agregando as colunas de ambas em uma nova planilha, apenas para os ativos em comum.

---

## Passo a Passo Explicado

### 1. Entendendo as Planilhas e as Colunas

**Planilha 1:** `filtrada status`

- **Coluna A:** `"TICKER"` – contém os códigos dos ativos.

**Planilha 2:** `fundamentos`

- **Coluna A:** `"papel"` – também contém os códigos dos ativos.
- **Colunas B, C, etc.:** Contêm informações adicionais que queremos trazer para a nova planilha.

**Nota Importante:** As colunas **"TICKER"** e **"papel"** representam os mesmos dados (os códigos dos ativos), servindo como chave para relacionar as duas planilhas.
### 2. Preparando a Nova Planilha

1. **Crie uma nova planilha** onde faremos a consolidação dos dados.

2. **Copie para a nova planilha** as colunas da planilha **"filtrada status"** que você deseja manter, incluindo a coluna **"TICKER"**.

---

### 3. Compreendendo a Função PROCV

A função **PROCV** (Procura Vertical) é usada para procurar um valor em uma coluna e retornar um valor correspondente de outra coluna na mesma linha.

**Sintaxe da Função:**

```plaintext
=PROCV(valor_procurado; matriz_tabela; índice_coluna; [procurar_intervalo])


valor_procurado: O valor que você quer encontrar (neste caso, o "TICKER").

matriz_tabela: O intervalo de células onde a busca será realizada (na planilha "fundamentos").

índice_coluna: O número da coluna no intervalo da matriz_tabela que contém o valor a ser retornado.

procurar_intervalo: Use 0 ou FALSO para correspondência exata.


---

**Parte 3:**

```markdown
### 4. Escrevendo a Fórmula Passo a Passo

**a) Referenciando o Valor Procurado**

- **A2**: É a célula na nova planilha que contém o **"TICKER"** do ativo que queremos procurar.

**b) Definindo a Matriz Tabela**

- **fundamentos.$A$2:$B$1000**: Representa o intervalo na planilha **"fundamentos"** onde a busca será realizada.
  - **fundamentos**: Nome da planilha onde estão os dados.
  - **$A$2:$B$1000**: Intervalo de células que inclui:
    - Coluna **A** (**"papel"**): Onde será procurado o valor.
    - Coluna **B**: Onde está o valor que queremos trazer (por exemplo, **"Setor"** ou qualquer outra informação).

**Notas Sobre o Intervalo:**

- O uso do **$** (cifrão) fixa a referência, impedindo que ela mude ao copiar a fórmula para outras células.
- Certifique-se de que o intervalo abrange todas as linhas com dados na planilha **"fundamentos"**.

**c) Determinando o Índice da Coluna**

- **2**: Indica que queremos o valor da segunda coluna do intervalo **$A$2:$B$1000**.
  - Coluna **A** é o índice **1**.
  - Coluna **B** é o índice **2**.

**d) Definindo o Tipo de Correspondência**

- **0**: Especifica que queremos uma correspondência exata (apenas quando os valores forem exatamente iguais).

**e) Construindo a Fórmula Completa**

Assim, a fórmula fica:

```plaintext
=PROCV(A2; fundamentos.$A$2:$B$1000; 2; 0)



---

**Parte 4:**

```markdown
### 5. Tratando Possíveis Erros com SEERRO

- Ao usar o PROCV, é possível que alguns valores não sejam encontrados, resultando em um erro **#N/D**.

- Para evitar que esses erros apareçam na planilha, usamos a função **SEERRO**.

**Sintaxe de SEERRO:**

```plaintext
=SEERRO(valor; valor_se_erro)


valor: A fórmula ou valor a ser avaliado (neste caso, o PROCV).

valor_se_erro: O valor a ser retornado se houver um erro (podemos usar "" para deixar a célula em branco).

Aplicando SEERRO à Fórmula:

=SEERRO(PROCV(A2; fundamentos.$A$2:$B$1000; 2; 0); "")


6. Inserindo a Fórmula na Nova Planilha

    Na célula B2 da nova planilha (ao lado do "TICKER" em A2), insira a fórmula acima.

Passos Práticos:

    Clique na célula B2.

    Digite a fórmula completa:


=SEERRO(PROCV(A2; fundamentos.$A$2:$B$1000; 2; 0); "")


Pressione Enter


---

**Parte 5:**

```markdown
### 7. Copiando a Fórmula para as Demais Linhas

- **Selecione a célula B2** (que contém a fórmula).

- **Utilize a alça de preenchimento** (o pequeno quadrado no canto inferior direito da célula) para arrastar a fórmula até a última linha com dados.

**Dica:** Ao arrastar a fórmula, as referências relativas (como **A2**) serão ajustadas automaticamente para **A3**, **A4**, etc.

---

### 8. Repetindo o Processo para Outras Colunas

- **Se desejar trazer informações de outras colunas** da planilha **"fundamentos"** (por exemplo, coluna **C**, **D**, etc.), repita o processo, ajustando o **índice_coluna** e o intervalo **matriz_tabela** conforme necessário.

**Exemplo para a Coluna C (índice 3):**

- Ajuste o intervalo para incluir até a coluna C: **fundamentos.$A$2:$C$1000**.

- Use o índice **3** para acessar a terceira coluna.

- Fórmula:

  ```plaintext
  =SEERRO(PROCV(A2; fundamentos.$A$2:$C$1000; 3; 0); "")



---

**Parte 6:**

```markdown
### 9. Garantindo Correspondência Correta dos Dados

- **Consistência nos Valores:** Certifique-se de que os valores em **"TICKER"** e **"papel"** são exatamente iguais, sem espaços extras ou diferenças de maiúsculas/minúsculas.

**Dicas:**

- **Remover Espaços Extras:** Use a função **ARRUMAR** se necessário.

  ```plaintext
  =ARRUMAR(A2)


Uniformizar Maiúsculas/Minúsculas: Use as funções MAIÚSCULA ou MINÚSCULA para padronizar.

=MAIÚSCULA(A2)


10. Entendendo o Significado de Cada Parte da Fórmula

    =SEERRO(...; "")

        Se a função PROCV dentro dos parênteses encontrar um erro (por exemplo, o valor não foi encontrado), a função SEERRO fará com que a célula fique em branco em vez de exibir o erro.

    PROCV(A2; fundamentos.$A$2:$B$1000; 2; 0)

        PROCV busca o valor em A2 (o "TICKER") dentro da primeira coluna do intervalo fundamentos.$A$2:$B$1000.

        Se encontrar, retorna o valor da segunda coluna do intervalo (índice 2), que corresponde à coluna B da planilha "fundamentos".

        O 0 (ou FALSO) indica que queremos uma correspondência exata.


---

**Parte 7:**

```markdown
### 11. Lidando com Possíveis Problemas

- **Erro #NOME?:** Geralmente ocorre devido a:

  - **Função não reconhecida:** Certifique-se de que seu LibreOffice Calc está em português e que está usando os nomes corretos das funções (**PROCV**, **SEERRO**).

  - **Usar o Separador Correto:** No LibreOffice Calc em português, o separador de argumentos é geralmente o ponto e vírgula **(;)**.

- **Dados Não Encontrados:**

  - Se após inserir a fórmula a célula ficar em branco (devido ao **SEERRO**), significa que o **"TICKER"** em **A2** não foi encontrado na planilha **"fundamentos"**.

---

### 12. Verificando a Correção da Fórmula

- **Exemplo Prático:**

  - Se o **"TICKER"** em **A2** for **"ABCD3"** e esse valor existir na coluna **"papel"** da planilha **"fundamentos"**, a fórmula deve retornar o valor correspondente na coluna **B** da mesma linha.

- **Teste a Fórmula com Valores Conhecidos:**

  - Escolha um **"TICKER"** que você sabe que existe e verifique se a fórmula traz o valor esperado.


### 13. Consolidando os Ativos em Comum

- **Após aplicar as fórmulas**, sua nova planilha conterá informações combinadas das duas planilhas, mas apenas os ativos em comum terão dados nas colunas trazidas da planilha **"fundamentos"**.

- **Filtrando os Ativos em Comum:**

  - Use o **Filtro Automático** para exibir apenas as linhas que possuem dados nas novas colunas.
  - Vá em **Dados** > **Autofiltro** e filtre as colunas para excluir células vazias.

---

## Conclusão

- **Dominando o PROCV:** Agora você entende como a função PROCV funciona para cruzar dados entre planilhas diferentes, utilizando uma coluna em comum.

- **Aplicações Futuras:**

  - Essa técnica é amplamente utilizada para combinar informações de diferentes fontes, sendo uma habilidade valiosa em análise de dados.

- **Pratique e Experimente:**

  - Tente aplicar esses passos com outros conjuntos de dados.
  - Explore outras funções e recursos do LibreOffice Calc para expandir ainda mais suas habilidades.

## Metáfora para Reforçar o Entendimento

Imagine que você tem dois livros de registros:

- **Livro A:** Contém uma lista de pessoas com seus nomes (**"TICKER"**) e algumas informações básicas.
- **Livro B:** Tem outra lista de pessoas com seus nomes (**"papel"**) e informações adicionais.

Você quer criar um **novo livro** que reúna todas as informações sobre as pessoas que estão nos dois livros. Usando o **PROCV**, você procura o nome de cada pessoa do Livro A no Livro B e, se encontrar, copia as informações adicionais para o novo livro. Se não encontrar, deixa em branco ou indica que a pessoa não está em ambos os registros.

---


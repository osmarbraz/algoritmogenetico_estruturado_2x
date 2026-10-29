# Algoritmo Genético Estruturado em Java para otimizar a função \(f(x)=2x\)

## 1. Descrição do projeto

Este projeto implementa um algoritmo genético em Java utilizando o paradigma de programação estruturado. Toda a implementação do algoritmo está em uma única classe a Principal.

O algoritmo utiliza cromossomos binários para representar possíveis soluções e uma função de avaliação que atribui a cada cromossomo o valor:

\[
f(x) = 2x
\]

em que \(x\) é o valor decimal correspondente à sequência binária do cromossomo.

A cada geração, os indivíduos são selecionados por roleta, combinados por crossover de um ponto e submetidos à mutação. O programa apresenta estatísticas das populações e, ao final, exibe os dados do melhor cromossomo da última população.

## 2. Objetivos

- Representar indivíduos por cromossomos binários.
- Gerar uma população inicial aleatória.
- Converter cromossomos binários para valores decimais.
- Calcular a aptidão de cada indivíduo.
- Selecionar pais por meio de roleta proporcional à aptidão.
- Criar descendentes utilizando crossover de um ponto.
- Implementar uma rotina de mutação por inversão de bits.
- Exibir estatísticas de cada geração.

## 3. Conceitos de algoritmo genético

Um algoritmo genético é uma técnica de busca e otimização inspirada em processos evolutivos. Neste programa, cada indivíduo é representado por uma sequência de bits, chamada cromossomo. A população contém vários indivíduos, e o algoritmo cria novas populações a partir da seleção de pais e da recombinação de seus cromossomos.

O ciclo implementado é composto por:

1. Geração da população inicial.
2. Cálculo da aptidão dos indivíduos.
3. Seleção dos pais por roleta.
4. Crossover de um ponto para gerar descendentes.
5. Chamada do procedimento de mutação.
6. Formação da nova população e apresentação das estatísticas.
7. Repetição até alcançar a quantidade definida de gerações.

## 4. Representação dos indivíduos

Cada indivíduo é representado por uma `String` binária de quatro bits. Por exemplo, o cromossomo `"1010"` representa o valor decimal `10`.

A população é armazenada em um vetor de strings. A população completa ao longo das gerações é armazenada em uma matriz bidimensional:

- `N = 4`: quantidade de indivíduos por população.
- `TAMANHOCROMOSSOMO = 4`: quantidade de bits por indivíduo.
- `NUMEROGERACAO = 10`: quantidade de populações consideradas durante a execução.

Como os cromossomos são gerados com quatro bits, os padrões binários completos representam valores entre `0` e `15`.

## 5. Função de aptidão

A função de aptidão implementada no código é:

\[
f(x)=2x
\]

O método `funcao(int x)` calcula o dobro do valor decimal. O método `funcao(String x)` primeiro converte o cromossomo binário para decimal e, em seguida, calcula sua aptidão.

Por exemplo, para o cromossomo `"1010"`:

- Valor binário: `1010`.
- Valor decimal: `10`.
- Aptidão: \(f(10)=2 \times 10=20\).

A aptidão é usada para calcular a soma da população e para orientar a seleção por roleta. Como a função é proporcional ao valor decimal e os cromossomos gerados podem representar zero, um indivíduo com cromossomo `"0000"` tem aptidão zero.

## 6. Como o programa funciona

A execução começa no método `main`, que cria um objeto `Principal` e chama `popular()`.

O método `popular()` gera a população inicial e apresenta suas estatísticas. Em seguida, repete o processo até completar dez populações. Para cada nova geração, chama `geracao()` usando a população anterior.

O método `geracao()` cria quatro descendentes. Para cada um deles, seleciona dois pais pela roleta, executa o crossover de um ponto, chama o método de mutação e armazena o filho na nova população.

### 6.1 Parâmetros utilizados

| Parâmetro | Valor | Significado |
|---|---:|---|
| `N` | `4` | Quantidade de indivíduos em cada população. |
| `TAMANHOCROMOSSOMO` | `4` | Quantidade de bits de cada cromossomo. |
| `PERCENTUALMUTACAO` | `0.2` | Probabilidade de 20% utilizada pelo código na rotina de mutação e também na escolha da ordem dos segmentos no crossover. |
| `NUMEROGERACAO` | `10` | Quantidade total de populações processadas, incluindo a população inicial. |

## 7. Principais métodos

| Método | Responsabilidade |
|---|---|
| `converteBinarioParaDecimal(String v)` | Converte uma string binária para um inteiro decimal. |
| `converteDecimalParaBinario(int v)` | Converte um inteiro para sua representação binária em string. |
| `converteVetorDecimalParaBinario(int v[])` | Converte todos os elementos de um vetor decimal para strings binárias. |
| `converteVetorBinarioParaDecimal(String v[])` | Converte todos os elementos de um vetor binário para inteiros decimais. |
| `mostrarVetorInteiro(int v[])` | Exibe os elementos de um vetor de inteiros. |
| `mostrarVetorString(String v[])` | Exibe os elementos de um vetor de strings. |
| `somaFuncao(String populacao[])` | Soma as aptidões de todos os indivíduos da população. |
| `estatisticas(String populacao[])` | Exibe os indivíduos, seus valores decimais, aptidões, probabilidade e índice de roleta. |
| `roleta(String populacao[])` | Seleciona um índice de indivíduo com base na soma acumulada das aptidões. |
| `gerarPopulacaoInicial()` | Cria uma população de cromossomos binários aleatórios. |
| `funcao(int x)` | Calcula a aptidão \(f(x)=2x\). |
| `funcao(String x)` | Converte o cromossomo para decimal e calcula sua aptidão. |
| `crossoverUmPonto(String pai1, String pai2)` | Combina segmentos de dois pais em um ponto de corte para produzir um filho. |
| `mutacao(String filho)` |  Inverte cada bit do cromossomo com probabilidade de 20%; na implementação atual, a alteração é devolvida ao chamador. |
| `geracao(String populacao[])` | Gera uma nova população por seleção, crossover e chamada da mutação. |
| `popular()` | Coordena a execução das dez gerações e apresenta as estatísticas. |
| `main(String args[])` | Ponto de entrada do programa. |

### 7.1 Tecnologias e ferramentas

| Tecnologia ou ferramenta | Utilização |
|---|---|
| **Java 8 (JDK 8)** | Linguagem e ambiente de desenvolvimento utilizados para implementar e executar o algoritmo. |
| **Apache Maven** | Pode ser utilizado para gerenciar a estrutura do projeto e as tarefas de compilação definidas no `pom.xml`. O código apresentado não depende explicitamente de bibliotecas externas. |
| `java.util.Random` | Gera os bits aleatórios da população inicial e escolhe o limite aleatório usado na seleção por roleta. |
| `java.lang.Math` | Fornece `Math.random()`, utilizado para escolher o ponto de corte, decidir a combinação dos segmentos e determinar tentativas de mutação. |
| `Integer.parseInt(..., 2)` | Converte strings binárias para inteiros. |
| `Integer.toString(v, 2)` | Converte inteiros para strings em base binária. |

## 8. Requisitos

- **JDK 8** ou versão compatível.
- **Apache Maven**, caso o projeto seja compilado e executado com Maven.
- Terminal ou prompt de comando para executar os comandos de compilação e iniciar o programa.

## 9. Estrutura do projeto

Considerando a estrutura convencional de um projeto Maven, os arquivos podem estar organizados da seguinte forma:

```text
algoritmo-genetico-binario/
├── pom.xml
├── README.md
└── src/
    └── main/
        └── java/
            └── Principal.java
```

O arquivo `Principal.java` contém a implementação do algoritmo genético. O arquivo `pom.xml` define as configurações do projeto Maven. Ajuste a estrutura apresentada se o projeto real utilizar outro nome de diretório ou pacote Java.

## 10. Compilação e execução

Na pasta raiz do projeto, onde está localizado o arquivo `pom.xml`, execute:

```bash
mvn clean package
```

Esse comando limpa os arquivos de compilação anteriores e empacota o projeto. A forma de execução depende das configurações existentes no `pom.xml`.

Se o projeto estiver configurado com o plugin Maven Exec, execute:

```bash
mvn exec:java -Dexec.mainClass="Principal"
```

Se a classe `Principal` estiver dentro de um pacote, utilize o nome totalmente qualificado da classe, por exemplo `br.edu.exemplo.Principal`.

Em um projeto simples sem pacote, também é possível compilar e executar diretamente pelo JDK:

```bash
javac -d target/classes src/main/java/Principal.java
java -cp target/classes Principal
```

## 11. Saída do programa

O programa apresenta estatísticas da população inicial e de cada geração subsequente. As informações exibidas incluem:

- Número do indivíduo.
- Cromossomo binário.
- Valor decimal representado pelo cromossomo.
- Aptidão calculada pela função \(f(x)=2x\).
- Campo de probabilidade.
- Índice retornado pela seleção por roleta.
- Soma das aptidões da população.

Os resultados variam entre execuções devido à geração aleatória dos cromossomos, aos cortes do crossover e às escolhas realizadas pela roleta.

## 12. Observações sobre a implementação

- **Cálculo da probabilidade:** em `estatisticas()`, a expressão `funcao(populacao[i]) / soma` divide dois valores inteiros antes de multiplicar por `100`. Isso pode fazer com que várias probabilidades apareçam como zero. Para calcular percentuais fracionários, a divisão precisaria usar valores `double`.
- **Possibilidade de aptidão total zero:** se todos os indivíduos da população forem `"0000"`, a soma das aptidões será zero. Nesse caso, a seleção por roleta não terá uma soma positiva para distribuir as probabilidades e o método pode retornar um índice inadequado.
- **Seleção por roleta:** o método pressupõe aptidões não negativas e uma soma positiva. Essa condição é satisfeita pela função `f(x)=2x` quando a população possui pelo menos um indivíduo com valor diferente de zero.
- **Crossover:** a constante `PERCENTUALMUTACAO` também é usada para escolher qual pai fornece o primeiro segmento. Esse uso é feito pelo código, embora o nome da constante sugira que ela se destina apenas à mutação.
- **Ponto de corte:** o corte é sorteado de `0` a `TAMANHOCROMOSSOMO - 1`. Um corte em zero pode fazer com que o filho seja uma cópia completa de um dos pais.
- **Conversão decimal para binário:** `Integer.toString(v, 2)` não completa o resultado com zeros à esquerda. Isso não afeta os cromossomos criados pela população inicial, que sempre têm quatro bits, mas pode ser relevante ao utilizar os métodos de conversão isoladamente.
- Os métodos `mostrarVetorInteiro`, `mostrarVetorString`, `converteVetorDecimalParaBinario` e `converteVetorBinarioParaDecimal` estão definidos, mas não são chamados pelo fluxo principal atual.

## 13. Limitações

- A população contém apenas quatro indivíduos.
- Cada cromossomo possui quatro bits.
- O programa executa dez populações e não possui um critério de parada baseado em convergência ou aptidão-alvo.
- A função de aptidão é fixa em \(f(x)=2x\).
- A mutação não modifica efetivamente os descendentes devido à forma como o método trata strings.
- O cálculo de probabilidade apresentado nas estatísticas pode estar incorreto por causa da divisão inteira.
- A seleção por roleta não trata explicitamente o caso em que a soma das aptidões é zero.
- Alguns métodos auxiliares de conversão e exibição não são utilizados no fluxo principal.


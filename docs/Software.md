# Linguagem de Programação

**Abstração:** Mascara um sistema complexo oferecendo uma interface comum\
**Assembly (bytecode):** Linguagem de baixo nível; somente compatível em uma CPU específica
	
**Nível de abstração:**  
- *Baixo Nível:* Assembly
- *Médio Nível:* C, C++, D, Objective C, etc.
- *Alto Nível:* Java, C#, PHP, Javascript, etc.
- *Altíssimo Nível:* Python, Ruby, Elixir, etc.
	
**Linguagens classificadas pela arquitetura da aplicação:**  
- *Desktop:* C, C++, Object Pascal, Java, etc.
- *Web:* PHP, Ruby, Javascript, Java, etc.
	
## Compilação e Interpretação

**Lexer (Análise Léxica):** Lexing ou Tokenização; lê os caracteres de entrada e os agrupa em unidades significativas chamadas _tokens_, seguindo as regras gramaticais definidas para a linguagem; primeira etapa do processo de compilação  
	
**Parser (Análise Sintática):** Recebe os tokens, verifica se a sequência de tokens segue a gramática da linguagem e os organiza em uma estrutura hierárquica chamada _Parse Tree_   
- *Parse Tree:* Estrutura sintática do código-fonte; representação intermediária usada pelo compilador para verificar a correção sintática do código  
- *Abstract Syntax Tree:* representação mais simplificada e abstrata do código-fonte, derivada da parse tree.
	
> Enquanto a Parse Tree mantém informações adicionais como espaços em branco e comentários, a Syntax Tree foca apenas nos elementos necessários para a geração de código de máquina  

![Formação da Syntax Tree](../images/Software/Syntax-Tree.png)

## Tipo de Execução

- *Linguagens Hibridas:* Java, Erlang, Elixir, etc
### Compiladas

*Linguagens compiladas:* C, C++, Pascal, D, GO, etc  
	
* Converte instruções humanas em instruções de máquina
* Bytecode gerado antes para execução na hora de execução _(Just in Time)_
* _.ELF (Executable and Linkable Format):_ formato de arquivo padrão comum para arquivos executáveis, código de objeto, bibliotecas compartilhadas

### Interpretadas

*Linguagens Interpretadas:* Python, Ruby, PHP, Javascript, etc  
	
* Não são compiladas antes; funcionamento a base de scripts
* Bytecode gerado depois para compilar continuamente enquanto executa _(Ahead of Time)_
	
**Interpretador:** AST (Abstract Syntax Tree) modificável\
**Script:** Código executado por interpretador que converte em instruções à CPU em sua execução\
**Linguagens Dinâmicas:** Que possuem a capacidade de injeção de novos códigos em tempo de execução

## Paradigmas de Programação
 
 - Conjunto de características que podem ser utilizados para *categorizar* determinado grupo de linguagens
 - Um paradigma pode oferecer técnicas apropriadas para uma aplicação específica
	
### Imperativo

*Programação Estruturada:* C, Pascal, Ada, etc  
*Programação Concorrente:* Java e Ada  
*Programação Orientada a Objetos:* Java, C#, C++, Objective C, D, etc  
	
- Se concentra na descrição passo-a-passo de como alcançar o resultado desejado
- É especificado explicitamente as operações a serem realizadas, incluindo sequências de instruções, condições e loops
- Controle detalhado sobre o fluxo de execução do programa

```java
public class SomaImperativa {
    public static void main(String[] args) {
        int[] numeros = {1, 2, 3, 4, 5};
        int soma = 0;
        
        for (int numero : numeros) {
            soma += numero;
        }
        
        System.out.println("Soma imperativa: " + soma);
    }
}
```

### Declarativo

*Programação Funcional:* Lisp, Scheme, Erlang, Elixir, etc  
	
 - Foca em "o quê" deve ser feito, em vez de "como" fazê-lo
 - Caracterizado por expressões que descrevem o resultado desejado sem especificar o método exato para alcançá-lo
 - É comum em linguagens de consulta (SQL) e em algumas linguagens de programação funcional

```java
import java.util.Arrays;

public class SomaDeclarativa {
    public static void main(String[] args) {
        Integer[] numeros = {1, 2, 3, 4, 5};
        int soma = Arrays.stream(numeros)
                          .reduce(0, Integer::sum);
        
        System.out.println("Soma declarativa: " + soma);
    }
}
```

|                  | Código Declarativo                  | Código Imperativo                                 |
| :--------------: | ----------------------------------- | ------------------------------------------------- |
|  **Vantagens**   | Mais simples e direto               | Mais fácil de entender quando há bugs internos    |
|                  | Mais legível                        | Mais fácil de testar                              |
|                  | Mais fácil de entender a finalidade | Mais fácil de implementar soluções personalizadas |
| **Desvantagens** | Menos explorável                    | Mais verboso                                      |
|                  | Menos flexível                      | Mais propenso a erros                             |

***

# Algoritmos

### Variáveis tipo Float

**Algarismos significativos:** número de casas decimais do resultado será igual ao do número com menor número de casas decimais\
_Exemplo:_ $$23,965 + 20,3 = 44,265$$ → $$44,3$$

* Números reais são representados por notação científica multiplicada por uma potência de base
* Seu processamento pode se dar pela “quebra” do número em parte inteira e parte decimal

**Erros de arredondamento:** Por armazenar números em formato binário, algumas frações decimais não podem ser representadas exatamente, onde o valor armazenado pode ser ligeiramente diferente do valor real

* _Acumulação de erros:_ Operações repetidas com números de ponto flutuante acumulam os erros de arredondamento, resultando em desvios significativos dos valores esperados

### Complexidade do Código

> Notação $$Big O$$

* Levar em consideração apenas _repetições de código_
* Verificar funções/métodos próprios da linguagem
* Ignorar constante e utilizar termo de maior grau (pior caso)

![BigO](../images/Software/BIgO.png)

---

# Versionamento de Software

## Identificadores Baseados em Sequência

* São usados para transmitir a _significância das alterações_ entre as versões
  * Potencial impacto em adotar uma nova versão
  * Risco de bugs ou alterações não declaradas de quebra
  * Grau de alterações no layout visual
  * Número de novos recursos
* Há uma variedade de esquemas de versionamento numérico

![Linha de Versionamento de Código](../images/Software/Versionamento-Codigo.png)

## Versionamento Semântico

![Versão em três partes](../images/Software/Major-Minor-Patch.png)

**Major (alto risco):** Modificações Breaking Change (modificação que quebra a compatibilidade da API); identificado nos commits pelo símbolo **!**\
**Minor (médio risco):** Modificações sem quebra\
**Patch (menor-risco):** Incrementos de patch\
**Pre-release tag:** Indica estágios de desenvolvimento; _alpha(a), beta(b), release candidate(rc), 0.x_

> Os desenvolvedores podem optar por **pular várias versões menores ao mesmo tempo** para indicar que recursos significativos foram adicionados, mas não são suficientes para justificar o incremento de um número de versão principal; ex: de 5.1 para 5.5

Outros esquemas conferem significado em sequências individuais:

* `major.minor[.build[.revision]]` (ex: _1.2.12.102_)
* `major.minor[.maintenance[.build]]` (ex: _1.4.3.5249_)

## Versionamento por Status mais Recente

**Sufixo Alfanumérico:** Esquema adotado pela versão semântica; traço e caracteres alfanuméricos para indicar status\
**Status Numérico:** Esquema que usa números para indicar status como se fosse parte da sequência; escolha típica é a terceira posição para o versionamento de quatro posições\
**Numeric 90+:** Esquema que também usa números, mas sob série de uma versão anterior; grande número na última posição, tipicamente 90 ou superior, comumente usado por projetos de código aberto mais antigos

| Estágio de Desenvolvimento | Versionamento Semântico | Status Numérico | Numeric90+ |
| -------------------------- | ----------------------- | --------------- | ---------- |
| Alpha                      | 1.2.0-a.1               | 1.2.0.1         | 1.1.90     |
| Beta                       | 1.2.0-b.2               | 1.2.1.2         | 1.1.93     |
| Release candidate (RC)     | 1.2.0-rc.3              | 1.2.2.3         | 1.1.97     |
| Release                    | 1.2.0                   | 1.2.3.0         | 1.2.0      |
| Post-release fixes         | 1.2.5                   | 1.2.3.5         | 1.2.5      |


---

# Testes de Software

- Garantir que o produto atingiu suas especificações e que funciona corretamente no ambiente para qual foi projetado

> Defeito ≠ Erro ≠ Falha 

*Falha:* Visível para o usuário, tem por trás algum erro  
*Erro:*  Cenário não testado pelo desenvolvedor; falha humana; evidencia o defeito  
*Defeito:* Bug; erro técnico; causa raiz  
	
*Verificação:* Verifica se esta sendo construído conforme os requisitos  
*Validação:* Valida se as regras de negócio e as expectativas do usuário foram atendidas  
	
**Níveis de Teste**  
	
*Testes Unitários:* Focam em validar a funcionalidade de componentes individuais   
*Testes de Integração:* Verificam como diferentes partes do sistema funcionam juntas; usados para identificar problemas na interação entre os componentes  
*Testes de Sistema:* Verifica se o sistema completo funciona conforme esperado, incluindo todas as suas funcionalidades e integrações; se funciona conforme esperado em um ambiente que simula o real  
*Teste de Regressão:* Garante que mudanças recentes ou correções de bugs não tenham introduzido novos defeitos em partes já testadas do software  
*Teste de Aceitação:* Últimos testes realizados antes da entrega do produto final; confirmar se o sistema atende aos critérios de aceitação definidos pelas partes interessadas; podem ser divididos em testes de aceitação do usuário (UAT) e testes de aceitação do negócio (BAT)  
	
> Alpha ➡ Beta ➡ Cannary  
	  
**Técnicas de Teste**  

*Caixa Branca:* Teste estrutural; garantir qualidade da implementação; validar dados, controles, fluxos, chamadas | Unidade, Integração, Regressão  
*Caixa Preta:* Teste funcional; verificar saídas usando vários tipos de entrada; teste sem conhecer a estrutura interna do software | Integração, Sistema, Aceitação  
*Caixa Cinza:* Mescla técnicas de Caixa branca e Caixa Preta; analisa parte lógica e também funcionalidade; Engenharia Reversa  
	
**Testes não funcionais**  
- Ligados a requisitos não funcionais (e não a regras de negócio) ➡ Qualidade
	- Comportamento do Sistema
	- Performance
	- Escalabilidade
	- Segurança
	- Infraestrutura
- Utilizam ferramentas/técnicas para apurar o comportamento do sistema em determinadas circunstâncias
	
*Teste de carga:* Verificar qual o volume de transações, acessos simultâneos ou usuários que um servidor/software/sistema suporta
*Testes de stress*: Submeter o software a situações extremas; testar os limites do software e avaliar seu comportamento, até quando pode ser exigido e quais as falhas (se existirem) decorrentes do teste  
*Testes de segurança:* Segurança cibernética que visa detectar vulnerabilidades em sistemas, software, redes e aplicativos  
	
![Pirâmide de Testes](images/Software/Piramide-Testes.jpg)

 
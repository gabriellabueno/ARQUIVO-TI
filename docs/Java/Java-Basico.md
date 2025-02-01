**Links Úteis**  
-  [Modern Java Cheat Sheet](https://philvarner.github.io/pages/modern-java.html)  
-  [Visual Guide to Swing Components](https://web.mit.edu/6.005/www/sp14/psets/ps4/java-6-tutorial/components.html)  

---

# Java

**Plataforma independente:** Java é compilado para bytecode, e este não está vinculado a nenhuma plataforma  
**Portátil:** Conceito WORA (Write Once Run Anywhere) e recurso independente de plataforma tornam o Java portátil; JVM e bytecode  
**Robusta:** Capaz de lidar com o encerramento inesperado de um programa; gerenciamento de memória forte; garbage collection automática; tratamento de exceção e mecanismo de verificação de tipo em Java  
**Compilada/Intepretada:** Os programas Java são compilados para gerar arquivos de bytecode e são interpretados, durante a execução, pelo sistema operacional do dispositivo ou pela *JVM (Java Virtual Machine)*  
**Multi-thread:** Subprocesso leve e independente de um processo que compartilha recursos; alta performance de execução    
	
**JVM - Java Virtual Machine:** Responsável pela interpretação
dos bytecodes, a execução do código; consiste em um conjunto de instruções, conjunto de registradores, a pilha (stack) , garbage-collected heap e a área de memória (armazenamento de métodos)  
		
**Compilação**  
	
```bash
javac HelloWorld.java  # compilar
java HelloWorld        # executar

javac <opção> Arquivo.java
-d dir # caminho onde as classes compiladas são armazenadas
-deprecation # compilação de código em desuso (versões anteriores)
-g # gera tabelas de debugging
-verbose # exibe informações adicionais sobre a compilação
-O # otimização de código  
-depend # compilação de todos os arquivos que dependem do arquivo que está sendo compilado

java <opção> Arquivo.java <lista de argumentos>
-debug # inicia o interpretador no modo debug
-D # redefinição de valores de propriedades
	ex = java -D nome=“Meu Nome” Hello
-jar # indica o nome do arquivo .jar que contém a classe a ser executada
-verbose # exibe informações adicionais sobre a execução

```

![](docs/Java/img/compilacao.webp)

### Pacotes

- Recurso que organiza classe, agrupamento de classes relacionadas  em um único namespace  
**Packages:** São subdiretórios, a partir da pasta *src* do projeto, onde estão localizadas as classes  
**Nome Simples:** Nome do arquivo (Usuario)  
**Nome Qualificado:** Nome do pacote + nome do arquivo (com.controle.acesso.model.Usuario)  
	
```java
package com.control.acess.model.User // define localização/pacote da classe

import com.control.acess.model.User // importa classe indicando a localização
```

**Organização de Classes** 

- Por camada  
*Model:* Representam estrutura de domínio da aplicação (Cliente, Pedido, Nota Fiscal etc)    
*Service:* Contém regras de negócio e validação de nosso sistema  
*Repository:* Contém uma integração com banco de dados  
*Controller:* Possuem a finalidade de disponibilizar alguma comunicação externa à aplicação, como http web ou webservices  
*Util:* Contém recursos comuns à toda a aplicação, utilitários  
	
```txt
├── com.app
    └── controller
        ├── CompanyController
        ├── ProductController
        └── UserController
    └── model
        ├── Company   
        ├── Product
        └── User
    └── repository
        ├── CompanyRepository   
        ├── ProductRepository
        └── UserRepository
    └── service
        ├── CompanyService
        ├── ProductService
        └── UserService
    └── util

```
	
- Por feature
```txt
├── com.app
    └── company
        ├── Company
        ├── CompanyController
        ├── CompanyRepository        
        └── CompanyService
    └── product
        ├── Product   
        ├── ProductController
        ├── ProductRepository
        └── ProductService
    └── util
    └── user
        ├── User   
        ├── UserController
        ├── UserRepository
        └── UserService
```
	
## Sintaxe
	
- Nome do arquivo `.java` deve ser o mesmo nome da Classes e deve sempre começar com letra maiúscula
- Utilizar o padrão "camelCase" em nomes de variáveis e métodos
- Variáveis dentro de um método devem ser inicializadas explicitamente para serem utilizadas

**Valores default:** Para boolean é `false`; para os tipos numéricos é `0` e tipo referencia é `null`  
	
**Tipos de Dados Primitivos**  
- Todo número Inteiro é tratado como int, desde que seu valor esteja na faixa de valores do int
	
```java
// Identificações
long L = 10L; // para não ser tratada como int
float F = 3.1f; // para não ser tratada como double
double pi = 3.14D; // para não comprometer a precisão numérica
```
	
 **Classe Executável:** Classe com capacidade de inicializar o projeto  
 - Possui método `main()` com visibilidade `public`, definida como `static`, do tipo `void`, pois não deve retornar nenhum valor, e deve ter como parâmetros um array de string `String[]`  
**Variáveis:** Iniciar com letra minúscula  
- Deve conter apenas letras, _ , $ ou os números de 0 a 9  
- Constantes são representadas pela palavra `final`, deve ser escrita em caixa alta e a divisão de palavras utilizando underline
- `final double PI_VALUE = 3.14;`  
	
**Métodos:** Devem ser nomeados como verbo  
**Indentação:** Escrever o código de forma hierárquica, facilitando a visualização e entendimento  

**Construtor:** Método que é unicamente invocado no momento da criação (instanciação) do objeto por meio do operador `new`;  sua função é criar (alocar memória) e inicializar as instâncias de uma classe; deve ter o mesmo nome da classe; uma classe pode ter um ou mais construtores (diferenciados pelos parâmetros)  

```java
public class Student {
	String name; 
	int age;

	public Aluno() {
		
	}
	
	public Aluno() {
		this.name = name;
		this.age = age;
	}
}
```

**Instanciação:** Operação de atribuição; objeto recebe espaço na memória reservado pelo construtor (`new`)    
	
```java 
// Instanciação
ExClass objectOne = new ExClass();
OtherClasse objectTwo = new OtherClasse(argument);
```
	
**Atributo (variável) Estático:** Valores compartilhados por todos os objetos  
- `private static double notaMinAprovacao`  
	
**Classes/Objetos anônimos:** Instância de classe que é utilizada uma única vez, enquanto estiver na memória  
- `new ClasseAnon();`   
	
## Modificadores de acesso
	
- Visibilidade
	
- *(-) private:* Somente a classe pode ver o valor do atributo  
- *(+) public:* Qualquer classe pode ver o valor do atributo  
- *(#) protected:* Somente a própria classe ou suas filhas por herança podem ver o valor
- *(~) package:* Somente classes do mesmo pacote podem ver o valor do atributo
	
| Direito de acesso                |  +  |  -  |  #  |        ~        |
| :------------------------------- | :-: | :-: | :-: | :-------------: |
| Membros da mesma classe          | sim | sim | sim |       sim       |
| Membros de classes derivadas     | sim | não | sim |       sim       |
| Membros de qualquer outra classe | sim | não | não | no mesmo pacote |
	
## Argumentos
	
- Quando uma classe que contenha o método **main** é executada, pode-se passar um array de argumentos, do tipo String  
-  Os parâmetros podem ser informados via linha de comando após a especificação da classe a ser executada  
- `java MyClass argument1 argument2`  
	
```bash
java AboutMe John 25 1.80
```
	
```java
public class AboutMe {
    public static void main(String[] args) {

        String name = args [0];
        int age = Integer.valueOf(args[1]);
        double height = Double.valueOf(args[2]);

        System.out.println("Name: " + nome);
        System.out.println("Age: " + age  + " and Height: " + height + " cm");
    }
}
```
	
- Também é possível passar argumentos pré-definidos via IDE, através do documento `launch.json`
	
```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "type": "java",
            "request": "launch",
            "mainClass": "AboutMe",
            "args": ["John", "25", "1.80"]
        }
    ]
}
```

## Classes 
	
**Scanner (Input)**  
	
```java
import java.util.Scanner;

String name ="abc";
int age;

Scanner scanner = new Scanner(System.in); // input de dados

name = scanner.next(); // strings
age = scanner.nextInt(); // números inteiros
heigth = scanner.nextDouble(); // números com ponto flutuante
System.out.println("Name: " + name + ", Age:" + age);

scanner.close();
```
	
**Date**  
	
```java
import java.time.LocalDate;

public class Main {
  public static void main(String[] args) {
    LocalDate myObj = LocalDate.now(); // cria um objeto LocalDate
    System.out.println(myObj); 
  }
}
```
	
**Random**  
	
```java
import.java.util.Random;

Random random = new Random(); // objeto Random para gerar números aletórios
int num = random.nextInt(100) + 1; // 0 até 100

```
	
**Enums:** Tipo especial de classe (*conjunto de objetos*), onde os objetos são previamente criados, imutáveis e disponíveis por toda aplicação  
- As opções (objetos), devem ser descritos em caixa alta separados por underline  
- Após as opções, deve-se encerrar com ponto e vírgula ";" 
- Um enum é como uma classe, logo, poderá ter atributos e métodos
- Os valores dos atributos devem já ser definidos após cada opção, dentro de parênteses como se fosse um new
- O construtor deve ser privado  
- Não é comum um enum possuir o recurso setter, somente os getters correspondentes  
- Não é possível instanciar um Enum
	
```java
public enum BrazilianStates {
	SAO_PAULO ("SP","São Paulo"),
	RIO_JANEIRO ("RJ", "Rio de Janeiro"),
	PIAUI ("PI", "Piauí"),
	MARANHAO ("MA","Maranhão") ;
	
	final String name; // "final" para não permitir alterações
	final String letters;
	
	private BrazilianStates(String letters, String name) {
		this.letters = letters;
		this.name = name;
	}
	
}
```
	
```java
BrazilianStates state = BrazilianStates.SAO_PAULO;
	
System.out.println(BrazilianStates.SAO_PAULO.letters); // SP
```
	
## Strings
	
**Comparação de Strings**  
	
```java
var.equals(varEx);
```
	
**Formatação de números com ponto flutuante** 
	
```java
double d = "1234567890.123456";

	System.out.println( );    // 1,234,567,890.12
System.out.println(String.format("%,.4f", d));    // 1,234,567,890.1235
System.out.println(String.format("%,020.2f", d)); // 00001,234,567,890.12
System.out.println(String.format("%,.010f", d));  // 1,234,567,890.1234560000
System.out.println(String.format("%e", d));       // 1.234568e+09
System.out.println(String.format(Locale.GERMAN, "%,.2f", d)); 1.234.567.890,12
```
	
## Palavras Reservadas
	
**Modificadores de classes, variáveis ou métodos**  
	
- *abstract:* classe que não pode ser instanciada ou método que precisa ser implementado, por uma subclasse não abstrata  
- *extends:* indica a superclasse que a subclasse está estendendo  
- *final:* impossibilita que uma classe seja estendida, que um método seja sobrescrito ou que uma variável seja reinicializada  
- *implements:* indica as interfaces que uma classe irá implementar  
- *native:* indica que um método está escrito em uma linguagem dependente de plataforma  
- *static:* faz um método ou variável pertencer à classe ao invés de às instâncias  
- *strictfp:* usado em frente a um método ou classe para indicar que os números de ponto flutuante seguirão as regras de ponto flutuante, em todas as expressões  
- *synchronized:* indica que um método só pode ser acessado por uma thread de cada vez  
- *transient:* impede a serialização de campos  
- *volatile:* indica que uma variável pode ser alterada durante o uso de threads  
	
**Tratamento de erros**  

- *assert:* testa uma expressão condicional  
- *try:* bloco de código que tentará ser executado, mas que pode causar uma exceção  
- *catch:* declara o bloco de código usado para tratar uma exceção  
- *finally:* bloco de código, após um try-catch, que é executado independentemente do fluxo de programa seguido ao lidar com uma exceção  
- *throw:* usado para passar uma exceção para o método que o chamou  
- *throws:* indica que um método pode passar uma exceção para o método que o chamou  
	
**Variáveis de referência**  
	
- *super:* superclasse imediata  
- *this:* instância atual do objeto  
	
> *const*: não utilizar para declarar constantes; usar **public static final**  
	
**Escopo de uso**  
	
| Uso      | Palavras                                                        |
| -------- | --------------------------------------------------------------- |
| Arquivo  | package, import, static.                                        |
| Classe   | public/protected/private + final/ abstract + extends/implements |
| Método   | public/protected/private  + static/final/abstract + void/return |
| Atributo | public/protected/private + static/final + tipo primitivo        |
	
| Palavra | Oposto     | Explicação                                                                                                                                                               |
| ------- | ---------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| package | import     | *package* determina o diretório real da classe; *import* informa de onde será importada a classe; devido a possibilidade de classes de mesmo nome                        |
| extends | implements | *extends* determina que uma classe estende outra classe; *implements* determina que uma classe implementa uma interface, porém nunca o contrário                         |
| final   | abstract   | *final* determina fim de alteração de valor ou lógica comportamental; *abstract* em métodos, exige que sub-classes precisarão definir comportamento e um método abstrato |
| throws  | throw      | *throws* determina que um método pode lançar uma exceção; *throw* é a implementação que dispara a exceção                                                                |



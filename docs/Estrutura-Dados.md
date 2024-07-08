

**Links Úteis**  
📌 [Data Structure Visualization](https://www.cs.usfca.edu/\~galles/visualization/Algorithms.html)\
📚 [Visualizing Algorithms](https://bost.ocks.org/mike/algorithms/)

***

> Array ➡ pesquisa  
> Lista ligada ➡ inserção/remoção sob demanda  

* Uma estrutura de dados é composta por dados/operações e algoritmos
* Programa = estrutura de dados + algoritmos

**Alocação Estática:** Arrays; elementos constantes; aloca espaços de acordo com o número de elementos\
**Alocação Dinâmica:** Ponteiros; não há um máximo de dados de elementos; usa espaço suficiente para um dado elemento

# Tipo Abstrato de Dados (ADT)

Contém duas partes:

1. Dados armazenados
2. Funções que manipulam os dados

* Encapsulamento de dados e operações
* Os dados podem ser armazenados em _variáveis, arrays ou ponteiros_
* As funções implementam procedimentos através de subprogramas chamados _operações, métodos ou serviços_

> INSERIR | REMOVER | CONSULTAR

## Fila

* Estrutura linear
* FIFO - primeiro a entrar, primeiro a sair
* Inserção no final
* Remoção no início

<details>

<summary>código</summary>

```java
public class Queue { 
	private int capacity;
	private int size;
	private int[] data;
	
	public Queue(int c) {
		capacity = c;
		size = 0;
		data = new int[capacity];
	}
	
	public boolean isEmpty() {
		return size == 0;
	}
	
	public boolean isFull() {
		return size == capacity;
	}
	
	// insere no fim
	public void enqueue(int d) { 
		if (isFull()) {
			System.out.print("Full!");
		} else {
			data[size] = d;
			size++;
		}
	}
	
	// remove do topo
	public void dequeue() { 
		if (isEmpty()) {
			System.out.print("\nEmpty!");
		}
		for (int i=0; i < size-1; i++) {
			data[i] = data[i+1];
		}
		size--;
	}
	
	public void print() {
		if(isEmpty()) {
		} else {
			System.out.println();
			for (int i=0; i < size; i++) {
				System.out.print(data[i] + " ");
			}
		}
	}
}

```

```java
public class Node {
	int data;
	Node next;
	
	public Node(int data) {
		this.data = data;
		this.next = null;
	}
}
```



</details>

## Lista

* Estrutura linear
* Pode conter elementos como: tipo primitivo (strings, números); tipo abstrato
* Inserções e exclusões em qualquer lugar
* _array_ para dados | _tamanho_ | _capacidade_

<details>

<summary>código</summary>

```java
public class List {
	
	private int capacity;
	private int size;
	private int[] data;
	
	public List(int c) {
	    capacity = c;
	    size = 0;
	    data = new int[capacity];
	}
	
	 public boolean isEmpty() {
	    return size == 0;
	}
	
	public boolean isFull() {
	    return size == capacity;
	}
	
	public int search(int d) {
	    for (int i = 0; i < size; i++) {
		    if (data[i] == d)
	        return i;
	    }
	    return -1;
	}
	
	 // insere no final
	public void insert(int d) {
	    if (isFull()) {
		    System.out.print("Full!");
	    } else {
		    data[size] = d;
		    size++;
	    }
	}
	
	public int delete(int d) { 
	    int i = search(d);
		
	    if (isEmpty()) {
		    return -1;
	    } else {
		     // move item para esquerda
		    for (int j = i; j < size - 1; j++) {
		        data[j] = data[j + 1];
		    }
		    size--;
		    return i;
	    }
	}
	
	public void list() {
	    if (isEmpty()) {
		    System.out.print("\nEmpty!");
		} else {
		    System.out.println();
		    for (int i = 0; i < size; i++) {
		        System.out.print(data[i] + " ");
		    }
	    }
	}
}
```

</details>

**ArrayList**

```java
import java.util.ArrayList;

public class Main {
  public static void main(String[] args) {
    ArrayList<String> cars = new ArrayList<String>();
    cars.add("Volvo");
    cars.add("BMW");
    cars.add("Ford");
    System.out.println(cars);
  }
}
```

**Lista Ligada**

* Alocação dinâmica
* Sequência de elementos chamados _nós_, onde cada nó está conectado ao próximo nó por meio de um ponteiro
* _dados_ - informação armazenada | _próximo_ - ponteiro para o próximo nó
* _cabeça_ - primeiro nó | _cauda_ - último nó (ponta para NULL)

![](../images/Estrutura-Dados/Lista-Ligada.png)

<details>

<summary>código</summary>

```java
public class LinkedList { 
	Node head;
	
	// adiciona um nó no primeiro índice, substitui nó cabeça
	public void addHead(int d) {
		Node newNode = new Node(d);
		newNode.next = head; // liga novo nó com antiga cabeça
		head = newNode;
	}
	
	// insere no fim
    public void appendNode(int d) { 
        Node current = head; // ponteiro temporário
        Node newNode = new Node(d);
        
        if (isEmpty())
            appendNode(d);
         else  {
	        // loop para procurar último nó
            while (current.next != null) { 
                current = current.next;
            }
            current.next = newNode;
        }
    }
	
	public Node removeHead() {
		Node aux = null;
		
		if (!isEmpty()) {
			head = head.next;
		}
		return aux;
	}
    
    public Node search(int d) {
        Node aux = null;
        Node current = head; // ponteiro temporário
		
		// loop para percorrer lista
        while (current != null) {
            if (current.data == d) {
                aux = current;
                break;
            }
            current = current.next;
        }
        return aux;
    }
	
	// loop simplificado
    public Node search2(int d) {
        Node aux = null;
        Node current = head;
		
		// une todas as condições
		/// for ( inicialização; condição; incremento)
        for(; current!=null && current.data!=d; current=current.next) {
        }
        // quando valor é encontrado
        aux = current;
        return aux;
    }
    
    public boolean isEmpty() {
        return head == null;
    }
    
    public void print() {
        No current = head;
        
        while (current != null ) {
            System.out.print(current.data + " ");
            current = current.next;
        }
        System.out.println();
    }
	
}
```



</details>

**LinkedList**

```java
import java.util.LinkedList;

public class Main {
  public static void main(String[] args) {
    LinkedList<String> cars = new LinkedList<String>();
    cars.add("Volvo");
    cars.add("BMW");
    cars.add("Ford");
    System.out.println(cars);
  }
}
```

**Lista (Ligada) Circular**

* Alocação dinâmica
* Feita por elementos que contêm ponteiros para o próximo elemento
* Variação da lista ligada na qual o último elemento, em vez de apontar para null, aponta para o primeiro nó _(loop)_
* Qualquer nó pode ser um ponto de partida
* _dados_ | _próximo_ | _cabeça_ | _cauda_ | _tamanho_ | _capacidade_

![](../images/Estrutura-Dados/Lista-Ligada-Circular.png)

<details>

<summary>código</summary>

```java
public class CircularList {
	int[] data;
	int head, tail, size, capacity;
	
	CircularList(int c) {
		head = 0;
		tail = 0;
		size = 0;
		capacity = c;
		data = new int[capacity];
	}
	
	boolean isEmpty() {
		return size == 0;
	}
	
	boolean isFull() {
		return size == capacity;
	}

	// insere no fim
	void insert(int d) {
		if (isFull())
			System.out.println("isFull!");
		else {
			data[tail] = d;
			size++;
			tail = (tail+1) % capacity; // recalcula posição da cauda
		}
	}

	// remove no início
	void remove() {
		if(isEmpty())
			System.out.println("isEmpty!");
		else {
			head = (head+1) % capacity; // recalcula posição da cabeça
			size--;
		}
	}
	
	void list() {
		for (int i=0; i < size; i++) {
			System.out.println(" " + data[ (head+i)% capaticy ])
		}
	}
	
}
```



</details>

## Pilha

* LIFO - último a entrar, primeiro a sair
* Estrutura linear
* As inserções e exclusões ocorrem no _topo_ da pilha
* Usada em recursão
* _topo_ (-1) | _array_ para dados | _capacidade_

<details>

<summary>código</summary>

```java
public class Stack {
	int top, capacity;
	int[] data;
	
	Stack(int c) {
	    capacity = c;
	    top = -1;
	    data = new int[capacity];
	}
	
	public boolean isEmpty() {
	    return top == -1;
	}
	
	public boolean isFull() {
	    return top == capacity - 1;
	}
	
	public void push(int d) {
	    if (isFull())
	      System.out.println("FULL!");
	    else {
	      top++;
	      data[top] = d;
	    }
	}
	
	public int pop() { 
	    int aux = -1;
	    if (isEmpty())
	      System.out.println("isEmpty!");
	    else {
	      aux = data[top];
	      top--;
	    }
	    return aux;
	}
	
	public void list() {
		for (int i = top; i >= 0; i--) {
			System.out.println(data[i] + " ");
		}
	}
	
}
```



</details>

## Recursão

* Condição de parada
* Chama a si mesma
* Mudança de estado

<details>

<summary>exemplos</summary>

```java

  public static int sum(int n) {
    if (n == 1)
      return 1;
    return n + sum(n-1);
}

 public static float sumF(float[] n, int i) {
    if (i == 0)
      return n[0];
    return n[i] + sumF(n, i-1);
}

  public static int sumEven(int n) {
    if (n == 1)
      return 0;
    if (n % 2 == 0)
      return n + sumEven(n-1);
    return sumEven(n-1);
}

  public static int sumOdd(int n) {
    if (n == 1)
      return 1;
    if (n % 2 == 1)
      return n + sumOdd(n-1);
    return sumOdd(n-1);
}

  public static void mult(int[] n, int i) {
    if (i >= 0) {
        mult(n, i-1);
		if (n[i] % 3 == 0)
	        System.out.print(n[i] + " "); 
    }
}
  
  public static int mdc(int a, int b) {
    if (b == 0)
      return a;
    return mdc(b, a % b);
}

  public static int exp(int x, int n) {
    if ( n == 0)
      return 1;
    return x * exp(x, n-1);
}

  public static int method(int n) {
    if (n == 1)
      return 1;
    return method(n-1) + n;
}

```



</details>

# Ordenação

## Bubble Sort

* Mais simples e mais lento algoritmo de ordenação
* Passa muitas vezes pelo array e compara os elementos em pares
* Se o primeiro for maior que o próximo número, troca os valores
* Em cada passagem os números mais baixos "flutuam" para o topo, lembrando bolhas em um tanque de água
* Melhor caso = $$O(n)$$
* Pior caso = $$O(n²)$$

<details>

<summary>código</summary>

```java
public static void bubbleSort(int[] array, int size) {
	boolean swap = true;
	int aux = 0;

	for(int i=0; i< size && swap; i++) {

		swap = false;
		for(int j=0; j< size-i-1; j++) {

			if(array[j] > array[j+1]) {
				swap = true;
				aux = array[j];
				array[j] = array[j+1];
				array[j+1] = aux;
			}

		}
	}
	return;
}
```



</details>

## Quick Sort

* Dividir para conquistar ➡ divide um problema maior em um problema recursivo menor
* A chave é o particionamento
* Escolhe um pivô e divide o array em torno do pivô escolhido
* Então, usando dois ponteiros, um para a esquerda e outro p/ a direita, compara os números ao pivô
* Os números menores que o pivô vão p/ o lado esquerdo e os maiores p/ o lado direito

## Merge Sort

* Também divide para conquistar
* Divide o array pela metade, então continua dividindo até que fique em grupos menores
* Compara os elementos de um grupo com outro para organizá-los em ordem, então mescla os elementos em um grupo maior
* E continua até que o array esteja totalmente unido e em ordem

<details>

<summary>código</summary>

```java
public static void mergeSort(int[] array) {
    int sizeArray = array.length;

    if(sizeArray < 2) { // se houver somente 1 elemento
        return;
    }

    int middle = sizeArray / 2; 
    int[] left = new int[middle]; // parte esquerda
    int[] right = new int[sizeArray - middle]; // parte direita
    // capacidade do array = tam vetor - meio (para calcular array com tamanho impar)

    // Preenchendo os Arrays
    for(int i=0; i < middle; i++) {  // início até o meio
        left[i] = array[i];
    }

    for(int i=middle; i < sizeArray; i++) { // meio até o final
        right[i - middle] = array[i]; 
        // [i - meio] para iniciar na posição 0 do vetor
        // já que o contador/index "i" inicia em "meio"
    }

    // Chamada recursiva para divisão dos vetores
    mergeSort(left);
    mergeSort(right);

    // Unindo as metades
    merge(array, left, right);
}

public static void merge(int[] array, int[] left, int[] right) {

    int leftSize = left.length;
    int rightSize = right.length;

    // index/contadores
    int iL=0, // esquerda
        iR=0, // direita
        iA=0; // vetor de merge

    // loop até esgotar os elementos
    while (iL < leftSize && iR < rightSize) {  
        if (left[iL] <= right[iR]) {
            array[iA] = left[iL];
            iL++;
        } else {
            array[iA] = right[iR];
            iR++;
        }
        iA++;
    }

    // Como o loop continua até acabarem os elementos de 1 dos arrays
    // precisa-se confirmar se há elementos restantes

    // Adicionando elementos da esquerda, se ainda houver
    while(iL < leftSize) {
        array[iA] = left[iL];
        iL++;
        iA++;
    }
    
    // Adicionando elementos da direita, se ainda houver
    while(iR < rightSize) {
        array[iA] = right[iR];
        iR++;
        iA++;
    }

}

```



</details>

# Árvores

* Estrutura composta por um nó _raiz_ e abaixo dela suas subárvores
* Cada nó tem um "nó pai"
* Nós que não têm filhos são chamados de _folhas_
* Valores menores que o nó pai vão a sua esquerda e maiores a direita

**Grau:** Número de filhos de um nó

* Grau máximo de uma árvore identifica tipo de árvore (binária, ternária etc)

**Altura (h):** Número máximo de links/arestas no caminho mais longo entre um nó e o último nó folha

* Altura de uma árvore = altura da raiz

**Profundidade/Nível:** Número de links/arestas necessários para ,alcançar um nó a partir do nó raiz; no nível k possui no máximo $$2^k$$ nós

![Estrutura da Árvore Binária](../images/Estrutura-Dados/Arvore.png)

![Atributos da Árvore Binária](../images/Estrutura-Dados/Altura-Profundidade-Arvore.jpg)

**Árvore Binária:** Abaixo de cada nó podem ter no máximo dois filhos\
**Árvore Estritamente Binária:** Árvore binária em que todo nó que não é folha tem subárvores esquerda e direita\
**Árvore Binária Completa:** Se uma árvore binária contém _m_ nós no nível _k_, ela conterá _2m_ nós no nível _k+1_

![Ordem de exibição](../images/Estrutura-Dados/Arvore-Ordem.png)

<details>

<summary>código</summary>

```java
public class Node {
    int data;
    Node left;
    Node right;
    
    Node (int data) {
        this.data = data;
        this.left = null;
        this.right = null;
    }
}
```

```java
public class Tree {
    Node root;
    
    public boolean isEmpty() {
        return root == null;
    }
    
    public void add(int value) {
        Node newNode = new Node(value);
        
        if (isEmpty()) {
            root = newNode;
        } else {
            Node temp = root, last = root;
            
            while (temp != null) {
                last = temp;
                if (value == temp.value)
                    break;
                if (value > temp.value) 
                    temp = temp.right;
                else 
                    temp = temp.left;
            }   
            
            if (value == last.value)
                System.out.println(value + " - Value already exists!");
            else if (value > last.value)
                last.right = newNode;
            else 
                last.left = newNode;
        }
    }

    public boolean delete(Node startNode, int key) {
        if (isEmpty()) {
            System.out.println("Tree is empty!");
            return false;
        }
        
        Node current, parentNode;
        current = search(startNode, key); // nó atual
        parentNode = searchParent(startNode, key); // pai do nó atual

        if (current == null) {
            System.out.println("No item to delete!");
            return false;
        }
        
        Node replacement, parentReplacement;

		// Se não há nós a esquerda e/ou a direita do nó atual
        // Nó a ser excluido tem 0 ou 1 filho
        if (current.left == null || current.right == null) {
            if (current.left!= null)
                replacement = current.left;
            else 
                replacement = current.right;
                
            if (parentNode == null) // raiz não tem pai
                this.root = replacement;
            else {
             // Atribui a atual o valor do substituto selecionado
                if (parentNode.left == current)
                    parentNode.left = replacement;
                else
                    parentNode.right = replacement;
            }
            current = null; // remove nó atual

		// Se há nós a esquerda e a direita do nó atual
        // Nó a ser excluido tem 2 filhos
        } else {    
			// Encontra maior valor a esquerda para manter ordenação
            replacement = leftLargest(current); 

			// Busca pai do nó atual
            parentReplacement = searchParent(this.root, replacement.value);

			// Atribui a atual o valor do substituto selecionado
            current.value = replacement.value;

			/* Remove valor nó substituto, dado que
			 * valor já foi reinserido na árvore 
			 * no lugar do nó atual */
            if (parentReplacement!= null)
                if (parentReplacement.left == replacement)
                    parentReplacement.left = replacement.left;
                else
                    parentReplacement.right = replacement.left;
            
            replacement = null;
        }
        return true;
    }

	// Métodos para busca
	
    public Node search(Node temp, int value) {
       if (temp!= null)
            if (value > temp.value)
                return search(temp.right, value);
            else if (value < temp.value)
                return search(temp.left, value);
        return temp;
    }
    
    public Node searchParent(Node root, int value) {
        Node temp = root; // starts from root
        Node parent = null; // null because root doesn't have a parent
        
        while (temp!= null && temp.value!= value) {
            parent = temp; // update parent of searched value
            if (value > temp.value)
                temp = temp.right;
            else 
                temp = temp.left;
        }
        return parent;
    }

	/// busca elemento mais próximo do nó a ser removido
	/// maior número a esquerda, porém, ainda menor que o nó atual
    public Node leftLargest(Node node) {
        node = node.left;
        if (node!= null) {
            while (node.right!= null) {
                node = node.right;
            }
        }
        return node;
    }
    
    public void printPreOrder(Node root) {
        if (root == null)
            return;
        System.out.print(root.value + " ");
        printPreOrder(root.left);
        printPreOrder(root.right);
    }
    
    // Impressão da Árvore
    
    public void printInOrder(Node root) {
        if (root == null)
            return;
        printInOrder(root.left);
        System.out.print(root.value + " ");
        printInOrder(root.right);
    }
    
    public void printPostOrder(Node root) {
        if (root == null)
            return;
        printPostOrder(root.left);
        printPostOrder(root.right);
        System.out.print(root.value + " ");
    }
    
}

```



</details>

# Tabela Hash

* Tabela de dispersão ou espalhamento
* Endereçamento direto
* Visa _buscas_ eficientes, no pior caso $$O(n)$$
* Por meio de uma _função de hash_, transforma chaves em endereços de uma tabela
  * _n_ chaves para serem armazenadas em uma tabela _T_ de tamanho _m_, as posições da tabela estão no intervalo _\[0, m-1]_
  * transforma cada chave _x_ em um endereço-base _h(x)_
  * se _h(x)_ estiver desocupado, armazena-se a chave _x_

> Hash é uma estrutura de dados do tipo _dicionário_
>
> > não permite elementos repetidos\
> > não permite recuperar elementos sequencialmente (ordenado)

**Funções de Hash**\
_Método da Divisão_

* simples e amplamente utilizado
* chave x é dividida pela dimensão da tabela m e o resto da divisão é usado como endereço da chave
* $$h(x) = x \mod m$$
* deve-se escolher bem o valor de _m_ para bons resultados práticos; deixar espaços livres para casos de colisão, porém não a ponto de ser desperdício de memória
  * _m_ deve ser um número primo não próximo a uma potência de 2
  * _m_ não deve possuir divisores primos menores que 20

**Colisão:** Quando o cálculo da função de hash retorna endereços iguais para chaves distintas, sendo necessário um _tratamento de colisão_

**Tratamento de Colisão - Técnicas**\
_Encadeamento:_ Informação é armazenada em estruturas encadeadas; tabela armazena ponteiros para uma lista ligada de elementos com mesmo endereço\
_Endereçamento Aberto:_ Informação é armazenada na própria tabela hash, sem utilização de ponteiros; redução no consumo de memória

* Rehash Linear: função hash para gerar sequências de tentativas
  * $$rh(k) = (k+i) \mod M$$
  * M - quantidade de entradas na tabela

<details>

<summary>código</summary>

```java
public class KeyValue {
    private int key;
    private String value;
    
    public KeyValue(int key, String value) {
        this.key = key;
        this.value = value;
    }

    public int getKey() {
        return key;
    }

    public void setKey(int key) {
        this.key = key;
    }

    public String getValue() {
        return value;
    }

    public void setValue(String value) {
        this.value = value;
    }

    @Override
    public String toString() {
        return "[" + "key=" + key + ", value=" + value + "]";
    }
}

```

```java
public class HashTable {
    private KeyValue[] table;
    private int capacity;
    private int size = 0;
    
    public HashTable(int capacity) {
        this.capacity = capacity;
        this.table = new KeyValue[capacity];
    }

    public int getCapacity() {
        return this.capacity;
    }
    
    public int getSize() {
        return this.size;
    }
    
    public void add(int key, String value) {
        if (full()) {
            System.out.println("Hash Table is full!!!");
        } else {
            int index = addHash(key);
            this.table[index] = new KeyValue(key, value);
            this.size++;
        }
    }
    
    public int addHash(int key) {
        int hash = getHash(key);
        int i = 0;
        
		// verifica colisoes
        while(table[hash]!=null && i < capacity) {
            i++;
            hash = getHash(key + i);
        }
        return hash;
    }
    
    public int findHash(int key) {
        int hash = getHash(key);
        int i = 0;
        
		// verifica se existiram colisoes
        while ((table[hash]!=null) && table[hash].getKey()!= key && i < capacity) {
            i++;
            hash = getHash(key + i);
        }
        if ((i == capacity) || table[hash] == null) {
            System.out.println("Key not found!!!");
            return -1;
        }
        return hash;
    }
    
    public String getValue(int key) {
        int index = findHash(key);
        return this.table[index].getValue();
    }
    
    public boolean full() {
        return (this.capacity == this.size);
    }
    
    public int getHash(int key) {
        return key % capacity;
    }
    
}

```



</details>

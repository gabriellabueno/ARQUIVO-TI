# Programação Mobile

**Android**

* Sistema operacional da Open Handset Alliance
* Liderado pela Google
* Código aberto (Apache License)
  * fabricantes customizam SO
* Baseado em Linux
* Android é responsável por gerenciar memória e processos
* Apesar de ser escrito em Java e Kotlin, os apps não utilizam a JVM e os bytecodes não são executados ➡ classes Java são compiladas para executáveis da máquina virtual Dalvik
  * _Dalvik (runtime):_ VM especializada desenvolvida e otimizada especificamente dispositivos móveis
* _.apk (Android Package):_ Executável gerado após construção (build) do projeto/app; contém conteúdos necessários para o runtime e instalação
* _.aab (Android APP Bundle):_ Executável que contém os conteúdos de um projeto Android, porém adicionalmente inclui metadados que não são necessários para o runtime; formato de publicação que não pode ser instalado em dispositivos,

![Arquitetura Android](../.gitbook/assets/arquitetura-android.png)

### Tipos de Aplicativos Mobile

**Aplicativos Web**

* Acesso pelo navegador e WebView
* Não exigem instalação no dispositivo do usuário
* Desenvolvidos usando tecnologias web como HTML, JavaScript e CSS
* Publicação mais rápida; atualização automática

**Aplicativos Híbridos**

* Desenvolvidos com tecnologias web (HTML, JavaScript e CSS), mas _executados dentro de um contêiner nativo_, permitindo o acesso a recursos do dispositivo
* Combinam elementos de aplicativos nativos e da web
* Depende de uma biblioteca de terceiros
  * Camada entre o aplicativo e a biblioteca da plataforma
* São escritos uma vez e podem ser executados tanto no Android quanto no iOS
* Principais bibliotecas e ferramentas: Cordova; Phonegap; Ionic; Appcelerator; JqueryMobile; Intel XDK

**Aplicativos Multiplataformas Nativos**

* Desenvolvidos com uma única base de código que pode ser executada em diferentes SOs
* Componentes são nativos, não HTML
* Escritos em uma linguagem específica, que é convertida em código nativo _(compilação cruzada)_ ou renderizada em tempo de execução _(runtime)_ em diferentes plataformas
  * Compilação cruzada tende a ter menor desempenho ➡ menor controle de como é compilado
* Podem acessar todos os recursos do dispositivo, como acelerômetro, giroscópio, geolocalização, etc
* Principais tecnologias: Xamarin (C#); Nativescript (Javascript, Typescript e XML); React Native (Javascript, Typescript e XML)

**Aplicativos Nativos**

* Bibliotecas próprias
* Funciona como um software desktop, com possibilidade de arquitetura client/server (consumo de serviços)
* Funcionamento offline
* Armazenamento de dados localmente
* Tarefas em segundo plano

![](../.gitbook/assets/desenvolvimento-mobile.png)

![](../.gitbook/assets/mobile-development.png)

### Compilação

* Processo de transformar/traduzir um código em de linguagem de programação de alto nível em um _programa executável_

**Preprocessamento:** O pré-processador lê o código-fonte (`.java`) e faz substituições necessárias para que o programa possa ser compilado\
**Verificação sintática:** Etapa que procura por erros de sintaxe nos códigos, como parênteses não fechados, falta de ponto e vírgula no final da instrução, etc\
**Compilação propriamente dita:** Transforma o código preprocessado em um programa objeto (`.class`) , que está em linguagem de máquina (bytecode), mas ainda não está pronto para ser executado\
**Linkedição (linking):** Programas objeto e bibliotecas necessárias são linkadas, transformando-os em um único executável em linguagem de máquina própria de uma plataforma

* _Tempo de Compilação:_ Durante o processo de conversão entre código-fonte e código-objeto
* _Tempo de Execução:_ Após a ativação do programa executável

![](../.gitbook/assets/compilacao.jpg)

### Arquitetura de Aplicativos

* Dispositivos móveis também têm recursos limitados, portanto, a qualquer momento, o SO pode _eliminar processos_ de aplicativos para abrir espaço para novos
* Dadas as condições deste ambiente, é possível que os componentes sejam iniciados individualmente e fora de ordem, e o SO ou usuário pode destruí-los a qualquer momento

> Não se deve armazenar ou manter na memória nenhum dado ou estado do aplicativo em componentes do aplicativo, e os _componentes não devem depender uns dos outros_

* Classes baseadas em UI devem conter apenas lógica que lide com interações de UI e sistema operacional, não se deve armazenar dados diretamente nestas
* Deve-se conduzir a UI a partir de _modelos de dados_ (de preferência persistentes), que representam os dados de um aplicativo; eles são independentes dos elementos da interface do usuário e de outros componentes

**SSOT - Single Source Of Truth:** Quando novos dados são definidos no aplicativo, estes são atribuídos a um SSOT, que é o proprietário desses dados, e apenas o SSOT pode modificá-los\
**UDF - Unidirecional Data Flow:** O estado ou os dados geralmente fluem em uma direção, dos tipos de escopo mais alto da hierarquia para os de escopo mais baixo; eventos geralmente são acionados a partir dos tipos de escopo inferior até atingirem o SSOT para o tipo de dados correspondente

> SSOT é frequentemente usado com o padrão UDF

**Camadas**

* _UI Layer:_ UI elements; state holders
* _Data Layer:_ Repositories; data sources

![Arquitetura de um aplicativo](../.gitbook/assets/arquitetura-app.png)

***

## Programação Android em Java

### Android Studio

```java
Log.d(tag, msg); // Console Logging
```

**Alterar ícone APP**

* app/src/main/res/minimap.../ic\_launcher.xml
* alterar também arquivo `AndroidManifest.xml`
  * `icon` e `roundIcon`
* criar versões de diversos tamanhos e cortes (quadrado, redondo etc)

**Componentes de Aplicativos**

* _Activity:_ Porta de entrada de interação do usuário; representa uma única tela com a UI (User Interface); facilita manejo dos processos pelo sistema, de acordo com contexto salvo e utilização do usuário
* _Services:_ Ponto de entrada de uso geral para manter um aplicativo em execução em segundo plano, ou até este se encerrar (started service) ou por dependência de outro aplicativo ou sistema (bound service)
* _Broadcast receivers:_ Componente que permite ao sistema entregar eventos ao aplicativo fora de um fluxo normal de usuários; são outra entrada para aplicativos, permitindo que o sistema forneça transmissões mesmo para aplicativos que não estão em execução no momento
* _Content providers:_ Gerencia um conjunto compartilhado de dados de aplicativos que podem ser armazenados no sistema de arquivos; através do provedor de conteúdo, outros aplicativos podem consultar ou modificar os dados

> Como o sistema executa cada aplicativo em um _processo separado_ com permissões que restringem o acesso, para ativar um componente em outro aplicativo, uma mensagem é entregue ao sistema especificando a _intenção_ (intent) de iniciar um componente específico

**Arquivos**

* _AndroidManifest.xml:_ Antes que o sistema possa iniciar um componente do aplicativo, ele lê o arquivo de Manifest do aplicativo, onde são declarados todos os componentes
* _Layout:_ Caixas para acoplar as views; base para componentes
* _XML:_ Linguagem de Marcação Extensível; permite descrever dados de maneira estruturada para criar interfaces de usuários (UI); estático
  * Para tornar dinâmico é necessário utilizar a _classe R_

**Resources:** Recursos; arquivos adicionais e conteúdo estático que o código usa, como bitmaps, definições de layout, strings de interface de usuário, instruções de animação e etc

**Estrutura Básica**

* Gerada automaticamente pelo Android Studio
* _Bundle:_ Classe utilizada para armazenar dados que serão passados entre componentes (Activities ou Fragments); os dados são armazenados em pares de chave-valor, a chave é uma String e o valores pode ser de diversos tipos primitivos, objetos e outros Bundles

```java
import android.os.Bundle;
import androidx.appcompat.app.AppCompatActivity;

public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
    }
}
```

1. Classe `MainActivity` herda de `AppCompatActivity`
2. O método `onCreate()` da classe `AppCompatActivity` é sobrescrito (@Override)
   * Responsável por realizar configurações iniciais, como definir o layout da Activity pelo método `setContentView`
3. Recebe o parâmetro `savedInstanceState` do tipo `Bundle`
   * Contém o estado anteriormente salvo da atividade, se houver
   * Útil para restaurar o estado da Activity após ela ser destruída e recriada pelo SO
4. `super.onCreate(savedInstanceState)` chama recursivamente o método onCreate da classe pai (AppCompatActivity), passando como parâmetro o Bundle declarado
   * Este método garante que a inicialização correta da atividade seja realizada pela classe pai
5. `setContentView(R.layout.activity_main)`: define o layout da atividade, o argumento passado é um identificador de recurso que referencia o arquivo XML do layout a ser utilizado.
   * `R.layout.activity_main` refere-se ao arquivo activity\_main.xml localizado na pasta res/layout do projeto

#### Activity

* Localizado no pacote`android.app`
* Módulo único e independente que está relacionado diretamente com uma tela de _interface_ de usuário e suas funcionalidades (similar a classe JFrame do swing Java)
* Podem ser organizadas em blocos totalmente reutilizáveis para serem compartilhadas entre diferentes aplicativos
* Controla seu _estado_ e a _passagem de parâmetros_ de uma tela para outra e controla os _eventos_ dos componentes visuais.

> Toda classe que representa uma tela, estende, direta ou indiretamente, a classe `Activity`\
> Toda classe `Activity` implementa o método `onCreate()`, que é obrigatório e responsável por realizar a inicialização necessária para executar a aplicação

#### View

* Localizado no pacote`android.view`
* Classe mais básica para a construção de _componentes visuais_, dos mais simples aos mais complexos
* Todos os componentes visuais no Android, como EditText, Button, ConstraintLayout e outros, são _subclasses da classe View_
* Cada View ocupa uma área retangular na tela e é responsável por desenhar a si mesma e tratar eventos (interações do usuário)

**Listener para eventos em Botão**

* `OnClickListener` se trata de um **Interface Funcional**, ou seja, contém apenas um método abstrato que deve ser implementado na classe que implementará a interface
* **Classes Anônimas:** Classe sem nome que é definida e instanciada ao mesmo tempo, pois serão utilizadas uma única vez enquanto estiver na memória; usada para implementar interfaces ou estender classes
  * `new ClasseAnon();`

```java
@FunctionalInterface
public interface OnClickListener {
    void onClick(View v);
}

public class MyListener implements View.OnClickListener {
    @Override
    public void onClick (View v) {
         // your code here;
    }
}

-----------

public void setOnClickListener(OnClickListener listener);

// Método "setOnClickListener" da classe "Button" é um método que permite 
// a definição de um ouvinte (listener) para eventos de clique no botão
```

* Por meio de instâncias das classes anônimas podemos implementar interfaces funcionais e declarar a implementação do método abstrato que esta contém

```java
// Declaração do botão e referência ao botão definido no layout
Button btn = findViewById(R.id.botaoMsg); 

// Interface "OnClickListener" que conteḿo método chamado "onClick()"
btn.setOnClickListener(new OnClickListener() { // instância de classe anônima
	// implementação do método
	@Override 
	public void onClick(View view) {
		// Código para executar quando o botão é clicado
	}

}); 
```

* Pode-se utilizar expressões **Lambda** para abstrair o código, dado que se a interface tem somente um método, não necessita da declaração explícita, sendo assim, não é mais necessário a declaração de uma classe anônima somente para implementar a interface

```java
// IMPLEMENTAÇÃO COM LAMBDA

Button btn = (Button) findViewById(R.id.botaoMsg);

// Omiti-se a declaração da classe anônima que implementa a interface funcional
// e do Override de seu método abstrato
// Somente é declarado o parâmetro que será utilizado no método abstrato

btn.setOnClickListener(view -> { 
    // Código para executar quando o botão é clicado
});
```

#### Classe R

* Classe especial que é gerada automaticamente pelo Android Studio
* Serve como um _índice_ para recursos, responsável por encontrar os recursos descritos nos arquivos XML e construir na aplicação
* Mediador entre o arquivo XML e o arquivo.java
* Quando um layout é definido em um arquivo XML, cada elemento no layout recebe um ID único
* Quando o aplicativo é compilado, essa ID é adicionada à classe R.
* Pode então referenciar esses IDs em código para manipular os elementos do layout

`setContentView(R.layout.activity_main);`

* `R.layout.activity_main` é uma referência a um layout chamado `activity_main.xml` que está localizado na pasta _res/layout/_
* Nunca modificar a classe R manualmente, pois ela é gerada automaticamente e qualquer alteração será sobrescrita na próxima compilação

#### Intent

* Localizado no pacote `android.content.Intent`
* Representa uma “ação” que uma aplicação deseja executar; intenção
* Essa intenção é enviada ao sistema operacional Android como forma de uma mensagem
* Ligam componentes individuais entre si em tempo de execução, solicitando uma ação de outros componentes

> _Intent_ é uma mensagem assíncrona que ativa três dos quatro tipos de componentes: activities, services, and broadcast receivers

**Transição entre Activity e Intent**

* Necessário o uso do método `startActivity(intent)`
* O parâmetro `intent` a ser passado ao método contém as informações necessárias sobre a Activity que será ativada pelo SO
* Pode-se passar parâmetros (dados) de uma tela para outra com o método `putExtra(chave, valor)`
* Recupera-se dados enviados da primeira tela com o método `getStringExtra()`

```java
Intent it = new Intent(getAplicationContext(), Tela.class);
it.putExtra("msg", "Olá Mundo"); // envia dados
startActivity(it); // inicia tela

------------------------

lblMensagem = finfViewById(R.id.lbl_mensagem);

Intent it = getIntent(); // obtem objeto enviado pela primeira tela
String mensagem = it.getStringExtra("msg"); // recupera a informação pela chave
lblMensagem.setText(mensagem); // exibe a informação em um TextView na segunda tela

```

### Recursos

**Recursos de String**

* Referenciado usando o valor fornecido no atributo `name` (e não no nome do arquivo XML)
* É possível combinar recursos de string com outros recursos em um arquivo XML em um elemento `<resources>`
* Reutilização de string em arquivos XML
* Localização do arquivo ➡ `res/values/filename.xml`
  * Nome do elemento é usado como ID do recurso
* Tipo de dados do recurso compilado ➡ ponteiro para um String
* Referência do recurso
  * Em java ➡ `R.string.str_name`
  * Em XML ➡ `@string/str_name`

> É possível utilizar _arrays_ com diversas strings

```xml
<?xml version="1.0" encoding="utf-8"?>

<resources>
	<string-array name="planets-array">
		<item>Venus</item>
		<item>Earth</item>
		<item>Mars</item>
	</string-array>
</resources>

```

```java
Resources res = getResources();
String[] planets = res.getStringArray(R.array.planets_array);
```

**Reutilização de Estilos**

* Criar arquivo `styles.xml` na pasta _res/values_

```xml
<resources>

    <!-- BOTÃO PADRÃO -->
    <style name="btnPadrao" parent="">
        <item name="android:textSize">20sp</item>
        <item name="android:textColor">@color/black</item>
        <item name="android:layout_width">wrap_content</item>
        <item name="android:layout_height">wrap_content</item>
        <item name="android:fontFamily">@font/alexandria_bold</item>
    </style>

</resources>
```

#### Componentes

**Caixa de Diálogo**

```java
public void abrirDialogo(View v) {

	// CONFIGURAÇÃO DA CAIXA DE DIÁLOGO - CONDICIONAL
	AlertDialog.Builder builder = new AlertDialog.Builder(this);
	builder.seTitle("Exclusão");
	builder.setMessage("Deseja excluir?");
	
	// Se clicar em SIM
	builder.setPositiveButton("SIM", new DialogInterface.OnClickListener() {
		@Override
		public void onClick(DialogInterface dialog, int which) {
			Toast.makeText(MainActivity.this, "Elemento excluído", Toat.LENGTH_SHORT).show();
			return;	
		}
	});

	// Se clicar em NÃO
	builder.setNegativeButton("NÃO", new DialogInterface.OnClickListener() {
		@Override
		public void onClick(DialogInterface dialog, int which) {
			Toast.makeText(MainActivity.this, "Elemento NÃO FOI excluído", Toat.LENGTH_SHORT).show();
			return;	
		}
	});

	// APRESENTA CAIXA DE DIÁLOGO CRIADA
	AlertDialog dialogo = builder.create();
	dialogo.show();
}

```

**ListView**

```xml
<ListView
	android:id="@+id/lvDados"
	android:layout_width="match_parent"
	android:layout_height="match_parent" />
```

```java
@Override
protected void onCreate(Bundle savedInstanceState) {
	super.onCreate(savedInstanceState);
	setContentView(R.layout.activity_tela1);

	// Componente ListView
	lvDados = findViewById(R.id.lvDados);
	
	// Fonte de Dados
	String[] estados = {"SP","RJ","MG"};

	// Adaptador do ListView
	ArrayAdapter<String> adaptador = new ArrayAdapter<String> (
		this, android.R.layout.simple_list_item_1, estados);

	// Relacionando o adaptador ao comonente ListView
	lvDados.serAdapter(adaptador);

	// Implementação do evento click do item
	lvDados.setOnItemClickListener(new ArrayAdapter.OnItemClickeListener() {
		
		@Override
		protected void onItemClick(AdapterView<?> parent, View view, int position, long id) {
		// Recebe nome da lista
		String uf = String.valueOf(parent.getAdapter().getItem(position));
		Toast.makeText(Tela1.this, uf, Toast.LENGTH_SHORT).show();
		}
		
	});
	
}

```

**Spinner (Combobox)**

```xml
<Spinner
	android:id="@+id/spiDados"/>
```

```java
@Override
protected void onCreate(Bundle savedInstanceState) {
	super.onCreate(savedInstanceState);
	setContentView(R.layout.activity_tela1);

	// Componente Spinner
	spiDados = findViewById(R.id.spiDados);
	
	// Fonte de Dados
	String[] estados = {"SP","RJ","MG"};

	// Adaptador do Spinner
	ArrayAdapter<String> adaptador = new ArrayAdapter<String> (
		this, android.R.layout.simple_list_item_1, estados);

	// Relacionando o adaptador ao comonente ListView
	spiDados.serAdapter(adaptador);

	// Implementação do evento click do item
	spiDados.setOnItemClickListener(new ArrayAdapter.OnItemClickeListener() {
		
		@Override
		protected void onItemClick(AdapterView<?> parent, View view, int position, long id) {
		// Recebe nome da lista
		String uf = String.valueOf(parent.getAdapter().getItem(position));
		Toast.makeText(Tela1.this, uf, Toast.LENGTH_SHORT).show();
		}

		// Se nada for selecionado
		@Override
		protected void OnNothingSelected(AdapterView<?> parent) {
		}
		
	});
	
}

```

**Autocomplete**

```xml
<AutoCOmpleteTextView
	android:id="@+id/actNome"/>

----------------------------------
<!-- RECURSO DE STRING -->

<resources>
	<string name="app_name">ADComponentes</string>
	<string name="txtTitulo">Componentes</string>

	<string-array name="nomes-array">
		<item>Fulano</item>
		<item>Ciclano</item>
		<item>Beltrano</item>
	</string-array>
</resources>

```

```java
@Override
protected void onCreate(Bundle savedInstanceState) {
	super.onCreate(savedInstanceState);
	setContentView(R.layout.activity_tela3);

	actNome = findViewById(R.id.actNome);
	
	// Fonte de Dados - Acessar recursos de string
	Resources res = getResources();
	String[] planets = res.getStringArray(R.array.nomes_array);
	
	// Adaptador do Auto Complete
	ArrayAdapter<String> adaptador = new ArrayAdapter<String> (
			this, android.R.layout.simple_list_item_1, nomes);

	// Relaciona adaptador ao componente
	actNome.serAdapter(adaptador);
	actNome.setThreshold(1);

}

```
